---
layout: default
title: Currying
parent: Intro to JavaScript
nav_order: 5
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

# Currying
Functions aren't limited to being arguments in other functions; they can also be outputs. One of the most important ways that returned functions can be used is through 'curring.'

Currying works by'binding' arguments to a function before passing the function somewhere else. For instance, let's imagine we want to pass `map` a `multiply` function, but want the answer to always be multiplied by some other number. We could define a a new function `multiplyBy`:

```js
function multiplyBy(a) {
    return function mult(b) {
        return (a * b);
    };
};
```

Then, when we pass a function into `.map()`, we can call `multiplyBy` with the value we want to multiply by; then, when `.map()` calls the function, `multiplyBy` will remember the value we originally provided it and multiply the arguments by this value.

```js
const array = [1, 2, 3, 4, 5];
const multArray = array.map(multiplyBy(5))

console.log(multArray); // [5, 10, 15, 20, 25]
```

Just like functions can be defined multiple ways, curried functions can be defined in several ways through the combination of function definition methods:

```js
const divideBy = (a) => (b) => {
    return b / a;
}

function nthPowerOf (a) {
    return (b) => b ** a;
}

function nthRootOf (a) {
    return function (b) {
        return b ** (1 / a);
    }
}
```
