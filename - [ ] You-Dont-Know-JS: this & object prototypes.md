# Chapter 1: this Or That?

De __this__ keyword. Het is een speciaal identifier keyword dat automatisch wordt gedefinieerd in de scope van elke functie, maar wat het previes doet hebben developers zelfs moeite mee.

Voorbeelden:
```js
   function identify() {  
  	return this.name.toUpperCase();
  }
  
  function speak() {
  	var greeting = "Hello, I'm " + identify.call( this );
  	console.log( greeting );
  }
