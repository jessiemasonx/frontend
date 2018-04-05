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

__1. Tokenizing/Lexing:__    
Een string opbreken in stukjes. Die stukjes heten __tokens__.  
*Voorbeeld: `var a = 2;` Dit zou opgedeeld worden in deze tokens: `va`r, `a`, `=` en `;`*

__2. Parsing:__  
Tokens bij elkaar nemen (array) en die omzetten naar een boom van geneste elementen die de grammaticale structuur van het programma voorstellen. Deze boom heet "AST" (Abstraxt Syntax Tree).
*Voorbeeld: de boom voor `var a = 2;` kan beginnen met een top-level node VariableDeclaration, met een child node Identifier.*  
......idk

__3. Code-Generation:__   
Het proces van het pakken van een AST en het omzetten naar uitvoerbare code. Dit onderdeel varieert afhankelijk van de taal, het platform, etc.
*Voorbeeld: Er is een manier om de AST van `var a = 2;` te nemen en te veranderen in een set van machine instructies om een variable te maken die `a` heet, en dan een waarde in `a` te stoppen.*

Deze 3 stappen worden in deze volgorde uitgevoerd!!

## Call Stack / Call Site

Een call stack keten heeft meestal maximaal 10-15 jumps van de ene naar de andere functie en nog een andere.
Als je recursive programming gebruikt (een functie die zichzelf herhaaldelijk noemt), of mutual recursion (twee of meer functies roepen elkaar aan), kan de call stack gemakkelijk honderden, duizenden of meer niveaus diep zijn. Dit kan problemen opleveren.  
Javascript engines hebben een limiet zodat het niet crasht. Daarom krijgen we some `RangeError: Maximum call stack size exceeded`.

De call stack is van begin tot het eind. Call stack van C is bijvoorbeeld A B C. Niet C B A.

De call site is de plek waar het ding waar je de call site van vraagt wordt aangeroepen.

## LHS en RHS

LHS is declaratie  
RHS is assinging a value  

*Voorbeeld: `var a = 2`  
LHS: `var a`  
RHS: `a = 2`*

Als ze vragen om de LHS en de RHS van `function foo(a)` schrijf je `function foo` niet op maar alleen `a`.

## Parser

De parser declareert een var eerst aan het begin van de code, voordat die var een waarde krijgt.

code die ik schrijf:
```js
var a {
  naam: jessie,
  leeftijd: 19
}
```

Code hoe de parser het *leest*
```js
var a;

a {
  naam: jessie,
  leeftijd: 19
}
```

## Overeenkomsten SCOPE en DOM html

- Er wordt genest in scopes en in html. In scopes bijvoorbeeld functies in functies en bij de DOM bij elementen in elementen.
- __Grouperen.__ Dingen worden in html bij elkaar gezet in containers zoals divs en sections. In de scopes worden dingen bij elkaar gezet bijvoorbeeld in een scope dus een functie.

## Var en Let for loops
```js
for (var i = 0; i < 5; i++) {
}
```
```js
for (let i = 0; i < 5; i++) {
}
```
Als je let heb gebruikt kan je daar van buitenaf niks meer mee doen. Maar als je var hebt gebruikt kan je er nog wel bij.

Variable luistert niet naar block scope. Als var a en let b in een block scope een waarde geeft zal je je de var buiten de scope op kunnen roepen maar let niet. Als die var en die let in een function scope zitten, kunnen ze ALLEBIJ niet worden aangeroepen buiten die functie scope.

## Eval

In eval() kan je een string zetten.
De eval is een soort parser. Hij parst code.   
Als je eval() gebruikt kan je code-injection doen en kan een hacker jouw code gewoon aanpassen at runtime en daarom wordt het een beetje gezien als cheating.

De scope kan worden aangepast __at runtime__ door eval().

__eval = evil!!__

## Objecten

### Object literal
Dit is een object literal:
```js
var clown1 = {
    naam: 'Bassie',
    schoenmaat: 80,
    lach: 'whahaha'
};
```

Die dingen er in zoals naam een schoenmaat zijn `properties`.

### Constructor function

```js
function Clown (naam, schoenmaat, lach) { // constructor functie
  this.naam = naam;
  this.schonmaat: schoenmaat;
  this.lach = lach;

  this.laugh = function(){
    console.log('ik heet ' + this.naam + this.laughType );
  }
}

var pipo = new Clown('pipo', 80, 'whoehahahaha')

// nu krijg je terug, door die console.log: ik heet pipo whohahahaha
```

Nu geef je de waardes van de properties mee als we het object gaan maken.

### Syntactic sugar

```
'hoi' ${this}  
in plaats van
'hoi ' + this
```


### arrow functie

### literal

Een literal houdt in dat je *on the fly* aanmaakt.

```js
var clowns = new Array()
```

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

 Als je een nummer in een string bijvoorbeeld * 1 doet wordt het een number  
 En andersom wordt het ook een string

```js
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
