#### Tips bij het lezen
- per hoofdstuk kijken
- kijken of dat overeen komt met conclusie
- zet er code bij als het relevant is

# Les 2

__IIFE__ Is een functie die zichzelf gelijk invoked. Dan hoef je 'm niet aan te roepen. Hij roept zichzelf gelijk aan. (function(). 

__Scope__ is waar variables worden opgeslagen. Waar je ze kan vinden. "Waar leeft een variable". Een set afspraken. Stel je hebt een functie a, en in die functie sla je een var b op. Dat betekend dat die var leeft in de scope van die functie. Dus als je een var in een functie definieert, leeft ie in de scope van die functie. Als je het in een blok definieert zit het in de globale scope. De globale scope is window. Maar die scope wordt afgeleid van de funtie window. En daarom zit je altijd in de functie scope van window.  

Een __referenceError__ betekent dat ie geen referentie kan vinden naar de variable. Dat krijg je dus als je je var in een functie maakt, en 'm buiten de functie aanroept.  

__Engin__ doet het werk. Zorgt er voor dat het programma wordt ingelezen en wordt doorgegeven aan de content. __LHS__ gaat over waar is de declaratie van de var. Wat is de container. En de __RHS__ gaat over wat de waarde is van die variable. Wat is er opgeslagen in de container. 

# Les 5

## This
[] array literal  
{} object literal  

Een object kan 2 dingen hebben
1. Properties -> key/ value pairs
2. Methods

```js
var clowns = [] // array literals
var clown = { // object literal
name: 'Pipo',
shoeSize: 80,
laugh: function(){
console.log('Ik heet ' + clown.name + ' whoehahahaha') // ik heet pipo whoehahahaha
}}
```

OF 

 ```js
var clowns = [] // array literals
var clown = { // object literal
name: 'Pipo',
shoeSize: 80,
laugh: function(){
console.log('Ik heet ' + this.name + ' whoehahahaha') // ik heet pipo whoehahahaha
}}
```

Hier staat er `this` ipv clown. In deze scope wordt `this` automatisch gegenereerd en het verwijst naar het object waar het op dit moment in zit. Ofterwel de context.

# Les 7


 met alleen {} maak je een block.
 ```js
 {
  content
 }
 ```
 Ook met if else, loop. Zijn ook `block`s. 
 
 Een `const` kan niet veranderen van type, maar kan wel een andere waarde krijgen. 
 
 `var body = document.body`
nu hebben we een html element  
```js
 body.addEventlistener('click', function(){
 
 console.log('de body was clicked') 
 })'
```
Dit is een `callback function` want je roept hem pas aan als er wordt geklikt.
 
arrow function `=>`
Als je this doet in de arrow function dan verwijst ie niet naar de functie maar naar de context er buiten. Dus bij het voorbeeld in de les verwees `this` naar the Window.
