# Chapter 1: What is Scope?

__Scope__ is the set of rules that determines where and how a variable (identifier) can be looked-up.
This may be for the purposes of assigning to the variable, which is an LHS (left-hand-side) reference, or it may 
be for the purposes of retrieving its value, which is an RHS (right-hand-dise) reference.  

> scope is waar een variable wordt opgeslagen. Waar je ze kan vinden. Een set afspraken. (uit de les)

## Compiler Theory

The JavaScript engine performs many of the same steps, albeit in more sophisticated ways than we may commonly 
be aware, of any traditional language-compiler. In a traditional compiled-language process, a chunk of source code, 
your program, will undergo typically three steps before it is executed, roughly called "compilation":

__1. Tokenizing/Lexing:__  
This is breaking up a string of characters in to meaningful chuncks, called __tokens__.  
*Example: var a = 2; This would be broken up into the folling tokens: var, a, = and ;.*  
__2. Parsing:__  
Taking a stream (array) of tokens and turning it into a tree of nested elements which represent the grammatical 
structure of the program. This tree is called __"AST"__ (Abstract Syntax Tree).  
*Example: the tree for var a = 2; might start with a top-level node called VariableDeclaration, with a child 
node called Indentifier*  
__3. Code-Generation:__   
The process of taking an AST and turning it into executable code. This part varies greatly depending on the language,
the platform it's targeting, etc.  
*Example: There's a way to take our above described AST for var a = 2; and turn it into a set of machine instructions
to actually create a variable called a (including reserving memory, etc.), and then store a value into a.*


## Understanding Scope

De manier waarop we het leren over scope, is door het proces als een gesprek te beschouwen. Maar wie voert het gesprek?

### The Cast

Let's meet the cast of characters that interact to process the program var a = 2;, so we understand their conversations 
that we'll listen in on shortly:

1. Engine:  
responsible for start-to-finish compilation and execution of our JavaScript program.

2. Compiler:  
one of Engine's friends; handles all the dirty work of parsing and code-generation (see previous section).

3. Scope:  
another friend of Engine; collects and maintains a look-up list of all the declared identifiers (variables), and 
enforces a strict set of rules as to how these are accessible to currently executing code.

### Back & Forth

When you see the program *var a = 2;*, you most likely think of that as one statement. But that's not how our new 
friend __Engine__ sees it. 
In fact, __Engine__ sees two distinct statements, one which *Compiler* will handle during compilation, and one which 
Engine will handle during execution.

the program var a = 2;

Compiler will proceed as:

1. Encountering var a, Compiler asks Scope to see if a variable a already exists for that particular scope collection. 
If so, Compiler ignores this declaration and moves on. Otherwise, Compiler asks Scope to declare a new variable called 
a for that scope collection.

2. Compiler then produces code for Engine to later execute, to handle the a = 2 assignment. The code Engine runs will 
first ask Scope if there is a variable called a accessible in the current scope collection. If so, Engine uses that 
variable. If not, Engine looks elsewhere (see nested Scope section below).


> Er worden dus twee verschillende acties ondernomen voor een *variable assignment*: ten eerste declareert __Compiler__ een 
variabele (indien niet eerder gedeclareerd in de huidige scope) en ten tweede zoekt __Engine__ tijdens het uitvoeren
de variabele op in Scope en wijst deze toe, indien gevonden.

### Compiler Speak

The type of look-up Engine performs affects the outcome of the look-up.

In our case, it is said that Engine would be performing an __"LHS"__ look-up for the variable a. The other type of look-up is called 
__"RHS"__. I bet you can guess what the "L" and "R" mean. These terms stand for __"Left-hand Side"__ and __"Right-hand Side"__.

Side... of what? Of an __assignment operation.__  
An LHS look-up is done when a variable appears on the left-hand side of an assignment operation, and an RHS look-up is done when a
 variable appears on the right-hand side of an assignment operation.  
 An RHS look-up is indistinguishable, for our purposes, from simply a look-up of the value of some variable, whereas the LHS look-up 
 is trying to find the variable container itself, so that it can assign. In this way, RHS doesn't really mean "right-hand side of an 
 assignment" per se, it just, more accurately, means "not left-hand side".
 
 > console.log( a );  
 The reference to a is an RHS reference, because nothing is being assigned to a here. Instead, we're looking-up to retrieve the value 
 of a, so that the value can be passed to console.log(..).
 
 > a = 2;  
 The reference to a here is an LHS reference, because we don't actually care what the current value is, we simply want to find the variable 
 as a target for the = 2 assignment operation.


