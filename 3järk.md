---
permalink: 3JARK
---

# 3. arendusjärk ("eIDAS"). Lähteülesanne
{: .no_toc}

- TOC
{:toc}

## Mõisted

_eIDAS klient_, Java rakendus, millega proovime läbi siseriikliku liidestamise RIA eIDAS konnektorteenusega; seejärel lõimime eIDAS kliendi koodi TARA serverrakendusse. eIDAS klient on mõeldu ühtlasi mudeliks ja näiteks teistele konnektorteenuse külge ühenduda soovivatele asutustele. 

Märkus. Kasutame ka [sõnastiku](Sonastik) mõisteid.

## Eesmärk

3\. arendusjärgu eesmärk on lisada TARA-teenusele eIDAS piiriülese autentimise võimekus.

Arendusjärgu tulemusena peab  Eesti e-teenusel olema võimalik:<br>
a) saata välismaalane TARA ja eIDAS piiriülese autentimise taristu kaudu autentimiseks välisriigi autentimisteenusesse<br>
b) autentimiselt tagasisuunatud välismaalane vastu võtta<br>
c) ja saada kätte autentimist kinnitav eIDAS autentimistõend.

Arendusjärguga jätkame TARA-teenuse [1.](1JARK) ja [2.](2JARK) arendusjärguga (OpenID Connect põhine siseriiklik autentimisteenus ID-kaardi ja m-ID kasutajatele) tehtut.

## Arhitektuur

TARA-teenuse üldistatud komponentmudel (arendusjärgu lõpus) on esitatud joonisel 1. Joonisel 2 on esitatud eIDAS kliendi üldistatud komponentmudel.

<img src='img/3JARK.PNG' style='width: 600px;'>

Joonis 1. eIDAS-võimekusega TARA autentimisteenus

<img src='img/3-1.PNG' style='width: 600px;'>

Joonis 2. eIDAS klient

## TARA serverrakendus

1\. ja 2. arendusjärguga on loodud TARA serverrakendus, mis teostab Eesti e-teenust kasutava eestlase autentimist (joonisel 1 kasutusvoog 1). Suhtlus klientrakendusega toimub [OpenID Connect](Viited#1-1) protokolli kohaselt. TARA serverrakendus on ehitatud [CAS platvormile](Viited#3-1).

## Teostatav kasutusvoog

3\. arendusjärgu lõpuks tuleb teostada kasutusvoog `3a` ("Eesti e-teenust kasutava välismaalase autentimine TARA kaudu") (vt joonis 1). Kasutusvoog koosneb järgmistest sammudest:

1\. Välismaalane avaldab soovi TARA-ga liidestatud Eesti-e teenuses sisse logida.

2\. e-teenus (TARA suhtes klientrakendus) suunab välismaalase TARA teenusesse.<br>
\- suunamine tehakse veebisirvija ümbersuunamiskorralduse abil, vastavalt OpenID Connect protokollile. Vt [Tehniline kirjeldus](TehnilineKirjeldus).

3\. Välismaalane saabub TARA-teenusesse, autentimismeetodi valiku lehele.

4\. Välismaalane valib välisriigi.<br>
\- kui välisriigist osaleb eIDAS-skeemis mitu identiteedisüsteemi, siis valib ka identiteedisüsteemi.

5\. TARA-teenus koostab SAML autentimispäringu.<br>
\- TARA teenus allkirjastab ja sõltuvalt seadistusest ka krüpteerib autentimispäringu.

6\. TARA-teenus suunab välismaalase RIA eIDAS konnektorteenusesse.<br>
\- ümbersuunamiskorralduses pannakse kaasa SAML autentimispäring.

7\. RIA eIDAS konnektorteenus korraldab välismaalase suunamise välisriiki, autentima.

8\. RIA eIDAS konnektorteenus suunab välisriigist tagasi saabunud välismaalase tagasi TARA-teenusesse.<br>
\- tagasisuunamisega koos edastab RIA eIDAS konnektorteenus allkirjastatud - ja vastavalt seadistusele - krüpteeritud eIDAS autentimisvastuse.

9\. TARA-teenus võtab vastu tagasisuunatud välismaalase, dekrüpteerib autentimisvastuse ja kontrollib allkirja.

10\. TARA-teenus, vastavalt OpenID Connect protokollile (volituskoodi voog) edastab tulemuse klientrakendusele.

11\. Klientrakendus, eduka autentimise korral pärib, vastavalt OpenID Connect protokollile TARA-teenuselt identsustõendi.

12\. TARA-teenus väljastab identsustõendi.

Kasutusvoogu on kujutatud ka [RIA SSO autentimisteenuses kavandis](Viited#4-3) oleval järgnevusdiagrammil.

## Tööde koosseis

Tööde järgnevus:<br>
1) kõigepealt loome RIA eIDAS konnektorteenusega liidest teostava „eIDAS-kliendi“ (vt joonis 2)<br>
2) ja siis lõimime selle TARA teenusesse (CAS platvormil töötavasse TARA serverrakendusse).

Tuleb teostada järgmised tööd:

