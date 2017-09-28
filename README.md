
Een restaurant dat gebruik maakt van [Nappkin](http://www.nappkin.nl) kan op zijn website kadobonnen aanbieden aan bezoekers. De betaling en verzending van de kadobon wordt geregeld door Nappkin met hulp van betalingsafhandelaar [Mollie](http://www.mollie.com). Dit document is bedoeld voor developers die de website van een Nappkin gebruiker geschikt willen maken voor de verkoop van kadobonnen.

![coupon](https://github.com/nappkin/kadobon/blob/master/pkpass.png)

## Soorten kadobonnen 
De verschillende typen kadobonnen  die door een restaurant worden aangeboden kun je opvragen met de volgende url
```
https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]
```
waarbij `[COMPANY]` het id is van het restaurant; dit kun je navragen bij help@nappkin.nl

Het response is een array met informatie per type kadobon, of `404` als er nog geen kadobonnen zijn gedefinieerd:
```
[
    {
        "id": 3,
        "name": "Kadobon / Diner",
        "amount": 40,
        "redirectUrl": "",
        "purchaseUrl": "https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]&coupon=3&email=[EMAIL]&count=1"
    },
    {
        "id": 5361,
        "name": "Kadobon? / Diner",
        "amount": 0.01,
        "redirectUrl": "",
        "purchaseUrl": "https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]&coupon=5361&email=[EMAIL]&count=1"
    },
    {
        "id": 5362,
        "name": "Kadobonnetje / Diner",
        "amount": 50,
        "redirectUrl": "",
        "purchaseUrl": "https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]&coupon=5362&email=[EMAIL]&count=1"
    }
]
```
#### id
Het unieke id van het type kadobon.

#### purchaseUrl
De url waar de gebruiker naar geleid wordt om de kadobon te kopen. Dit endpoint retourneert vervolgens een redirect naar [Mollie](http://www.mollie.com) die zorgt voor de iDEAL flow. Het `[EMAIL]`adres moet opgevraagd worden bij de gebruiker.

#### redirectUrl
De pagina op de restaurant website waar de gebruiker terecht komt nadat de iDEAL betaling is uitgevoerd. Dit kan dezelfde pagina zijn als de pagina waar de aankoop is gestart of een speciale pagina met een beschrijving van de voorwaarden etc.

#### amount
De waarde van de betreffende kadobon.

#### name
Omschrijving van de kadobon.

## Formulier
De website van het restaurant moet minimaal een `input` element bevatten voor het email adres van de koper en een aankoopbutton. Als de koper op de aankoopbutton klikt moet de gebruiker naar de volgende url geleid worden:
```
https://cellarapp.apphb.com/api/v1/coupon?company=[COMPANY]&coupon=[COUPON]&email=[EMAIL]&count=1
```
waarbij `[COUPON]` het `id` is van de kadobon (zie boven), `[EMAIL]` het ingevulde emailadres en `[COMPANY]` het Nappkin id van het restaurant.


Als er meerdere soorten kadobonnen zijn moet de gebruiker een keuze kunnen maken, bijvoorbeeld met een `select` element. Je kunt hierbij gebruik maken van de velden `name` en `amount` in  bovengenoemde response.

## Contact
Als je vragen hebt mail ons dan op help@nappkin.nl