## Nested Scope

There's usually more than one Scope to consider.   
Just as a block or function is nested inside another block or function, scopes are nested inside other scopes. So, if a variable cannot be 
found in the immediate scope, Engine consults the next outer containing scope, continuing until found or until the outermost (aka, global)
scope has been reached.

> De regels voor het doorzoeken van geneste scope: de *Engine* start bij de momenteel actieve scope, zoekt naar de variabele daar, 
en als deze niet wordt gevonden, blijft deze één niveau omhoog gaan, enzovoort. Als de buitenste globale scope wordt bereikt, stopt de 
zoekopdracht, ongeacht of deze de variabele vindt of niet.

## Errors

It matters whether we call it LHS or RHS because these two types of look-ups behave differently in the circumstance where the variable 
has not yet been declared (is not found in any consulted Scope).

If an RHS look-up fails to ever find a variable, anywhere in the nested Scopes, this results in a ReferenceError being thrown by the Engine. 
It's important to note that the error is of the type __ReferenceError__.

By contrast, if the Engine is performing an LHS look-up and arrives at the top floor (global Scope) without finding it, and if the program 
is not running in "Strict Mode", then the global Scope will create a __new variable__ of that name __in the global scope__, 
and hand it back to __Engine__.

## REVIEW

> assigning to the variable, which is an LHS (left-hand-side) reference   
> retrieving its value, which is an RHS (right-hand-side) reference  

# Chapter 2: Lexical Scope 

There are two predominant models for how scope works.

1. __Lexical Scope__  
by far the most common, used by the vast majority of programming languages
2. __Dynamic Scope__  
still used by some languages

## Lex-time

The first traditional phase of a standard language compiler is called __lexing__ (aka, tokenizing). The lexing process examines a string of source code characters and assigns semantic meaning to the tokens as a result of some stateful parsing.

__Lexical scope__ is based on where variables and blocks of scope are authored, by you, at write time, and thus is (mostly) set in stone by the time the lexer processes your code.

There are three nested scopes inherent in this code example. It may be helpful to think about these scopes as bubbles inside of each other.

