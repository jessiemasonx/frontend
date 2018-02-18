
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
[chapone](# chapone)  
[Chapter 2: Values](# Chapter 2: Values)  
[Chapter 3: Natives](# Chapter 3: Natives)  


## chapone

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


