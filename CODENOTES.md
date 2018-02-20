#### Tips bij het lezen
- per hoofdstuk kijken
- kijken of dat overeen komt met conclusie
- zet er code bij als het relevant is

## Antwoord op Nina's vragen 
__IIFE__ Is een functie die zichzelf gelijk invoked. Dan hoef je 'm niet aan te roepen. Hij roept zichzelf gelijk aan. (function(). 

# aantekeningen les 2
__Scope__ is waar variables worden opgeslagen. Waar je ze kan vinden. "Waar leeft een variable". Een set afspraken. Stel je hebt een functie a, en in die functie sla je een var b op. Dat betekend dat die var leeft in de scope van die functie. Dus als je een var in een functie definieert, leeft ie in de scope van die functie. Als je het in een blok definieert zit het in de globale scope. De globale scope is window. Maar die scope wordt afgeleid van de funtie window. En daarom zit je altijd in de functie scope van window.  

Een __referenceError__ betekent dat ie geen referentie kan vinden naar de variable. Dat krijg je dus als je je var in een functie maakt, en 'm buiten de functie aanroept.  

__Engin__ doet het werk. Zorgt er voor dat het programma wordt ingelezen en wordt doorgegeven aan de content. __LHS__ gaat over waar is de declaratie van de var. Wat is de container. En de __RHS__ gaat over wat de waarde is van die variable. Wat is er opgeslagen in de container. 

# Samenvatting Tekst les 1
Scope is the set of rules that determines where and how a variable (identifier) can be looked-up. This may be for the purposes of assigning to the variable, which is an LHS (left-hand-side) reference, or it may be for the purposes of retrieving its value, which is an RHS (right-hand-dise) reference.  

## Compiler Theory

The JavaScript engine performs many of the same steps, albeit in more sophisticated ways than we may commonly be aware, of any traditional language-compiler. In a traditional compiled-language process, a chunk of source code, your program, will undergo typically three steps before it is executed, roughly called "compilation":

__1. Tokenizing/Lexing:__
This is breaking up a string of characters in to meaningful chuncks, called __tokens__.  
*Example: var a = 2; This would be broken up into the folling tokens: var, a, = and ;.*
__1. Parsing:__  
Taking a stream (array) of tokens and turning it into a tree of nested elements which represent the grammatical structure of the program. This tree is called __"AST"__ (Abstract Syntax Tree).
*Example: the tree for var a = 2; might start with a top-level node called VariableDeclaration, with a child node called Indentifier*


# You Don't Know JS: Types & Grammar

