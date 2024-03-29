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

TypeScript uses the same syntax as JavaScript, with the addition of "type annotation" requirements, where you specify what type a variable is allowed to be. This is usually done by following a variable name with a colon and the type. The most basic type in TypeScript is `any`; TypeScript will effectively forgo any type checking on `any` variables and allow any oprations to be carried out on it. 

```ts
let value : any = 124;
```

In addition to `any`, the basic types are `number`, `string` and `boolean`. JavaScript has some strangeness with types, compared to other langauges, primarily with how it handles numeric data: there is no seperate `float` and `integer` type, so all numbers are simply of type `number`. The TypeScript compiler is able to use these type hints to let you know when the arguments you've provided do not match the type they should, and warn you about potentially unhandled values.

```ts
const var : number = 15;
const ltr : string = 'hello world';
const bol : boolean = true;

function multiply(a: number, b: number) : number {
    return a * b;
}
```

For non-`any` types, TypeScript will show an error if you try to reassign a variable to a value that does not match its type.

```ts
let value : number = 124;
value = 'hello world';
// TypeScript will object and tell you a string cannot be assigned to a number

let anything : any = 136;
anything = 'goodnight moon`;
// TypeScript has no issues with this

```

If a variable is allowed to be multiple types, you indicate this using the `|` (the 'or') operator. 

```ts
let cond : number | boolean = 24;
cond = true; // Ok with TS
cond = 'false'; // Not ok with TS
```

TypeScript's compiler won't let you leave variables `undefined` or `null` unless you specifically mark that they are allowed to be undefined. This can be done by adding `| undefined` or `| null` to the type annotation. For function argument and classes, there are often fields that you would want to leave optional, but this syntax can get verbose; TypeScript thus gives us the option of using the `?` symbol at the end of the variable name (in function arguments or for class variable definititions) as a way of concisely indicating that it may be `undefined`.

```ts
let val : number | undefined;

class Animal {
    name: string;
    legs: number;
    tailLength?: number;
    constructor (name: string, legs: number, tailLength?: number) {
        this.name = name;
        this.legs = legs;
        this.tailLength = tailLength;
    }
}

const human = new Animal('human', 2);
```

Arrays and objects are also annotated. Arrays are indicated by placing `[]` at the end of the type allowed in the array;
