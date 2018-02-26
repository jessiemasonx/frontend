
# Chapter 3: Into YDKJS

> scope is waar een variable wordt opgeslagen. Waar je ze kan vinden. Een set afspraken. (uit de les)

## Scope & Closures

De JS-engine verzamelt je code vlak voor (en soms tijdens!) De uitvoering. The typical metaphor for JS variable scope management, __"Hoisting."__

Closure is perhaps the single most important concept in all of JS, but if you haven't first grasped firmly how scope works, closure will likely remain beyond your grasp. One important application of closure is the __module pattern__. The module pattern is perhaps the most prevalent code organization pattern in all of JavaScript; deep understanding of it should be one of your highest priorities.

## this & Object Prototypes

> __this__ keyword refereert niet naar de functie waar hij in zit!! 

De This keyword wordt dynamisch gebonden op basis van hoe de functie in kwestie wordt uitgevoerd.

## Types & Grammar

Is coercion really so confusing, so bad, so treacherous, that your code is doomed from the start if you use it? I say no.

But I'm not merely suggesting that coercion is sensible and learnable, I'm asserting that coercion is an incredibly useful and totally underestimated tool that you should be using in your code. I'm saying that coercion, when used properly, not only works, but makes your code better.

## Async & Performance

We identify two major deficiencies of callbacks-only coding: *Inversion of Control (IoC) trust loss* and *lack of linear reason-ability.*

To address these two major deficiencies, ES6 introduces two new mechanisms (and indeed, patterns): __promises__ and __generators__.

__Promises__ are a time-independent wrapper around a "future value," which lets you reason about and compose them regardless of if the value is ready or not yet. Moreover, they effectively solve the IoC trust issues by routing callbacks through a trustable and composable promise mechanism.

__Generators__ introduce a new mode of execution for JS functions, whereby the generator can be paused at yield points and be resumed asynchronously later. The pause-and-resume capability enables synchronous, sequential looking code in the generator to be processed asynchronously behind the scenes. By doing so, we address the non-linear, non-local-jump confusions of callbacks and thereby make our asynchronous code sync-looking so as to be more reason-able.

But it's the combination of promises and generators that "yields" our most effective asynchronous coding pattern to date in JavaScript.

## ES6 & Beyond

JavaScript is never going to stop evolving, and moreover, the rate of evolution is increasing rapidly. 

Since ES6 is nearly complete at the time of this writing, ES6 & Beyond starts by dividing up the concrete stuff from the ES6 landscape into several key categories, including new syntax, new data structures (collections), and new processing capabilities and APIs.
