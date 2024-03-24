---
layout: default
title: Anonymous Functions
parent: Intro to JavaScript
nav_order: 3
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# Anonymous Functions
Most of the time, we want our functions named and usable in multiple instances. But that isn't always the case.

## Functions as Arguments

Functions can be defined using the `function` keyworld, and a name, but sometimes we don't want to have to define them before we use them. When that is the case, we use what are called 'anonymous functions.' These functions are especially important as arguments that can be passed to other functions. One way we can define an anonymous function is by simply doing `function (<args>) {<operation>}`. 

```js
const anonymous = function (a) {return a * a;};
```

However, this is quite verbose, so JavaScript gives us a second way of defining anonymous function. If you think back to the section about function definitions, you'll remember that there are two ways to define functions:

```js
function add(a, b) {
    return a + b;
}
const subtract = (a, b) => {
    return a - b;
}
```

The second way is actually an anonymous function which is being assigned to the variable `subtract`. Anonymous functions are concisely defined using the `() =>` syntax. Inside the `()` are any arguments which the function uses, and on the other side of the `=>` are the actions taken by the function. 

JavaScript allows functions to be passed as arguments into functions; one example could be in the following function, where the input `func` is applied to the input `arg`.

```js
function applyFunc(func, arg1, arg2) {
    return func(arg1, arg2);
}
```

We could provide `applyFunc` with a function that has been defined earlier in the code, like this:

```js
const output = applyFunc(subtract, 19, 20);
console.log(output); // => -1
```

But we don't always want our functions to be seperated from the code that is running them. In those cases, we can use an anonymous function declaration to declare it immediately in the arguments of the function call. Because anonymous functions do not need to be bound to a variable, they can be defined on the spot.

```js
const newOutput = applyFunc((a, b) => {return a * b;}, 19, 20);
console.log(newOutput); // => 380 
```

Anonymous functions can use `{}`, but `{}` are primarily used to collect together functions that need to span multiple lines. Most of the time, our anonymous functions do not need to be longer than one line. In those cases, we can write them without the `{}`, and also do not need to use a `;` at the end of the line. When we write anonymous functions like this, we can also leave out the `return` statement, and JavaScript will automatically return the one line's output as the function's return.

```js
const longWay = (a, b) => {return a * b;};
const shortWay = (a, b) => a * b;

const shortApply = applyFunc((a, b) => a ** b, 2, 5);
console.log(shortApply); // => 32
```

In the next page on callback methods, you'll see more of how these anonymous functions may be useful.