![code](https://github.com/getify/You-Dont-Know-JS/blob/master/scope%20%26%20closures/fig2.png)

__Bubble 1__ encompasses the global scope, and has just one identifier in it: foo.  
__Bubble 2__ encompasses the scope of foo, which includes the three identifiers: a, bar and b.  
__Bubble 3__ encompasses the scope of bar, and it includes just one identifier: c.  

### Look-ups

In the above code snippet, the Engine executes the console.log(..) statement and goes looking for the three referenced variables a, b, and c. It first starts with the innermost scope bubble, the scope of the bar(..) function. It won't find a there, so it goes up one level, out to the next nearest scope bubble, the scope of foo(..). It finds a there, and so it uses that a. Same thing for b. But c, it does find inside of bar(..).

__Scope look-up stops once it finds the first match.__

> window.a  
This technique gives access to a global variable which would otherwise be inaccessible due to it being shadowed. However, non-global shadowed variables cannot be accessed.

## Cheating Lexical

__cheating lexical scope leads to poorer performance.

### eval

The eval(..) function in JavaScript takes a string as an argument, and treats the contents of the string as if it had actually been authored code at that point in the program. In other words, you can programmatically generate code inside of your authored code, and run the generated code as if it had been there at author time.

> function foo(str, a) {  
> 	     eval( str ); // cheating!  
> 	     console.log( a, b );  
> }  
>  
> var b = 2;  
>  
> foo( "var b = 3;", 1 ); // 1 3  

The string "var b = 3;" is treated, at the point of the eval(..) call, as code that was there all along. Because that code happens to declare a new variable b, it modifies the existing lexical scope of foo(..). In fact, as mentioned above, this code actually creates variable b inside of foo(..) that shadows the b that was declared in the outer (global) scope.

> ????????

> can modify existing lexical scope at runtime by evaluating a string of "code" which has one or more declarations in it

### with

with is typically explained as a short-hand for making multiple property references against an object without repeating the object reference itself each time.

> // "easier" short-hand  
> with (obj) {  
> 	a = 3;  
> 	b = 4;  
> 	c = 5;  
> }  

> essentially creates a whole new lexical scope at runtime by treating an object reference as a "scope" and that object's properties as scoped identifiers.

### Performance

Both eval(..) and with cheat the otherwise author-time defined lexical scope by modifying or creating new lexical scope at runtime.

Aren't these good features? No.

Most of those optimizations it would make are pointless if eval(..) or with are present, so it simply doesn't perform the optimizations at all.  
Your code will almost certainly tend to run slower simply by the fact that you include an eval(..) or with anywhere in the code. No matter how smart the Engine may be about trying to limit the side-effects of these pessimistic assumptions, __there's no getting around the fact that without the optimizations, code runs slower.__

## Review (TL;DR)

Lexical scope means that scope is defined by author-time decisions of where functions are declared. The lexing phase of compilation is essentially able to know where and how all identifiers are declared, and thus predict how they will be looked-up during execution.

Two mechanisms in JavaScript can "cheat" lexical scope: eval(..) and with. The former can modify existing lexical scope (at runtime) by evaluating a string of "code" which has one or more declarations in it. The latter essentially creates a whole new lexical scope (again, at runtime) by treating an object reference as a "scope" and that object's properties as scoped identifiers.

The downside to these mechanisms is that it defeats the Engine's ability to perform compile-time optimizations regarding scope look-up, because the Engine has to assume pessimistically that such optimizations will be invalid. Code will run slower as a result of using either feature. Don't use them.

# Chapter 3: Function vs. Block Scope

Scope consists of a series of "bubbles" that each act as a container or bucket, in which identifiers (variables, functions) are declared. These bubbles nest neatly inside each other, and this nesting is defined at author-time.

Maar wat precies maakt die bubble? Alleen een functie of ook andere dingen?

## Scope From Functions

Javascript heeft function-based scope. Bij elke functie maakt hij z'n eigen bubble. 

	 function foo(a) {
	 	           var b = 2;
	 
	 	// some code
	 
	 	function bar() {
			// ...
	 	}
	  
	 	// more code
	  
	 	var c = 3;
	 }

Hier zit in de bubble van foo(..) de indentifiers a, b. c en bar. En bar heeft ook z'n eigen bubble. Als al die dingen zijn niet te bereiken buiten foo(). Dan krijg je een ReferenceError. Maar de dingen die in foo() zitten kan je wel bereiken in bar().

## Hiding In Plain Scope

De traditionele manier van het denken over een functie is dat je een functie declareert en dan de code erin zet/ Maar de tegenovergestelde manier is ook powerful en useful. Eerst de code dan die dingen er omheen. Daardoor "hide" je de code.

In other words, you can "hide" variables and functions by enclosing them in the scope of a function. The "Principle of Least Privilege" states that in the design of software, such as the API for a module/object, you should expose only what is minimally necessary, and "hide" everything else.

### Collision Avoidance

Another benefit of "hiding" variables and functions inside a scope is to avoid unintended collision between two different identifiers with the same name but different intended usages.

	> function foo() {  
	> 	function bar(a) {  
	> 		i = 3; // changing the `i` in the enclosing scope's for-loop  
	> 		console.log( a + i );  
	> 	}
	>   
	> for (var i=0; i<10; i++) {  
	> 	bar( i * 2 ); // oops, infinite loop ahead!  
	> }  
	> }  
	>  
	> foo();  

The i = 3 assignment inside of bar(..) overwrites, unexpectedly, the i that was declared in foo(..) at the for-loop. In this case, it will result in an infinite loop, because i is set to a fixed value of 3 and that will forever remain < 10.

#### Global "Namespaces"

A particularly strong example of (likely) variable collision occurs in the global scope. 

Such libraries typically will create a single variable declaration, often an object, with a sufficiently unique name, in the global scope. This object is then used as a "namespace" for that library, where all specific exposures of functionality are made as properties of that object (namespace), rather than as top-level lexically scoped identifiers themselves.

For example:

	> var MyReallyCoolLibrary = {  
	> 	awesome: "stuff",  
	> 	doSomething: function() {  
	> 		// ...  
	> 	},  
	> 	doAnotherThing: function() {  
	> 		// ...  
	> 	}  
	> };  

#### Module Management

Another option for collision avoidance is the more modern "module" approach, using any of various dependency managers. Using these tools, no libraries ever add any identifiers to the global scope, but are instead required to have their identifier(s) be explicitly imported into another specific scope through usage of the dependency manager's various mechanisms.

## Functions As Scopes

We've seen that we can take any snippet of code and wrap a function around it, and that effectively "hides" any enclosed variable or function declarations from the outside scope inside that function's inner scope. While this technique "works", it is not necessarily very ideal. There are a few problems it introduces.  
The first is that we have to declare a named-function foo(), which means that the identifier name foo itself "pollutes" the enclosing scope (global, in this case). We also have to explicitly call the function by name (foo()) so that the wrapped code actually executes.

It would be more ideal if the function didn't need a name (or, rather, the name didn't pollute the enclosing scope), and if the function could automatically be executed.

