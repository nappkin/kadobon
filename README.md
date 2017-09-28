Om een kadobon te kunnen kopen zijn de volgende gegevens nodig:
- id van het restaurant
- emailadres van de koper
- id van het type kadobon

Het id van het restaurant kun je navragen bij help@nappkin.nl.

# Soorten kadobon 
De verschillende typen kadobonnen kun je opvragen met de volgende url
```
https://cellarapp.apphb.com/api/v1/coupon?company={COMPANY}
```
waarbij `{COMPANY}` het id is van het restaurant
Het response bevat informatie over de verschillende kadobonnen die het restaurant aanbiedt. 
```
{
    "info": "url: the address you should direct the user to when clicking 'buy'",
    "coupons": [
        {
            "id": 3,
            "header": "Kadobon",
            "subheader": "Diner",
            "amount": 40,
            "url": "https://cellarapp.apphb.com/api/v1/coupon?company={COMPANY}&coupon=3&email={EMAIL}&count=1"
        },
        {
            "id": 5361,
            "header": "All-in 4 gangen menu",
            "subheader": "Diner",
            "amount": 75,
            "url": "https://cellarapp.apphb.com/api/v1/coupon?company={COMPANY}&coupon=5361&email={EMAIL}&count=1"
        },
        {
            "id": 5362,
            "header": "All-in 6 gangen menu",
            "subheader": "Diner",
            "amount": 100,
            "url": "https://cellarapp.apphb.com/api/v1/coupon?company={COMPANY}&coupon=5362&email={EMAIL}&count=1"
        }
    ]
}
```
`purchaseUrl`
De url waar de gebruiker naar geleid wordt om de kadobon te kopen. Dit endpoint doet vervolgens redirect naar [Mollie](http://www.mollie.com) die zorgt voor de iDEAL flow.

`redirectUrl`
De pagina op de restaurant website waar de gebruiker terecht komt nadat de iDEAL betaling is uitgevoerd. Dit kan dezelfde pagina zijn als de pagina waar de aankoop is gestart.

`amount`
De waarde van de betreffende kadobon

`name`
Omschrijving van de kadobon   