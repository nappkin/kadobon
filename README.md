
Een restaurant kan op de website kadobonnen aanbieden aan bezoekers. De betaling en verzending van de kadobon wordt geregeld door Nappkin met hulp van betalingsafhandelaar Mollie.

Om een kadobon te kunnen kopen zijn de volgende gegevens nodig:
- id van het restaurant
- emailadres van de koper
- id van het type kadobon

Het id van het restaurant kun je navragen bij help@nappkin.nl.

## Soorten kadobonnen 
De verschillende typen kadobonnen  die door een restaurant worden aangeboden kun je opvragen met de volgende url
```
https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]
```
waarbij `[COMPANY]` het id is van het restaurant

Het response is een array met informatie per type kadobon:
```
[
    {
        "id": 3,
        "name": "Kadobon / Diner",
        "amount": 40,
        "redirectUrl": "",
        "url": "https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]&coupon=3&email=[EMAIL]&count=1"
    },
    {
        "id": 5361,
        "name": "Kadobon? / Diner",
        "amount": 0.01,
        "redirectUrl": "",
        "url": "https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]&coupon=5361&email=[EMAIL]&count=1"
    },
    {
        "id": 5362,
        "name": "Kadobonnetje / Diner",
        "amount": 50,
        "redirectUrl": "",
        "url": "https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]&coupon=5362&email=[EMAIL]&count=1"
    }
]
```
### purchaseUrl
De url waar de gebruiker naar geleid wordt om de kadobon te kopen. Dit endpoint retourneert vervolgens een redirect naar [Mollie](http://www.mollie.com) die zorgt voor de iDEAL flow.

### redirectUrl
De pagina op de restaurant website waar de gebruiker terecht komt nadat de iDEAL betaling is uitgevoerd. Dit kan dezelfde pagina zijn als de pagina waar de aankoop is gestart.

### amount
De waarde van de betreffende kadobon.

### name
Omschrijving van de kadobon.

## Formulier
De website van het restaurant moet minimaal een `input` element bevatten voor het email adres van de koper en een aankoopbutton. Als de koper op de aankoopbutton klikt moet de gebruiker naar de volgende url geleid worden:
```
https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]&coupon=[COUPON]&email=[EMAIL]&count=1
```
waarbij `[COUPON]` het id is van de kadobon.


Als er meerdere soorten kadobonnen zijn moet de gebruiker een keuze kunnen maken, bijvoorbeeld met een `select` element. 