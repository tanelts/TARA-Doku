---
permalink: Arikirjeldus
---

# Autentimisteenus TARA

Autentimisteenus TARA on Riigi Infosüsteemi Ameti poolt pakutav teenus, millega asutus saab oma e-teenusesse lisada nii siseriiklike kui ka Euroopa Liidu piiriüleste autentimismeetodite toe.

Siseriiklikest autentimismeetoditest pakume autentimist riikliku identiteedisüsteemiga:

- mobiil-ID
- ID-kaart

ja vahendame erasektori autentimismeetodeid: 

- Smart-ID
- Coop pank
- LHV pank
- Luminor pank
- SEB pank
- Swedbank

Samuti pakume välismaalase autentimist, eIDAS piiriülese autentimise skeemiga.

## Kellele?

 Avaliku sektori asutustele, kes soovivad:
- oma e-teenustes pakkuda kasutajatele laia valikut autentimismeetodeid, ise neid meetodeid teostamata.
- lisada oma e-teenusele piiriülese autentimise toe.

## Tehnilised tingimused?

- E-teenus liidestatakse autentimisteenusega OpenID Connect protokolli kohaselt.

## Kuidas liituda?

Asutusel tuleb:

1 välja selgitada, kas ja millistes e-teenustes RIA autentimisteenust tahab kasutada<br>

2 kavandada ja tellida liidestamistöö

- autentimiskomponendi täiendamine OpenID Connect-ga või väljavahetamine
- hinnanguline töömaht: kogenud arendajal u 2 päeva, kui OpenID Connect-i pole varem teinud, siis 2 nädalat.

3 teostada arendus<br>

4 esitada RIA-le taotlus teenusega liitumiseks<br>

- seejuures esitada kasutajate arvu prognoos
- RIA registreerib teie rakenduse teenuse kliendiks ja avab teile testteenuse.

5 testida liidest RIA testteenuse vastu

- RIA abistab võimalike probleemide lahendamisel

6 eduka testimise järel taodelda ühendamist toodanguteenusega

- RIA avab toodanguteenuse.

## Millal?

Testteenus on avatud 2017. a sügisest.

Teenus on toodangus avatud 2018. a märtsist.

## Kuidas teenus välja näeb?

<img src='img/KUVA-04.png' width='500'>

## Soovitused Riigi autentimisteenuse integreerimiseks kliendi teenuses:

- kui teenuses on kasutuses üksnes Riigi autentimisteenus (TARA), on soovituslik kasutada viidet “Sisene” koos paigutusega veebilehe paremal üleval servas

<img src='img/eesti_ee.png' width='500'>

- ainult eIDAS-liidestuse korral on soovituslik Riigi autentimisteenusele (TARA) suunamiseks kasutada viidet “EL kodanik” / “EU citizen” või kasutada logo <img src='img/eu_citizen_login_btn_190x50_rgb.png' width='80'> 

  (https://github.com/e-gov/TARA-Server/blob/master/disain/assets/eu_citizen_login_btn_190x50.svg)

- kui teenuses on kasutusel Riigi autentimisteenuse (TARA) kõrval ka teisi autentimisvahendeid, on soovituslik kasutada viitena RIA autentimisteenuse logo <img src='img/tara-logo-et.png' width='80'>  koos selgitusega “Sisene Riigi autentimisteenuse kaudu” või “Sisene läbi Riigi autentimisteenuse”.
  
  (https://github.com/e-gov/TARA-Server/blob/master/disain/assets/tara_logo.svg)

## Rohkem teavet?

Kontakt: `help@ria.ee`.

[Tehniline kirjeldus](TehnilineKirjeldus) (liidese arendajale).

      
