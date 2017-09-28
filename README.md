Om een kadobon te kunnen kopen zijn de volgende gegevens nodig:
- id van het restaurant
- emailadres van de koper
- id van het type kadobon

Het id van het restaurant kun je navragen bij help@nappkin.nl.

De verschillende typen kadobonnen kun je opvragen met de volgende url
```
https://cellarapp.apphb.com/api/v1/coupon?company=ID
```
waarbij `ID` het id is van het restaurant
Het response bevat informatie over de verschillende kadobonnen die het restaurant aanbiedt. 
```
{
    "info": "url: the address you should direct the user to upon clicking 'buy'",
    "coupons": [
        {
            "id": 3,
            "header": "Kadobon",
            "subheader": "Diner",
            "amount": 40,
            "url": "https://cellarapp.apphb.com/api/v1/coupon?company=449&coupon=3&email=xxxxx&count=1"
        },
        {
            "id": 5361,
            "header": "All-in 4 gangen menu",
            "subheader": "Diner",
            "amount": 75,
            "url": "https://cellarapp.apphb.com/api/v1/coupon?company=449&coupon=5361&email=xxxxx&count=1"
        },
        {
            "id": 5362,
            "header": "All-in 6 gangen menu",
            "subheader": "Diner",
            "amount": 100,
            "url": "https://cellarapp.apphb.com/api/v1/coupon?company=449&coupon=5362&email=xxxxx&count=1"
        }
    ]
}
```