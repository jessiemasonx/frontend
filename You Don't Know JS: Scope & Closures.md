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





