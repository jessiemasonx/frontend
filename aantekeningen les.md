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