| nr |       töö       |  tulemus    | töömahu orientiir |
|----|-----------------|-------------|-------------------|
| 1  | RIA eIDAS konnektorteenuse siseriikliku poole spetsifitseerimine | tehniline spetsifikatsioon, mille järgi saab konnektorteenusega liidestada nii eIDAS kliendi, seejärel TARA-teenuse, aga ka teiste asutuste eIDAS-st kasutavad süsteemid | |
| 2  | RIA eIDAS konnektorteenuse seadistamine | konnektorteenus on valmis siseriiklike rakenduste liidestamiseks, vastavalt töös nr 1 koostatud spetsifikatsioonile | |
| 3  | autentimismeetodi valiku kuva täiendamine piiriülese autentimismeetodi valimisega | konfigureeritud ja ülalolevad välisriikide autentimismeetodid on kasutajale valitavad |  |
| 4  | SAML autentimispäringu moodustamine | TARA serverrakendus suudab moodustada korrektse SAML autentimispäringu. NB! Autentimispäringu vorming on spetsifitseeritud |  |
| 5  | välismaalase suunamine RIA eIDAS konnektorteenusesse | TARA serverrakendus suudab teha _browser redirect_-i RIA eIDAS konnektorteenusesse (SAML autentimispäring pannakse kaasa) |  |
| 6  | välismaalase vastuvõtmine RIA eIDAS konnektorteenusest | TARA serverrakendus suudab välismaalase RIA eIDAS konnektorteenusest vastu võtta |  |
| 7  | SAML autentimisvastuse dekrüpteerimine ja valideerimine | TARA serverrakendus suudab SAML autentimisvastuse dekrüpteerida ja valideerida |
| 8  | välismaalase tagasisuunamine autentimisrakendusse | TARA serverrakendus suudab välismaalase OpenID Connect _redirect_-ga klientrakendusse tagasi saata | | 
| 9  | identsustõendi moodustamine | TARA serverrakendus suudab moodustada korrektse OpenID Connect identsustõendi. Tõend jääb klientrakenduse järeletulemist ootama |
| 10  | identsustõendi väljastamine klientrakendusele | TARA serverrakendus suudab identsustõendi klientrakendusele väljastada |
| 11  | eIDAS nõuete kohased logimised (vrdl [eIDAS-Node Error and Event Logging](Viited#2-4)) | TARA-teenuse logimised vastavad nõuetele | |
| 12 | SAML metaandmeotspunkti teostus | TARA-teenus on publitseerinud oma SAML metaandmed |  |
| 13 | eIDAS kliendi lõimimine TARA-teenusesse | Eelmistes töödes arendatud eIDAS-klientrakendus on lõimitud TARA serverrakendusse. | |

Arendustööd hõlmavad:
- kavandamist, sh
  - tehnilist kavandamist
  - projektijuhtimist
- programmeerimist, sh
  - koodi läbivaatust
- testimist, vt Testistrateegia (eraldi dokument)
- dokumenteerimist.

Ettevalmistavate ja kaasnevate töödena:
- tutvumine olemasoleva TARA-teenuse dokumentatsiooniga ja koodiga
- tutvumine eIDAS Node tarkvara dokumentatsiooniga koodiga.

## Riskid

| nr   | risk | kirjeldus | ohuhinnang |
|------|------|-----------|-------------|
| 1    | eIDAS Node tarkvara ebastabiilsus | eIDAS konnektorteenuse tarkvara ei ole kahjuks veel stabiilne. Sept 2017 avaldati eIDAS Node v1.4. See versioon on RIAs paigaldatud. Euroopa Komisjonil on töös v2.0, milles suur muutus saab olema SAML 2-lt üleminek SAML 3.0-le (OpenSAML). Komisjoni sõnul v2.0 tuleb jaan-veebr 2018. | võib oluliselt ohustada töid (vajadus ümber teha) |
| 2    | eIDAS "protokolli" muutumine | Praegu kehtib eIDAS tehniline spetsifikatsioon v1.1. Kavas on seda uuendada, kuid tähtaegu teada ei ole. | Ohtu hindame väikeseks. |
| 3    | eIDAS Node tarkvara dokumentatsiooni puudulikkus | Komisjon on täiendanud eIDAS Node-i tehnilist dokumentatsiooni. Seda tehti meie soovi peale. Palgati professionaalne _technical writer_, kes on teinud head tööd. Siiski ei saa dokumentatsiooni lugeda perfektseks. | Ohtu meie töödele hindame keskmiseks. |
| 4    | raskused valitud platvormi tõttu | Vt [TARA tarkvara jätkusuutlikkus](Jatkusuutlikkus) | Hetke parima teadmise põhjal peame eIDAS-võimekust valitud platvormil teostatavaks. |
| 5    | testimine võib kujuneda ajamahukaks | Testimine hõlmab piiriüles end-to-end testimist. | |

## Lisa 1 Esimesed tööd

(sisendiks esimese sprindi planeerimisele)

1 eIDAS-kliendi kavandamine
- rakenduse arhitektuur
- komponendid-teegid
- UI lahendamise kava

2 Demo-SP uurimine
- selgitada välja, kuidas suhtleb konnektorteenusega
- hinnata, kas ja mida Demo-SP-st saaks kasutada eIDAS-kliendi ehitamisel

3 eIDAS tehnilise spetsifikatsiooni uurimine
- kõik neli dokumenti 

4 eIDAS-Node dokumentatsiooni uurimine
- eriti dokumendid:
  - eIDAS-Node National IdP and SP Integration Guide
  - eIDAS-Node ja SAML

5 konnektorteenuse siseriikliku liidese speki kavandamine