Fortunately, JavaScript offers a solution to both problems.

	> var a = 2;  
	>   
	> (function foo(){ // <-- insert this  
	>   
	> 	var a = 3; 
	> 	console.log( a ); // 3 
	>  
	> })(); // <-- and this  
	>  
	> console.log( a ); // 2  

Notice that the wrapping function statement starts with (function... as opposed to just function... This is actually a major change. Instead of treating the function as a standard declaration, the function is treated as a function-expression.

The key difference we can observe here between a function declaration and a function expression relates to where its name is bound as an identifier.

### Anonymous vs. Named

function() is een  "anonymous function expression", because function()... has no name identifier on it. 

Anonymous function expressions are quick and easy to type, and many libraries and tools tend to encourage this idiomatic style of code. However, they have several draw-backs to consider:

1. Anonymous functions have no useful name to display in stack traces, which can make debugging more difficult.

2. Without a name, if the function needs to refer to itself, for recursion, etc., the deprecated arguments.callee reference is unfortunately required. Another example of needing to self-reference is when an event handler function wants to unbind itself after it fires.

3. Anonymous functions omit a name that is often helpful in providing more readable/understandable code. A descriptive name helps self-document the code in question.

The best practice is to always name your function expressions:

> setTimeout( function timeoutHandler(){ // <-- Look, I have a name!

### Invoking Function Expressions Immediately

Now that we have a function as an expression by virtue of wrapping it in a ( ) pair, we can execute that function by adding another () on the end, like (function foo(){ .. })(). The first enclosing ( ) pair makes the function an expression, and the second () executes the function.

	> (function foo(){  
	>  
	>	var a = 3;  
	>	console.log( a ); // 3  
	>  
	> })();  

A few years ago the community agreed on a term for it: __IIFE__, which stands for __Immediately Invoked Function Expression__.

## Blocks As Scopes

	> for (var i=0; i<10; i++) {  
	> 	console.log( i );  
	> }  

We declare the variable i directly inside the for-loop head, most likely because our intent is to use i only within the context of that for-loop, and essentially ignore the fact that the variable actually scopes itself to the enclosing scope (function or global).

That's what block-scoping is all about. Declaring variables as close as possible, as local as possible, to where they will be used. 

### with

 It's an example of (a form of) block scope, in that the scope that is created from the object only exists for the lifetime of that with statement, and not in the enclosing scope.
 
 ### try/catch
 
 It's a very little known fact that JavaScript in ES3 specified the variable declaration in the catch clause of a try/catch to be block-scoped to the catch block.
 
 > ??
 
 ### let
 
  ES6 introduces a new keyword __let__ which sits alongside var as another way to declare variables.  
The *let* keyword attaches the variable declaration to the scope of whatever block (commonly a { .. } pair) it's contained in. In other words, *let* implicitly hijacks any block's scope for its variable declaration.

	> if (foo) {  
	> 	let bar = foo * 2;  
	> 	bar = something( bar );  
	> 	console.log( bar );  
	> }  

Using __let__ to attach a variable to an existing block is somewhat implicit. Usually, explicit code is preferable over implicit or subtle code.

### Garbage Collection

Another reason block-scoping is useful relates to closures and garbage collection to reclaim memory.

Declaring explicit blocks for variables to locally bind to is a powerful tool that you can add to your code toolbox.

### let Loops

	> for (let i=0; i<10; i++) {  
	>	console.log( i );  
	> }  
		>  
>  console.log( i ); // ReferenceError  

Not only does let in the for-loop header bind the i to the for-loop body, but in fact, it re-binds it to each iteration of the loop, making sure to re-assign it the value from the end of the previous loop iteration.

### const

n addition to let, ES6 introduces __const__, which also creates a block-scoped variable, but whose value is fixed (constant). Any attempt to change that value at a later time results in an error.

## Review (TL;DR)

Functions are the most common unit of scope in JavaScript. Variables and functions that are declared inside another function are essentially "hidden" from any of the enclosing "scopes", which is an intentional design principle of good software.

But functions are by no means the only unit of scope. Block-scope refers to the idea that variables and functions can belong to an arbitrary block (generally, any { .. } pair) of code, rather than only to the enclosing function.

Starting with ES3, the try/catch structure has block-scope in the catch clause.

In ES6, the let keyword (a cousin to the var keyword) is introduced to allow declarations of variables in any arbitrary block of code. if (..) { let a = 2; } will declare a variable a that essentially hijacks the scope of the if's { .. } block and attaches itself there.

Though some seem to believe so, block scope should not be taken as an outright replacement of var function scope. Both functionalities co-exist, and developers can and should use both function-scope and block-scope techniques where respectively appropriate to produce better, more readable/maintainable code.

## Chapter 4: Hoisting

__any variable declared within a scope is attached to that scope.__

### Chicken Or The Egg?

	 a = 2;  
	   
	 var a;  
	   
	 console.log( a );  
	
Mensen zouden denken dat console.log undefined zou geven omdat de var a statement na de a = 2 komt. Maar de output is gewoon 2. 

	console.log( a );

	var a = 2;
	
Maaar bij dit stukje geeft ie undefined.  

### The Compiler Strikes Again

Recall that the Engine actually will compile your JavaScript code before it interprets it. 
 
So, the best way to think about things is that all declarations, both variables and functions, are processed first, before any part of your code is executed.

When you see __var a = 2;__, you probably think of that as one statement. But JavaScript actually thinks of it as two statements: *var a;* and *a = 2;*. The first statement, the __declaration__, is processed during the __compilation__ phase. The second statement, __the assignment__, is left in place for the __execution__ phase.

	var a;
	a = 2;

	console.log( a );
	
Eerste deel is compilation en 2e deel is execution.

Variable and function declarations are "moved" from where they appear in the flow of the code to the top of the code. This gives rise to the name __"Hoisting"__.

In other words, the egg (declaration) comes before the chicken (assignment).

__hoisting is per-scope__  
Als je var a in een functie hebt gaat ie bovenaan die functie dus die scope.

	function foo() {
		var a;
	
		console.log( a ); // undefined
	
		a = 2;
	}
	
	foo();
	
Function declarations are hoisted, as we just saw. But function expressions are not.

	foo(); // not ReferenceError, but TypeError!  
	
	var foo = function bar() {
		// ...
	};

foo has no value yet (as it would if it had been a true function declaration instead of expression). So, foo() is attempting to invoke the undefined value, which is a TypeError illegal operation.

## Functions First

Both function declarations and variable declarations are hoisted. But a subtle detail (that can show up in code with multiple "duplicate" declarations) is that functions are hoisted first, and then variables.

	foo(); // 1
	
	var foo;
	
	function foo() {
		console.log( 1 );
	}
	
	foo = function() {
		console.log( 2 );
	};
1 is printed instead of 2!

De volgorde wordt nu zo geprint door de *engine*:

	function foo() {
		console.log( 1 );
	}
	
	foo(); // 1
	
	foo = function() {
		console.log( 2 );
	};
	
## Review 

We can be tempted to look at var a = 2; as one statement, but the JavaScript Engine does not see it that way. It sees var a and a = 2 as two separate statements, the first one a compiler-phase task, and the second one an execution-phase task.

What this leads to is that all declarations in a scope, regardless of where they appear, are processed first before the code itself is executed. You can visualize this as declarations (variables and functions) being "moved" to the top of their respective scopes, which we call "hoisting".

Declarations themselves are hoisted, but assignments, even assignments of function expressions, are not hoisted.

Be careful about duplicate declarations, especially mixed between normal var declarations and function declarations -- peril awaits if you do!
