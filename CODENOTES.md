## Antwoord op Nina's vragen 
__IIFE__ Is een functie die zichzelf gelijk invoked. Dan hoef je 'm niet aan te roepen. Hij roept zichzelf gelijk aan. (function(). 



# aantekeningen les 1
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