- [Chapter 1: Types](https://github.com/jessiemasonx/frontend/blob/master/CODENOTES.md#chapter-1-types)  
- [Chapter 2: Values](https://github.com/jessiemasonx/frontend/blob/master/CODENOTES.md#chapter-2-values)  
- [Chapter 3: Natives](https://github.com/jessiemasonx/frontend/blob/master/CODENOTES.md#chapter-3-natives)    
- [Chapter 4: Coercion](https://github.com/jessiemasonx/frontend/blob/master/CODENOTES.md#chapter-4-coercion) 
- [Chapter 5: Grammar](https://github.com/jessiemasonx/frontend/blob/master/CODENOTES.md#chapter-5-grammar)    

## Chapter 1: Types

### Built-in Types
JavaScript defines seven built-in types:
	•	null
	•	undefined
	•	boolean
	•	number
	•	string
	•	object
	•	symbol -- added in ES6!

The typeof operator inspects the type of the given value, and always returns one of seven string values. 
Functions are actually objects. So are Arrays.

### Values as Types
In JavaScript, variables don't have types -- values have types. Variables can hold any value, at any time.
The value 42 has an intrinsic type of number, and its type cannot be changed. Another value, like "42" with the string type, can be created from the number value 42 through a process called __coercion__.

If you use typeof against a variable, it's not asking *”what’s the type of the variable?”* as it may seem, since JS variables have no types. Instead, it's asking *”what’s the type of the __value__ in the variable?”*

#### undefined vs "undeclared"
Variables that have no value currently, actually have the undefined value. Calling typeof against such variables will return “undefined”. It's tempting for most developers to think of the word *undefined* and think of it as a synonym for *undeclared*. However, in JS, these two concepts are quite different.

An __undefined__ variable is one that has been declared in the accessible scope, but at the moment has no other value in it. By contrast, an __undeclared__ variable is one that has not been formally declared in the accessible scope.

var a;  
a; // undefined  
b; // ReferenceError: b is not defined  

Here b is undeclared. 

Another special behaviour: The typeof operator returns "undefined" even for "undeclared" (or "not defined") variables.

## Chapter 2: Values
### Arrays
 JavaScript arrays are just containers for any type of value, from string to number to object to even another array

Be careful about creating "sparse" arrays (leaving or creating empty/missing slots). Arrays are numerically indexed (as you'd expect), but the tricky thing is that they also are objects that can have stringkeys/properties added to them (but which don't count toward the length of the array). 

#### Array-Likes
There will be occasions where you need to convert an array-like value (a numerically indexed collection of values) into a true array, usually so you can call array utilities (like indexOf(..), concat(..), forEach(..), etc.) against the collection of values.

### Strings
Strings do have a shallow resemblance to arrays -- array-likes, as above. For instance, both of them having a length property, an indexOf(..) method, and a concat(..) method.  So, they're both basically just "arrays of characters", right? __Not exactly__:


Een consequentie van onveranderlijke __strings__ is dat geen van de *string methods*  die de inhoud wijzigen, de inhoud van de string op zijn plaats kan wijzigen. Maar eerder nieuwe reeksen moet maken en retourneren. Veel van de methoden die de __array__-inhoud wijzigen, veranderen daarentegen wel op hun plaats. 

Nog een voorbeeld: reversing a string. Arrays have a reverse() in-place mutator method, but strings do not:  

a.reverse;		// undefined  

> b.reverse();	                // ["!","o","O","f"]  
> b;				// [“!","o","O","f"]

### Numbers
JavaScript has just one numeric type: number. This type includes both "integer" values and fractional decimal numbers. 

#### Numeric Syntax
Number literals are expressed in JavaScript generally as base-10 decimal literals.

Very large or very small numbers will by default be outputted in exponent form, the same as the output of the toExponential() method, like:

> var a = 5E10;  
> a;					// 50000000000  
> a.toExponential();	// "5e+10"  

> var b = a * a;  
> b;					// 2.5e+21  

> var c = 1 / a;  
> c;					// 2e-11  

Number values can access methods that are built into the Number.prototype. 
Voorbeeld: toFixed(..) method. Geeft aan met hoeveel decimalen u de waarde wilt laten weergeven:
var a = 42.59;

> a.toFixed( 0 ); // "43"  
> a.toFixed( 1 ); // "42.6"  
> a.toFixed( 2 ); // "42.59"  
> a.toFixed( 3 ); // "42.590"  
> a.toFixed( 4 ); // "42.5900"

toPrecision(..) lijkt er op, maar geeft aan hoe veel *significant digits* moeten worden gebruikt om de waarde aan te geven:
var a = 42.59;

> a.toPrecision( 1 ); // "4e+1"  
> a.toPrecision( 2 ); // "43"  
> a.toPrecision( 3 ); // "42.6"  
> a.toPrecision( 4 ); // "42.59"  
> a.toPrecision( 5 ); // "42.590"  
> a.toPrecision( 6 ); // "42.5900"  

number literals can also be expressed in other bases, like binary, octal, and hexadecimal:

> 0xf3; // hexadecimal for: 243  
> 0Xf3; // ditto  
> 0363; // octal for: 243

### Small Decimal Value
The most (in)famous side effect of using binary floating-point numbers is:
0.1 + 0.2 === 0.3; // false

Why is it false?  It's really close: 0.30000000000000004. but if your comparison fails, "close" is irrelevant.

### Safe Integer Ranges
Because of how numbers are represented, there is a range of "safe" values for the whole number "integers", and it's significantly less than Number.MAX_VALUE. The maximum integer that can "safely" be represented is __2^53 - 1__, which is 9007199254740991.

### Testing for Integers
To test if a value is an integer, you can use the ES6-specified Number.isInteger(..):

Number.isInteger( 42 );		// true  
Number.isInteger( 42.000 );	// true  
Number.isInteger( 42.3 );	// false  

To test if a value is a safe integer, use the ES6-specified Number.isSafeInteger(..):
Number.isSafeInteger( Number.MAX_SAFE_INTEGER );	// true
Number.isSafeInteger( Math.pow( 2, 53 ) );			// false
Number.isSafeInteger( Math.pow( 2, 53 ) - 1 );		// true

### 32-bit (Signed) Integers
While integers can range up to roughly 9 quadrillion safely, there are some numeric operations that are only defined for 32-bit numbers, so the "safe range" for numbers used in that way must be much smaller.
The range then is Math.pow(-2,31) (-2147483648, about -2.1 billion) up to Math.pow(2,31)-1 (2147483647, about +2.1 billion).

## Special Values
There are several special values spread across the various types that the alert JS developer needs to be aware of, and use properly.

### The Non-value Values
For the undefined type, there is one and only one value: undefined. For the null type, there is one and only one value: null. So for both of them, the label is both its type and its value.   

Both undefined and null are often taken to be interchangeable as either "empty" values or "non" values. Other developers prefer to distinguish between them with nuance. For example:
	•	null is an empty value
	•	undefined is a missing value
Or:
	•	undefined hasn't had a value yet
	•	null had a value and doesn't anymore

### Undefined
In de non-*strict* modus is het eigenlijk mogelijk om een ​​waarde toe te kennen aan de *undefined* identifier.
function foo() {
	undefined = 2; // really bad idea!
}

foo();

__Friends don't let friends override undefined. Ever.__

#### void Operator
While undefined is a built-in identifier that holds the built-in undefined value, another way to get this value is the void operator.

De uitdrukking __void__ ___ maakt elke waarde ongeldig, zodat het resultaat van de uitdrukking altijd de undefined value is. Het wijzigt de bestaande waarde niet; het zorgt er alleen voor dat er geen waarde meer terugkomt van de operator expression.
var a = 42;

console.log( void a, a ); // undefined 42

> snap dit void gedeelte niet zo goed dus er is een groot deel geslipt

### Special Numbers
Het number type bevat verschillende speciale waarden.

#### The Not Number, Number
__NaN__ literally stands for *not a number*. It would be much more accurate to think of NaN as being "invalid number," "failed number," or even "bad number," than to think of it as "not a number."

var a = 2 / "foo";		// NaN  
typeof a === "number";	// true

In other words: "the type of not-a-number is 'number'!" Hooray for confusing names and semantics. NaN is a kind of "sentinel value" that represents a special kind of error condition within the number set. The error condition is, in essence: "I tried to perform a mathematic operation but failed, so here's the failed number result instead.
NaN is a very special value in that it's never equal to another NaN value. NaN is the only value in the whole language where that's true; every other value is always equal to itself.

#### Infinities
Developers from traditional compiled languages like C are probably used to seeing either a compiler error or runtime exception, like "Divide by zero,”. However, in JS, this operation is well-defined and results in the value __Infinity__.

#### Zeros
While it may confuse the mathematics-minded reader, JavaScript has both a *normal zero* 0(positive zero +0) and a *negative zero* -0.

Besides being specified literally as -0, negative zero also results from certain mathematic operations. For example:
var a = 0 / -3; // -0  
var b = 0 * -3; // -0  

However, if you try to stringify a negative zero value, it will always be reported as "0", according to the spec.

a;							// -0
a.toString();				// "0"


### Special Equality
As of ES6, there's a new utility that can be used to test two values for absolute equality, without any of these exceptions. It's called __Object.is(..)__:

Object.is( a, NaN );	// true  
Object.is( b, -0 );		// true

Object.is(..) probably shouldn't be used in cases where == or === are known to be safe, as the operators are likely much more efficient and certainly are more idiomatic/common. Object.is(..) is mostly for these special cases of equality.

### Value vs. Reference
In many other languages, values can either be assigned/passed by value-copy or by reference-copy depending on the syntax you use.

> …

## Chapter 3: Natives

Here's a list of the most commonly used natives:

- String()
- Number()
- Boolean()
- Array()
- Object()
- Function()
- RegExp()
- Date()
- Error()
- Symbol()

As you can see, these natives are actually built-in functions.

The result of the constructor form of value creation (new String("abc")) is an object wrapper around the primitive ("abc") value.

### Internal [[Class]]
Values that are typeof "object" (such as an array) are additionally tagged with an internal [[Class]] property. This property cannot be accessed directly, but can generally be revealed indirectly by borrowing the default Object.prototype.toString(..) method called against the value. 

> Object.prototype.toString.call( [1,2,3] );			// "[object Array]"

So, for the array in this example, the internal [[Class]] value is "Array".

### Boxing Wrappers

These object wrappers serve a very important purpose. Primitive values don't have properties or methods, so to access .length or .toString() you need an object wrapper around the value. Thankfully, JS will automatically box (aka wrap) the primitive value to fulfill such accesses.

> var a = "abc";  

> a.length; // 3  
> a.toUpperCase(); // "ABC"

#### Object Wrapper Gotchas

There are some gotchas with using the object wrappers directly that you should be aware of if you do choose to ever use them.

For example, consider *Boolean* wrapped values:

> var a = new Boolean( false );

> if (!a) {
> 	console.log( "Oops" ); // never runs
> }

The problem is that you've created an object wrapper around the *false* value, but objects themselves are *"truthy"*, so using the object behaves oppositely to using the underlying false value itself, which is quite contrary to normal expectation.

### Unboxing
If you have an object wrapper and you want to get the underlying primitive value out, you can use the __valueOf()__ method:

> var a = new String( "abc" );
> var b = new Number( 42 );
> var c = new Boolean( true );

> a.valueOf(); // "abc"
> b.valueOf(); // 42
> c.valueOf(); // true

Unboxing can also happen implicitly, when using an object wrapper value in a way that requires the primitive value. This process (coercion) will be covered in more detail in Chapter 4, but briefly:

> var a = new String( "abc" );
> var b = a + ""; // `b` has the unboxed primitive value "abc"

> typeof a; // "object"
> typeof b; // "string"

### Natives as Constructors
For array, object, function, and regular-expression values, it's almost universally preferred that you use the literal form for creating the values, but the literal form creates the same sort of object as the constructor form does.

#### Array(..)
> var a = new Array( 1, 2, 3 );
> a; // [1, 2, 3]

> var b = [1, 2, 3];
> b; // [1, 2, 3

Firefox reports [ , , , ] for a and c. Did you catch why that's so confusing? Look closely. Three commas implies four slots, not three slots like we'd expect.

*hier is een lang stuk over alles dat niet werkt en het is nogal verwarrend*

#### Object(..), Function(..), and RegExp(..)

The Object(..)/Function(..)/RegExp(..) constructors are also generally optional (and thus should usually be avoided unless specifically called for):

> var c = new Object();
> c.foo = "bar";
> c; // { foo: "bar" }

> var d = { foo: "bar" };
> d; // { foo: "bar" }

> var e = new Function( "a", "return a * 2;" );
> var f = function(a) { return a * 2; };
> function g(a) { return a * 2; }

> var h = new RegExp( "^a*b+", "g" );
> var i = /^a*b+/g;

There's practically no reason to ever use the new Object() constructor form, especially since it forces you to add properties one-by-one instead of many at once in the object literal form.

The Function constructor is helpful only in the rarest of cases, where you need to dynamically define a function's parameters and/or its function body. Do not just treat Function(..) as an alternate form of eval(..). You will almost never need to dynamically define a function in this way.

#### Date(..) and Error(..)

The Date(..) and Error(..) native constructors are much more useful than the other natives, because there is no literal form for either. To create a date object value, you must use new Date(). The Date(..) constructor accepts optional arguments to specify the date/time to use, but if omitted, the current date/time is assumed.

#### Symbol(..)

New as of ES6, an additional primitive value type has been added, called "Symbol". Symbols are special "unique" values that can be used as properties on objects with little fear of any collision. 

There are several predefined symbols in ES6, accessed as static properties of the Symbol function object, like Symbol.create, Symbol.iterator, etc. To use them, do something like:

> obj[Symbol.iterator] = function(){ /*..*/ };

### Native Prototypes

Each of the built-in native constructors has its own .prototype object -- Array.prototype, String.prototype, etc.  
These objects contain behavior unique to their particular object subtype.

> NIKS KOMT BINNEN.NL

## Chapter 4: Coercion

> snap function onlyOne(a,b,c) niet
### Converting Values
It may not be obvious, but JavaScript coercions always result in one of the scalar primitive values, like string, number, or boolean. There is no coercion that results in a complex value like object or function. 

The difference should be obvious: __explicit coercion__ is when it is obvious from looking at the code that a type conversion is intentionally occurring, whereas __implicit coercion__ is when the type conversion will occur as a less obvious side effect of some other intentional operation.

For example, consider these two approaches to coercion:

> var a = 42;  
> var b = a + "";			// implicit coercion  
> var c = String( a );           	// explicit coercion

For b, the coercion that occurs happens implicitly, because the + operator combined with one of the operands being a string value ("") will insist on the operation being a *string concatenation* (adding two strings together), which as a (hidden) side effect will force the 42 value in a to be coerced to its string equivalent: "42".  
The String(..) function makes it pretty obvious that it's explicitly taking the value in a and coercing it to a string representation.

### Abstract Value Operations

We need to learn the basic rules that govern how values become either a string, number, or boolean. We will specifically pay attention to: ToString, ToNumber, and ToBoolean, and to a lesser extent, ToPrimitive.

#### ToString

When any non-string value is coerced to a string representation, the conversion is handled by the ToString abstract operation in section 9.8 of the specification.
> a.toString(); // "1.07e21" 
> het zet er haakjes omheen. maakt het dus een string

__JSON Stringification__

Another task that seems awfully related to ToString is when you use the JSON.stringify(..) utility to serialize a value to a JSON-compatible string value.For most simple values, JSON stringification behaves basically the same as toString() conversions, except that the serialization result is always a string:

> JSON.stringify( 42 );	// "42"  
> JSON.stringify( "42" );	// ""42"" (a string with a quoted string value in it)

> __JSON.stringify(..) ??__

### ToNumber

For example, true becomes 1 and false becomes 0. undefined becomes NaN, but (curiously) null becomes 0.

> var c = [4,2];  
> c.toString = function(){  
> 	return this.join( "" );	// "42"  
> };
>   
> Number( c );			// 42  
> Number( "" );			// 0  
> Number( [] );			// 0  
> Number( [ "abc" ] );	// NaN

### ToBoolean

First and foremost, JS has actual keywords true and false, and they behave exactly as you'd expect of boolean values. It's a common misconception that the values 1 and 0 are identical to true/false. While that may be true in other languages, in JS the numbers are numbers and the booleans are booleans. You can coerce 1 to true (and vice versa) or 0 to false (and vice versa). But they're not the same.

> var a = new Boolean( false );  
> var b = new Number( 0 );  
> var c = new String( "" );  
We know all three values here are objects (see Chapter 3) wrapped around obviously falsy values. But do these objects behave > as true or as false? That's easy to answer:  
>   
> var d = Boolean( a && b && c );  
>  
> d; // true  

So, all three behave as true, as that's the only way d could end up as true.

## Explicit Coercion

__Explicit coercion__ refers to type conversions that are obvious and explicit. There's a wide range of type conversion usage that clearly falls under the explicit coercion category for most developers.

### Explicitly: Strings <--> Numbers

To coerce between strings and numbers, we use the built-in String(..) and Number(..) functions, but very importantly, we do not use the new keyword in front of them. As such, we're not creating object wrappers.

Instead, we're actually explicitly coercing between the two types:

> var a = 42;  
> var b = String( a );  
>  
> var c = "3.14";  
> var d = Number( c );  
  
> b; // "42"  
> d; // 3.14  

I call this __explicit coercion__ because in general, it's pretty obvious to most developers that the end result of these operations is the applicable type conversion.

Besides String(..) and Number(..), there are other ways to "explicitly" convert these values between string and number:

>  var a = 42;  
>  var b = a.toString();  
>  
>  var c = "3.14";  
>  var d = +c;  
>  
>  b; // "42"  
>  d; // 3.14  

+c here is showing the unary operator form (operator with only one operand) of the + operator. Instead of performing mathematic addition (or string concatenation -- see below), the unary + explicitly coerces its operand (c) to a number value. 
Is +c explicit coercion? Depends on your experience and perspective. If you know that unary + is explicitly intended for number coercion, then it's pretty explicit and obvious. However, if you've never seen it before, it can seem awfully confusing, implicit, with hidden side effects, etc.

### Date To number

Another common usage of the unary + operator is to coerce a Date object into a number, because the result is the unix timestamp *(milliseconds elapsed since 1 January 1970 00:00:00 UTC)* representation of the date/time value:

> var d = new Date( "Mon, 18 Aug 2014 08:53:06 CDT" );  
> +d; // 1408369986000

The most common usage of this idiom is to get the current now moment as a timestamp, such as:

> var timestamp = +new Date();

__The Curious Case of the ~__

One coercive JS operator that is often overlooked and usually very confused is the tilde ~ operator.  
Using bitwise operators (like | or ~) with certain special number values produces a coercive effect that results in a different number value.  

For example, let's first consider the | "bitwise OR" operator used in the otherwise no-op idiom 0 | x, which (as Chapter 2 showed) essentially only does the ToInt32 conversion:

> 0 | -0;			// 0  
> 0 | NaN;		// 0  
> 0 | Infinity;	// 0  
> 0 | -Infinity;	// 0  

So, let's turn our attention back to ~. The ~ operator first "coerces" to a 32-bit number value, and then performs a bitwise negation (flipping each bit's parity).  
This is very similar to how ! not only coerces its value to boolean but also flips its parity.


Let's try again: ~x is roughly the same as -(x+1). That's weird, but slightly easier to reason about. So:

> ~42;	// -(42+1) ==> -43  

t's pretty common to try to use indexOf(..) not just as an operation to get the position, but as a boolean check of presence/absence of a substring in another string. Here's how developers usually perform such checks: 

> var a = "Hello World";  
  
> if (a.indexOf( "lo" ) >= 0) {	// true  
> 	// found it!  

There's one more place ~ may show up in code you run across: some developers use the double tilde ~~ to truncate the decimal part of a number (i.e., "coerce" it to a whole number "integer"). It's commonly (though mistakingly) said this is the same result as calling Math.floor(..).

### Explicitly: Parsing Numeric Strings

A similar outcome to coercing a string to a number can be achieved by __parsing__ a number out of a string's character contents. There are, however, distinct differences between this parsing and the type conversion we examined above.

> var a = "42";  
> var b = "42px";  
>   
> Number( a );	// 42  
> parseInt( a );	// 42  
>  
> Number( b );	// NaN  
> parseInt( b );	// 42  

Parsing should not be seen as a substitute for coercion. These two tasks, while similar, have different purposes. Parse a string as a number when you don't know/care what other non-numeric characters there may be on the right-hand side. Coerce a string (to a number) when the only acceptable values are numeric and something like "42px" should be rejected as a number.

#### Parsing Non-Strings

One somewhat infamous example of parseInt(..)'s behavior is highlighted in a sarcastic joke post a few years ago, poking fun at this JS behavior:

>  parseInt( 1/0, 19 ); // 18

> heeel veel overgeslagen want snap t niet

### Explicitly: * --> Boolean

Just like with String(..) and Number(..) above, Boolean(..) is an explicit way of forcing the ToBoolean coercion:

> var a = "0";  
> var b = [];  
> var c = {};  
>  
> var d = "";  
> var e = 0;  
> var f = null;  
> var g;  
>  
> Boolean( a ); // true  
> Boolean( b ); // true  
> Boolean( c ); // true  
> 
> Boolean( d ); // false  
> Boolean( e ); // false  
> Boolean( f ); // false  
> Boolean( g ); // false  

### Implicit Coercion

Implicit coercion refers to type conversions that are hidden, with non-obvious side-effects that implicitly occur from other actions. In other words, implicit coercions are any type conversions that aren't obvious (to you).

#### Simplifying Implicitly

Before we even get to JavaScript, let me suggest something pseudo-code'ish from some theoretical strongly typed language to illustrate:

> SomeType x = SomeType( AnotherType( y ) )

In this example, I have some arbitrary type of value in y that I want to convert to the SomeType type. The problem is, this language can't go directly from whatever y currently is to SomeType. It needs an intermediate step, where it first converts to AnotherType, and then from AnotherType to SomeType.

Now, what if that language (or definition you could create yourself with the language) did just let you say:

> SomeType x = SomeType( y )

Wouldn't you generally agree that we simplified the type conversion here to reduce the unnecessary "noise" of the intermediate conversion step?

> ?  
> ?  
> ???????

#### Implicitly: Strings <--> Numbers

Earlier in this chapter, we explored explicitly coercing between string and number values. Now, let's explore the same task but with implicit coercion approaches.

The + operator is overloaded to serve the purposes of both number addition and string concatenation. So how does JS know which type of operation you want to use? Consider:
> var a = "42";  
> var b = "0";  
> var c = 42;  
> var d = 0;  
>  
> a + b; // "420"  
> c + d; // 42  

What's different that causes "420" vs 42? It's a common misconception that the difference is whether one or both of the operands is a string, as that means + will assume string concatenation. While that's partially true, it's more complicated than that.

You can coerce a number to a string simply by "adding" the number and the "" empty string:

> var a = 42;  
> var b = a + "";  
>  
> b; // "42"

What about the other direction? How can we implicitly coerce from string to number?

> var a = "3.14";  
> var b = a - 0;  
>   
> b; // 3.14  

What about object values with the - operator? Similar story as for + above:

> var a = [3];  
> var b = [1];  
>  
> a - b; // 2  

### Implicitly: Booleans --> Numbers

Ik denk dat een geval waarin __implicit coercion__ echt kan schijnen, het vereenvoudigen van bepaalde typen gecompliceerde boolean logica in eenvoudige numerieke optelling is. Dit is natuurlijk geen algemene techniek, maar een specifieke oplossing voor specifieke gevallen.
 
> function onlyOne(a,b,c) {  
> 	return !!((a && !b && !c) ||  
> 		(!a && b && !c) || (!a && !b && c));  
> }  
>  
> var a = true;  
> var b = false;  
>   
> onlyOne( a, b, b );	// true  
> onlyOne( b, a, b );	// true  
>  
> onlyOne( a, b, a );	// false  

This __onlyOne(..)__ utility should only return true if exactly one of the arguments is true / truthy. It's using __implicit coercion__ on the truthy checks and explicit coercion on the others, including the final return value.

But what if we needed that utility to be able to handle four, five, or twenty flags in the same way? Here's where coercing the boolean values to numbers (0 or 1, obviously) can greatly help:

> for (var i=0; i < arguments.length; i++) {  
> 		// skip falsy values. same as treating   
> 		// them as 0's, but avoids NaN's.  
> 		if (arguments[i]) {  
> 			sum += arguments[i];  
> 		}

What we're doing here is relying on the 1 for true/truthy coercions, and numerically adding them all up. sum += arguments[i] uses implicit coercion to make that happen. If one and only one value in the arguments list is true, then the numeric sum will be 1, otherwise the sum will not be 1 and thus the desired condition is not met.

We could of course do this with explicit coercion instead:

> function onlyOne() {
> 	var sum = 0;
> 	for (var i=0; i < arguments.length; i++) {
> 		sum += Number( !!arguments[i] );
> 	}
> 	return sum === 1;
> }

We first use !!arguments[i] to force the coercion of the value to true or false. That's so you could pass non-boolean values in, like onlyOne( "42", 0 ), and it would still work as expected (otherwise you'd end up with string concatenation and the logic would be incorrect).  
Once we're sure it's a boolean, we do another explicit coercion with Number(..) to make sure the value is 0 or 1.

### Implicitly: * --> Boolean

What sort of expression operations require/force (implicitly) a boolean coercion?

1. The test expression in an if (..) statement.
2. The test expression (second clause) in a for ( .. ; .. ; .. ) header.
3. The test expression in while (..) and do..while(..) loops.
4. The test expression (first clause) in ? : ternary expressions.
5. The left-hand operand (which serves as a test expression -- see below!) to the || ("logical or") and && ("logical and") operators.

Any value used in these contexts that is not already a boolean will be implicitly coerced to a boolean using the rules of the ToBoolean abstract operation covered earlier.

var a = 42;
var b = "abc";
var c;
var d = null;


> if (a) {  
> 	console.log( "yep" );		// yep  
> }  
>    
> while (c) {  
> 	console.log( "nope, never runs" );  
> }  
>  
> c = d ? a : b;  
> c;					// "abc"  
>  
> if ((a && d) || c) {  
> 	console.log( "yep" );		// yep  
> }  



In all these contexts, the non-boolean values are implicitly coerced to their boolean equivalents to make the test decisions.

### Operators || and &&

__||__ logical or  
__&&__ logical and

I'd call them "selector operators," or more completely, "operand selector operators". Because they don't actually result in a logic value (aka boolean) in JavaScript, as they do in some other languages.  
They result in the value of one (and only one) of their two operands. In other words, they __select one of the two operand's values__.

> var a = 42;  
> var b = "abc";  
> var c = null;  
>  
> a || b;		// 42  
> a && b;		// "abc"  
>  
> c || b;		// "abc"  
> c && b;		// null  

__Wait, what!?__.  In languages like C and PHP, those expressions result in true or false, but in JS, the result comes from the values themselves.

For the || operator, if the test is true, the || expression results in the value of the first operand (a or c). If the test is false, the || expression results in the value of the second operand (b).  
Inversely, for the && operator, if the test is true, the && expression results in the value of the second operand (b). If the test is false, the && expression results in the value of the first operand (a or c).

> I don't get when it's true and when it's false..

> a || b;  
> // roughly equivalent to:  
> a ? a : b;  
>  
> a && b;  
> // roughly equivalent to:  
> a ? b : a;  

An extremely common and helpful usage of this behavior, which there's a good chance you may have used before and not fully understood, is:

> function foo(a,b) {  
> 	a = a || "hello";  
> 	b = b || "world";  
>  
> 	console.log( a + " " + b );  
> }  
>   
> foo();					// "hello world"  
> foo( "yeah", "yeah!" );	// "yeah yeah!"  

The a = a || "hello" idiom (sometimes said to be JavaScript's version of the C# "null coalescing operator") acts to test a and if it has no value (or only an undesired falsy value), provides a backup default value ("hello").

What about &&?

The && operator "selects" the second operand if and only if the first operand tests as truthy, and this usage is sometimes called the "guard operator" -- the first expression test "guards" the second expression:

> function foo() {  
> 	console.log( a );  
> }  
> var a = 42;  
> a && foo(); // 42  

OK, so || and && have some neat tricks up their sleeve, as long as you're willing to allow the implicit coercion into the mix.

### Symbol Coercion

*Explicit coercion* of a symbol to a string is allowed, but *implicit coercion* of the same is disallowed and throws an error.

> var s1 = Symbol( "cool" );  
> String( s1 );					// "Symbol(cool)"  
>   
> var s2 = Symbol( "not cool" );  
> s2 + "";						// TypeError  

> het onderste is dus implicit want hij doet die + ""

Symbol values kunnen nooit *coercen* naar een number (geeft altijd error), maar gek genoeg kunnen ze allebei *explicitly* en *implicitly coercen* naar boolean (altijd true).

### Loose Equals vs. Strict Equals

Loose equals is the == operator, and strict equals is the === operator. Both operators are used for comparing two values for "equality," but the "loose" vs. "strict" indicates a very important difference in behavior between the two, specifically in how they decide "equality."

The correct description is: "== allows coercion in the equality comparison and === disallows coercion."

#### Equality Performance

If you're comparing two values of the same types, == and === use the identical algorithm, and so other than minor differences in engine implementation, they should do the same work. If you're comparing two values of different types, the performance isn't the important factor. What you should be asking yourself is: when comparing these two values, do I want coercion or not?    
If you want coercion, use == loose equality, but if you don't want coercion, use === strict equality.

#### Abstract Equality

Some minor exceptions to normal expectation to be aware of:

- NaN is never equal to itself   
- +0 and -0 are equal to each other 

##### Comparing: strings to numbers

To illustrate == coercion, let's first build off the string and number examples earlier in this chapter:

> var a = 42;  
> var b = "42";  
>  
> a === b;	// false  
> a == b;	// true  

But exactly what kind of coercion happens here? Does the a value of 42 become a string, or does the b value of "42" become a number?

In the ES5 spec, clauses 11.9.3.4-5 say:

> If Type(x) is Number and Type(y) is String, return the result of the comparison x == ToNumber(y).
> If Type(x) is String and Type(y) is Number, return the result of the comparison ToNumber(x) == y.

##### Comparing: anything to boolean

One of the biggest gotchas with the implicit coercion of == loose equality pops up when you try to compare a value directly to true or false.

> var a = "42";  
> var b = true;  
>  
> a == b;	// false  

Reason:  
> If Type(x) is Boolean, return the result of the comparison ToNumber(x) == y.
> If Type(y) is Boolean, return the result of the comparison x == ToNumber(y).

> Ze zetten de boolean in een nummer. Dus true wordt 1 en false wordt 0. Dus eigenlijk doen ze nu "42" == 1. En das dus false.

#### Comparing: nulls to undefineds

> If x is null and y is undefined, return true.  
> If x is undefined and y is null, return true.   

Null and undefined, when compared with == loose equality, equate to (aka coerce to) each other (as well as themselves, obviously), and no other values in the entire language.

What this means is that null and undefined can be treated as indistinguishable for comparison purposes, if you use the == loose equality operator to allow their mutual implicit coercion.

var a = null;
var b;

> a == b;	// true  
> a == null;	// true  
> b == null;	// true  
>    
> a == false;	// false  
> b == false;	// false  
> a == "";	// false  

alleen null en undefined zijn dus samen true

> var a = doSomething();  
>   
> if (a == null) {  
> 	// ..  
> }  

The a == null check will pass only if doSomething() returns either null or undefined, and will fail with any other value, even other falsy values like 0, false, and "".

##### Comparing: objects to non-objects
If an object/function/array is compared to a simple scalar primitive (string, number, or boolean), the ES5 spec says in clauses 11.9.3.8-9:

> If Type(x) is either String or Number and Type(y) is Object, return the result of the comparison x == ToPrimitive(y).
> If Type(x) is Object and Type(y) is either String or Number, return the result of the comparison ToPrimitive(x) == y.

> var a = 42;  
> var b = [ 42 ];  
>  
> a == b;// true  

The [ 42 ] value has its ToPrimitive abstract operation called (see the "Abstract Value Operations" section earlier), which results in the "42" value. From there, it's just 42 == "42", which as we've already covered becomes 42 == 42, so a and b are found to be coercively equal.

The __null__ and __undefined__ values cannot be boxed -- they have no object wrapper equivalent -- so Object(null) is just like Object() in that both just produce a normal object.

#### Edge Cases

Let's try to call out the worst, craziest corner cases so we can see what we need to avoid to not get bitten with coercion bugs.

##### A Number By Any Other Value Would...

> Number.prototype.valueOf = function() {  
> 	return 3;  
> };  
>  
> new Number( 2 ) == 3;	// true  

Evil, huh? Of course it is. No one should ever do such a thing. 

Next, let's consider another tricky example, which takes the evil from the previous example to another level:

> if (a == 2 && a == 3) {  
> 	// ..  
> }

You might think this would be impossible, because a could never be equal to both 2 and 3 *at the same time*. But "at the same time" is inaccurate, since the first expression a == 2 happens strictly before a == 3.

##### False-y Comparisons

The most common complaint against implicit coercion in == comparisons comes from how falsy values behave surprisingly when compared to each other.


> "0" == null;			// false  
> "0" == undefined;		// false  
> "0" == false;			// true -- UH OH!  
> "0" == NaN;				// false  
> "0" == 0;				// true  
> "0" == "";				// false  
>  
> false == null;			// false  
> false == undefined;		// false  
> false == NaN;			// false  
> false == 0;				// true -- UH OH!  
> false == "";			// true -- UH OH!  
> false == [];			// true -- UH OH!  
> false == {};			// false  
>  
> "" == null;				// false  
> "" == undefined;		// false   
> "" == NaN;				// false  
> "" == 0;				// true -- UH OH!  
> "" == [];				// true -- UH OH!  
> "" == {};				// false  
>  
> 0 == null;				// false  
> 0 == undefined;			// false  
> 0 == NaN;				// false  
> 0 == [];				// true -- UH OH!  
> 0 == {};				// false  

##### The Crazy Ones

We don't have to stop there, though. We can keep looking for even more troublesome coercions:

> [] == ![];		// true

What do we know about the ! unary operator? It explicitly coerces to a boolean using the ToBoolean rules (and it also flips the parity). So before [] == ![] is even processed, it's actually already translated to [] == false. We already saw that form in our above list (false == []), so its surprise result is not new to us.

> 2 == [2];		// true   
> "" == [null];	// true

You could rightly make the case that since String(null) becomes "null", then String([null]) should also become "null". That's a reasonable assertion. So, that's the real culprit.

> heeeel veel rare code dingetjes waar je bij denkt WHY

##### Sanity Check

We have a list of coercions that are totally sane and explainable.

> Denk nog ff aan die lijst van hiervoor..

Four of the seven items on this list involve == false comparison, which we said earlier you should always, always avoid. That's a pretty easy rule to remember.

Now the list is down to three.

> "" == 0;				// true -- UH OH!  
> "" == [];				// true -- UH OH!  
> 0 == [];				// true -- UH OH!  

##### Safely Using Implicit Coercion

hTe most important advice I can give you: examine your program and reason about what values can show up on either side of an == comparison. To effectively avoid issues with such comparisons, here's some heuristic rules to follow:

1. If either side of the comparison can have true or false values, don't ever, EVER use ==.
2. If either side of the comparison can have [], "", or 0 values, seriously consider not using ==.

##### Being more explicit/verbose in these cases will save you from a lot of headaches.

The question of == vs. === is really appropriately framed as: should you allow coercion for a comparison or not?

In the overall scheme of things, there's relatively few cases where implicit coercion is truly dangerous. But in those places, for safety sake, definitely use ===.

### Abstract Relational Comparison

While this part of implicit coercion often gets a lot less attention, it's important nonetheless to think about what happens with a < b comparisons).

> var a = [ 42 ];  
> var b = [ "43" ];  
>   
> a < b;	// true  
> b < a;	// false  

logisch tochh

> var a = [ "42" ];  
> var b = [ "043" ];  
>   
>  a < b;	// false  

a and b are not coerced to numbers, because both of them end up as strings after the ToPrimitive coercion on the two arrays. So, "42" is compared character by character to "043", starting with the first characters "4" and "0", respectively. Since "0" is lexicographically less than than "4", the comparison returns false.


## Chapter 5: Grammar

### Statements & Expressions

Statements are sentences, expressions are phrases, and operators are conjunctions/punctuation.

> var a = 3 * 6;  
> var b = a;  
> b;  

In this snippet, 3 * 6 is an expression (evaluates to the value 18). But a on the second line is also an expression, as is b on the third line. The a and b expressions both evaluate to the values stored in those variables at that moment, which also happens to be 18.

#### Statement Completion Values

Let's consider var b = a. What's the completion value of that statement?

The b = a assignment expression results in the value that was assigned (18 above), but the var statement itself results in undefined. Why? Because var statements are defined that way in the spec. If you put var a = 42; into your console, you'll see undefined reported back instead of 42.

> var b;  
>    
> if (true) {  
> 	b = 4 + 38;  
> }  

If you typed that into your console/REPL, you'd probably see 42 reported, since 42 is the completion value of the if block, which took on the completion value of its last assignment expression statement b = 4 + 38.

In other words, the completion value of a block is like an __implicit return__ of the last statement value in the block.

This kind of code doesn't work:

> var a, b;  
>   
> a = if (true) {  
> 	b = 4 + 38;  
> };  

We can't capture the completion value of a statement and assign it into another variable in any easy syntactic/grammatical way. So, what can we do?

There's a proposal for ES7 called "do expression." Here's how it might work:

> var a, b;  
>   
> a = do {  
> 	if (true) {  
> 		b = 4 + 38;  
> 	}  
> };
>  
> a;	// 42

#### Expression Side Effects

Most expressions don't have side effects. For example:

> var a = 2;  
> var b = a + 3;  

The expression a + 3 did not itself have a side effect, like for instance changing a. It had a result, which is 5, and that result was assigned to b in the statement b = a + 3.

The most common example of an expression with (possible) side effects is a function call expression:

> function foo() {  
> 	a = a + 1;  
> }
> 
> var a = 1;
> foo();		// result: `undefined`, side effect: changed `a`

-----

The expression a++ has two separate behaviors. First, it returns the current value of a, which is 42 (which then gets assigned to b). But next, it changes the value of a itself, incrementing it by one.

> var a = 42;  
> var b = a++;  
>  
> a;	// 43  
b;	// 42  

Many developers would mistakenly believe that b has value 43 just like a does. But the confusion comes from not fully considering the when of the side effects of the ++ operator.

There's an option, though: the , statement-series comma operator. This operator allows you to string together multiple standalone expression statements into a single statement:

> var a = 42, b;  
> b = ( a++, a );  
>   
> a;	// 43  
> b;	// 43  

Another example of a side-effecting operator is delete. As we showed in Chapter 2, delete is used to remove a property from an object or a slot from an array. But it's usually just called as a standalone statement:

> var obj = {  
> 	a: 42  
> };  
>    
> obj.a;			// 42  
> delete obj.a;	// true 
> obj.a;			// undefined 

#### Contextual Rules

There are quite a few places in the JavaScript grammar rules where the same syntax means different things depending on where/how it's used. This kind of thing can, in isolation, cause quite a bit of confusion.

##### { .. } Curly Braces

There's two main places that a pair of { .. } curly braces will show up in your code. Let's take a look at each of them.

__Object Literals__


> // assume there's a `bar()` function defined  
>   
> var a = {   
> 	foo: bar()  
> };  

How do we know this is an object literal? Because the { .. } pair is a value that's getting assigned to a.

__Labels__  

What happens if we remove the var a = part of the above snippet?

> // assume there's a `bar()` function defined  
>   
> {  
> 	foo: bar()   
> }  

A lot of developers assume that the { .. } pair is just a standalone object literal that doesn't get assigned anywhere. But it's actually entirely different.

Here, { .. } is just a regular code block. The { .. } code block here is functionally pretty much identical to the code block being attached to some statement, like a for/while loop, if conditional, etc.

##### Blocks
Another commonly cited JS gotcha (related to coercion -- see Chapter 4) is:

> [] + {}; // "[object Object]"  
> {} + []; // 0  

This seems to imply the + operator gives different results depending on whether the first operand is the [] or the {}. But that actually has nothing to do with it!

##### Object Destructuring
Another place that you'll see { .. } pairs showing up is with "destructuring assignments" , specifically object destructuring. Consider:

> function getData() {  
> 	// ..  
> 	return {  
> 		a: 42,  
>		b: "foo"  
>	};  
> }  

As you can probably tell, var { a , b } = .. is a form of ES6 destructuring assignment, which is roughly equivalent to:

> var res = getData();  
> var a = res.a;  
> var b = res.b;  
>  
> var { a, b } = getData();  
>  
> console.log( a, b ); // 42 "foo"  
 
#### else if And Optional Blocks

It's a common misconception that JavaScript has an else if clause, because you can do:

> if (a) {  
> 	// ..  
> }  
> else if (b) {  
> 	// ..  
> }  
> else {  
> 	// ..  
> }  

But there's a hidden characteristic of the JS grammar here: there is no else if. But if and else statements are allowed to omit the { } around their attached block if they only contain a single statement. 

### Operator Precedence

example from above:

> var a = 42, b;  
> b = ( a++, a );  
>  
> a;	// 43  
> b;	// 43  

But what would happen if we remove the ( )?

> var a = 42, b;  
> b = a++, a;  
>  
> a;	// 43  
> b;	// 42  

#### Short Circuited

For both && and || operators, the right-hand operand will not be evaluated if the left-hand operand is sufficient to determine the outcome of the operation. Hence, the name "short circuited".

For example, with a && b, b is not evaluated if a is falsy, because the result of the && operand is already certain, so there's no point in bothering to check b. Likewise, with a || b, if a is truthy, the result of the operand is already certain, so there's no reason to check b.

This short circuiting can be very helpful and is commonly used:

> function doSomething(opts) {  
> 	if (opts && opts.cool) {  
> 		// ..  
> 	}  
> }  

#### Tighter Binding

Does the ? : operator have more or less precedence than the && and || operators?

> a && b || c ? c || b ? a : c && b : a  

I that more like this:

> a && b || (c ? c || (b ? a : c) && b : a)

or this?

> (a && b || c) ? (c || b) ? a : (c && b) : a

The answer is the second one. But why?  
Because && is more precedent than ||, and || is more precedent than ? :.

#### Associativity

But what about multiple operators of the same precedence? Do they always process left-to-right or right-to-left?

It's important to note that associativity is not the same thing as left-to-right or right-to-left processing.

> var a = foo() && bar();

Here, foo() is evaluated first, and then possibly bar() depending on the result of the foo() expression. That definitely could result in different program behavior than if bar() was called before foo().

But this behavior is just left-to-right processing. It has nothing to do with the associativity of &&. In that example, since there's only one && and thus no relevant grouping here, associativity doesn't even come into play.

But that's not always the case. Some operators would behave very differently depending on left-associativity vs. right-associativity.

Consider the ? : ("ternary" or "conditional") operator:

> a ? b : c ? d : e;

__? :__ is right-associative, so which grouping represents how it will be processed?

> a ? b : (c ? d : e)

The right-associativity here actually matters, as (a ? b : c) ? d : e will behave differently for some (but not all!) combinations of values.

#### Disambiguation

We should mix both operator precedence/associativity and ( ) manual grouping into our programs -- I argue the same way in Chapter 4 for healthy/safe usage of implicit coercion, but certainly don't endorse it exclusively without bounds.

For example, if (a && b && c) .. is perfectly OK to me, and I wouldn't do if ((a && b) && c) .. just to explicitly call out the associativity, because I think it's overly verbose.

### Automatic Semicolons

ASI (Automatic Semicolon Insertion) is when JavaScript assumes a ; in certain places in your JS program even if you didn't put one there. Because if you omit even a single required ; your program would fail. Not very forgiving. ASI allows JS to be tolerant of certain places where ; aren't commonly thought to be necessary. But the semicolons are not inserted in the middle of a line.

Consider:
> var a = 42, b  
> c;

Should JS treat the c on the next line as part of the var statement? It certainly would if a , had come anywhere (even another line) between b and c. But since there isn't one, JS assumes instead that there's an implied ; (at the newline) after b. Thus, c; is left as a standalone expression statement.

#### Error Correction

Most, but not all, semicolons are optional, but the two ;s in the for ( .. ) .. loop header are required.

Let me just share my perspective. A strict reading of the spec implies that ASI is an "error correction" routine. What kind of error, you may ask? Specifically, a parser error. In other words, in an attempt to have the parser fail less, ASI lets it be more tolerant.

My take: __use semicolons wherever you know they are "required," and limit your assumptions about ASI to a minimum.__

### Errors

Not only does JavaScript have different subtypes of errors (TypeError, ReferenceError, SyntaxError, etc.), but also the grammar defines certain errors to be enforced at compile time, as compared to all other errors that happen during runtime.

One simple example is with syntax inside a regular expression literal. There's nothing wrong with the JS syntax here, but the invalid regex will throw an early error:

> var a = /+foo/;		// Error!

ES5's strict mode defines even more early errors. For example, in strict mode, function parameter names cannot be duplicated:

> function foo(a,b,a) { }					// just fine  
>  
> function bar(a,b,a) { "use strict"; }	// Error!  

#### Using Variables Too Early

ES6 defines a new concept called the __TDZ__ ("Temporal Dead Zone").

The TDZ refers to places in code where a variable reference cannot yet be made, because it hasn't reached its required initialization.

The most clear example of this is with ES6 let block-scoping:

> {  
> 	a = 2;		// ReferenceError!  
>	let a;  
> }  

The assignment a = 2 is accessing the a variable (which is indeed block-scoped to the { .. } block) before it's been initialized by the let a declaration, so it's in the TDZ for a and throws an error.

### Function Arguments

Another example of a TDZ violation can be seen with ES6 default parameter values:

> var b = 3;  
>   
> function foo( a = 42, b = a + b + 5 ) {  
> 	// ..  
> }

The b reference in the assignment would happen in the TDZ for the parameter b (not pull in the outer b reference), so it will throw an error. However, the a in the assignment is fine since by that time it's past the TDZ for parameter a.

#### try..finally

The code in the finally clause always runs (no matter what), and it always runs right after the try (and catch if present) finish, before any other code runs. In one sense, you can kind of think of the code in a finally clause as being in a callback function that will always be called regardless of how the rest of the block behaves.

So what happens if there's a return statement inside a try clause? It obviously will return a value, right? But does the calling code that receives that value run before or after the finally?

> function foo() {  
> 	try {  
> 		return 42;  
> 	}  
> 	finally {  
> 		console.log( "Hello" );  
> 	}  
>  
> 	console.log( "never runs" );  
> }  
>  
> console.log( foo() );  
> // Hello  
> // 42  

The return 42 runs right away, which sets up the completion value from the foo() call. This action completes the try clause and the finally clause immediately runs next. Only then is the foo() function complete, so that its completion value is returned back for the console.log(..) statement to use.


#### switch

Let's briefly explore the switch statement, a sort-of syntactic shorthand for an if..else if..else.. statement chain.

> switch (a) {  
> 	case 2:  
> 		// do something  
> 		break;  
> 	case 42:  
> 		// do another thing    
> 		break;  
> 	default:  
> 		// fallback to here  
> }  

As you can see, it evaluates a once, then matches the resulting value to each case expression (just simple value expressions here). If a match is found, execution will begin in that matched case, and will either go until a break is encountered or until the end of the switch block is found.
