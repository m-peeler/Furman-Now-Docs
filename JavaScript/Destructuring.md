---
layout: default
title: Destructuring
parent: Intro to JavaScript
nav_order: 2
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

# Destructuring

Object decomposition is one of the most powerful recent features of JavaScript, and is used extensively throughout the Furman Now! codebase. 

## Basic Idea

When working with objects and arrays, we often want to pull a specific entry out of the structure and use its value somewhere else in our code. We could do this by saying `<array>[<index>]` or `<object>.<key>`, but that can become tedious and repetative. Similarly, we could assign these values to variables doing something like `const val = <object>.<key>`, but we would have to repeat this for every value we want to take out of the object. Destructuring allows us to pull out and assign many values at once from the same object. 

## Syntax

Destructuring is done through normal asssignment operations, with the object or array being destructured on the right, and syntax to indicate how the object should be destructured on the left. 

### Arrays
For an array, we wrap the left side's assignment name in `[]`, then specify the variable name we would like for each index; if we want index `0` to become the variable `a`, we would make the assignment side `[a]`. Arrays are destructured in order, so that the first name on the left is assigned to the value of the first entry in the array, and the second name to the second entry, and so on.

```js
const myArr = ['alice', 'bob', 'charlie', 'david']
const [first, second, third, fourth] = myArr;

console.log(first, second, third, fourth); // => 'alice bob charlie david'
```

Elements in the array can go unassigned, either by using fewer names (if, say, the last few entries are unneeded), or by writing commas in the destructuring assignment without a name in between.

```js
const [a, b, , d] = myArr;
console.log(a, b, d); // => 'alice bob david'
```
One possible usecase is when a function returns an array as output; destructuring allows us to take the output and assign its various parts to the variables desired. Another is to swap variable values.

```js
function example() {
    return [1, 2, 3];
}

const [a, b, c] = example();
console.log(a, b, c); // => '1 2 3'

let x = 12;
let y = 18;
[y, x] = [x, y];
```

Destructuring assignments can have default values, which are used if the part being destructured is non-existant or undefined.

```js
const [a = 12, b = 19, c = 20] = [null, undefined];
console.log(a, b, c) // null 19 20
```

If you want to save the remaining values of an array into a subset array, we "pack" them into a variable using the `...` assignment. Canonically, this is typically done into variables named `rest`.

```js
const [first, ...rest] = myArr;

console.log(first); // => 'alice'
console.log(rest); // => "['bob', 'charlie', 'david']"
```

Arrays can be 'unpacked' using the same `...` operator; this can be used to turn an array into a series of function inputs, such as with `console.log`.

```js
console.log(rest); // => "['bob', 'charlie', 'david']"
console.log(...rest); // => 'bob charlie david'

function add(a, b) {
    return a + b;
}
const nums = [18, 27];
const sum = add(...nums);
console.log(sum) // => 45
```

### Objects
For objects, we destructure by wrapping assignment names in `{}`, then specify the key we would like to pull out. Since objects have defined keys, destructuring allows for selection of any specific values using those keys, without having to leave empty spaces like with arrays. Instead, we automatically bind them to the variable of their key name.

```js
const myObj = {a: 'alice', b: 'bob', c: 'charlie', d: 'david'};
const {d} = myObj;
console.log(d) // => 'david'
```

We don't always want to use the object's key as the variable; we can thus re-bind the names using a `:`.

```js
const {c: person} = myObj;
console.log(person); // => 'charlie'
```

Object destructuring can also have default values, and can also pack unused values using `...`.

```js
const {z: user = 'zim'} = myObj;
const {a, ...rest} = myObj;

console.log(z) // => 'zim'
console.log(a) // => 'alice'
console.log(rest) // => {b: 'bob', c: 'charlier', d: 'david'}
```

## Complex Destructuring
Destructuring assignments can be chained together for complexer objects and arrays; this often comes into use with JSON parsing or passing objects between function. We do this by adding in more destructuring values to the left side. When we chain together destructuring values, *only the deepest level of assignment have the variable names bound to their value.* In the below example, `a` and `b` are *not defined* as variables; only `x`, `y`, and `z` are. Similarly, `chamber` is bound (to `'house'`) but `leader` is not bound since `head` takes the assignment (to `'speaker of the house'`).

```js
const complex = { a: { b: [1, 2, 3] } };
const {a: {b: [x, y, z]}} = complex;

const congress = [
  {chamber: 'house', leader: 'speaker of the house'},
  {chamber: 'senate', leader: 'president pro tempore'}
]
const [{chamber, leader : head}] = congress;
// leader  
```

This can be chained into as many levels as you want. It is especially useful in iterators, which will be discussed later.
