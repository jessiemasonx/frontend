# Aantekeningen alles

## Promises
Als er dingen na elkaar moeten gebeuren bij asynchrone code zoals een functie en als die wordt uitgevoerd een andere functie etc dan kan je callbacks in callbacks maken maar dat is heel lelijk en veel code. Je kan beter `.then` gebruiken. Dit hoort bij __promises__.  
Je kan een promise in een var stoppen.  
Een primise resolvet of reject altijd maar 1 keer.


```js
new Promise(function(resolve) {
  console.log('first');
  resolve();
  console.log('second');
}).then(function() {
  console.log('third');
})
```
bij `resolve` gebeurt het en bij `reject` gebeurt het niet.

ajax is asynchroon. Dan gebruik je promises.

Web workers zijn asynchroon.

## IIFE
__Immediatly invoked function expression__
```js
(function () {
})();
```
Het is een anonieme functie die gelijk 'invoked'(uitgevoerd) wordt.

## Hoisting

```js
a = 2;  

var a;  

console.log( a );
```
Door de hoisting lukt de bovenstaande code gewoon wel. `var a` gaat omhoog.   
Hoisting gebeurt binnen een scope. Dus als er een var in een functie zit gaat die var in die functie bovenaan.  
Zowel functies als vars worden gehoist. Maar een belamgrijk detail is dat eerst functies worden gehoist en daarna variabelen.

```js
foo(); // 1

var foo;

function foo() {
	console.log( 1 );
}

foo = function() {
	console.log( 2 );
};
```
wordt
```js
function foo() {
	console.log( 1 );
}

foo(); // 1

foo = function() {
	console.log( 2 );
};
```
## Tokenizing/Lexing, Parsing, Code-Generation

1. Tokenizing/Lexing:
Een string opbreken in stukjes. Die stukjes heten __tokens__.  
*Voorbeeld: `var a = 2;` Dit zou opgedeeld worden in deze tokens: `va`r, `a`, `=` en `;`*

2. Parsing:
Tokens bij elkaar nemen (array) en die omzetten naar een boom van geneste elementen die de grammaticale structuur van het programma voorstellen. Deze boom heet "AST" (Abstraxt Syntax Tree).
*Voorbeeld: de boom voor `var a = 2;` kan beginnen met een top-level node VariableDeclaration, met een child node Identifier.*
> idk

3. Code-Generation
Het proces van het pakken van een AST en het omzetten naar uitvoerbare code. Dit onderdeel varieert afhankelijk van de taal, het platform, etc.
*Voorbeeld: Er is een manier om de AST van `var a = 2;` te nemen en te veranderen in een set van machine instructies om een variable te maken die `a` heet, en dan een waarde in `a` te stoppen. 

Deze 3 stappen worden in deze volgorde uitgevoerd!! 

## kleine dingen

`'string'` , `function hoi(parameter)`

----------

`==	gelijk aaan
===	zelfde value en type
!=	net gelijk
!==	niet zelfde value of type
>	groter dan
<	kleiner dan
>=	groter of gelijk aan
<=	kleiner of gelijk aan
?	Conditional Operator. 1 van de 2 wordt uitgevoerd`

Het enige verschil tussen `==` en `===` is dat `==` elke soort *coercion* zou proberen om er voor te zorgen dat de 2 waardes matchen. `===` doet dit niet.

-----------

```js
null === undefined // false
null == undefined // true
null === null // true
 ```

 als je een nummer in een string bijvoorbeeld * 1 doet wordt het een number  
 En andersom wordt het ook een string

```
var a = '4' // '4'
b = a * 1 // 4
```
Typeof null is een object  
new alles is een object
```
typeof NaN === 'number';
typeof new Date() === 'object';
typeof null === 'object';
```
