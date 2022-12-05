## Nappkin kadobonnen

Een restaurant dat gebruik maakt van [Nappkin](http://www.nappkin.nl) kan op zijn website kadobonnen aanbieden aan bezoekers. De betaling, verzending en administratie van de kadobon wordt geregeld door Nappkin met hulp van betalingsafhandelaar [Mollie](http://www.mollie.com). 

Dit document is bedoeld voor developers/designers die de website van een Nappkin gebruiker geschikt willen maken voor de verkoop van kadobonnen.

![coupon](https://github.com/nappkin/kadobon/blob/master/pkpass.png)

## Quick setup
De snelste en eenvoudigste manier om de website gereed te maken voor verkoop van kadobonnen is het opnemen van de volgende tags:
```
<script
    src='https://coupons.nappkin.nl/widget.js' 
    data-company='[COMPANY]'
    data-container='coupon-container'
    id='coupon-script'>
</script>
...
<div id='coupon-container'></div>
```
waarbij `[COMPANY]` het id is van het restaurant; dit kun je navragen bij help@nappkin.nl

Het script zorgt er voor dat de `div` met het id `coupon-container` wordt gevuld met widget html.

## Custom setup
Als je volledige controle wil over het design dan kan je via een script de verschillende typen kadobonnen opvragen en op basis daarvan een formulier genereren.

### Soorten 
De verschillende typen kadobonnen die door een restaurant worden aangeboden kun je opvragen met de volgende url
```
https://api.nappkin.nl/couponpass?company=[COMPANY]
```
waarbij `[COMPANY]` het id is van het restaurant; dit kun je navragen bij help@nappkin.nl

Het response is een array met informatie per type kadobon, of `404` als er nog geen kadobonnen zijn gedefinieerd:
```
[
    {
        "id": 1,
        "name": "Kadobon / Diner",
        "amount": 50,
        "type": "Money",
        "redirectUrl": "",
        "purchaseUrl": "https://api.nappkin.nl/couponpass?company=[COMPANY]&coupon=1&email=[EMAIL]&amount=[AMOUNT]&text=[TEXT]&count=1"
    },
    {
        "id": 2,
        "name": "All-in menu 5 gangen / Diner",
        "amount": 75,
        "type": "Event",
        "redirectUrl": "",
        "purchaseUrl": "https://api.nappkin.nl/couponpass?company=[COMPANY]&coupon=2&email=[EMAIL]&text=[TEXT]&count=1"
    },
    {
        "id": 3,
        "name": "All-in menu 6 gangen / Diner",
        "amount": 95,
        "type": "Money",
        "redirectUrl": "",
        "purchaseUrl": "https://api.nappkin.nl/couponpass?company=[COMPANY]&coupon=3&email=[EMAIL]&text=[TEXT]&count=1"
    }
]
```
#### `id`
Het unieke id van het type kadobon.

#### `name`
Omschrijving van de kadobon.

#### `amount`
De waarde van de kadobon.

#### `type`
Een kadobon is van het type `Money` of `Event`. Op een kadobon van het type `Money` staat de waarde van de bon in euros zichtbaar vermeld. De gebruiker zal met de kadobon een gedeelte van de rekening kunnen voldoen.<br/>Bij het type `Event` staat op de kadobon geen bedrag maar in plaats daarvan het aantal personen. De naam van kadobon is bij dit type een beschrijving van de geleverde dienst, zoals 'All-in 5 gangen menu'. De gebruiker zal behoudens uitzonderingen de hele rekening met de kadobon voldoen.

#### `redirectUrl`
De pagina op de restaurant website waar de gebruiker terecht komt nadat de iDEAL betaling is uitgevoerd. Dit kan dezelfde pagina zijn als de pagina waar de aankoop is gestart of een speciale pagina met een beschrijving van de voorwaarden etc.

#### `purchaseUrl`
De url waar de gebruiker naar geleid wordt om de kadobon te kopen. Dit endpoint retourneert vervolgens een redirect naar [Mollie](http://www.mollie.com) die zorgt voor de iDEAL flow. Het `[EMAIL]`adres moet opgevraagd worden bij de gebruiker.

Met een optionele `[AMOUNT]` parameter kan je een waarde opgeven die afwijkt van de standaard waarde van het kadobon-type. Als een `[TEXT]` parameter is opgenomen in de url dan wordt deze tekst op de kaart getoond in plaats van de standaard naam van het kadobontype. Deze twee optionele parameters zijn alleen van toepasssing bij een kadobon van het type `Money`.

### Formulier
De website van het restaurant moet minimaal een `input` element bevatten voor het email adres van de koper en een "koop" button. Als de koper op de button klikt moet hij naar de volgende url geleid worden:
```
https://api.nappkin.nl/couponpass?company=[COMPANY]&coupon=[COUPON]&email=[EMAIL]&amount=[AMOUNT]&text=[TEXT]&count=1
```
waarbij `[COUPON]` het `id` is van de kadobon (zie boven), `[EMAIL]` het ingevulde emailadres en `[COMPANY]` het Nappkin id van het restaurant. De parameters `[AMOUNT]` en `[TEXT]` zijn optioneel.


Als er meerdere soorten kadobonnen zijn moet de gebruiker een keuze kunnen maken, bijvoorbeeld met een `select` element. Je kunt hierbij gebruik maken van de velden `name` en `amount` in  bovengenoemde response.

#### `Money`
Bij een kadobon van het type `Money` is het mogelijk om een eigen tekst te tonen op de kaart, zoals "Verjaardag Piet". Daarnaast kan men zelf de gewenste waarde van de bon bepalen. Om deze gegevens op te vragen zullen `input` elementen moeten worden opgenomen op de site.

#### `Event`
Bij dit type moet de koper kunnen aangeven voor hoeveel personen de kadobon is. Dit is de `count` parameter in de `purchaseUrl`.

## Contact
Als je vragen hebt mail ons dan op help@nappkin.nl
