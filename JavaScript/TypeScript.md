---
layout: default
title: TypeScript
parent: Intro to JavaScript
nav_order: 6
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# TypeScript

JavaScript is a dynamically-typed language; that means typing doesn't matter. However, many times it can be helpful to have the guidance of typing in the language. Because of that, the language of TypeScript was created; at runtime it is compiled to JavaScript, and can be called normally from JavaScript functions. When writing methods that are pure JavaScript, like data structures, the Furman Now! codebase will sometimes use TypeScript to provide some of these security measures. 

TypeScript uses the same syntax as JavaScript, with the addition of "type hinting" capabilities, where you specify what type a variable is allowed to be. This is usually done by following a variable name with a colon and the type. JavaScript has some strangeness with types, compared to other langauges, primarily with how it handles numeric data: there is no seperate `float` and `integer` type, so all numbers are simply of type `number`.

The TypeScript compiler is able to use these type hints to let you know when the arguments you've provided do not match the type they should, and warn you about potentially unhandled values.

```ts
const var : number = 15;
const ltr : string = 'hello world';

function multiply(a: number, b: number) : number {
    return a * b;
}
```
