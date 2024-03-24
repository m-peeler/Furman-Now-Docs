---
layout: default
title: Syntax
parent: Intro to JavaScript
nav_order: 1
---

# Basic Syntax

JavaScript is relatively straightforward in its synatx, much of which is taken from Java. 

## Variables

Variables are defined in one of two ways - either using the keyword `const` or the keyword `let`, followed by the variable name and an equal sign. These fulfil similar but distinct roles; `const` variables cannot be rebound after declaration, while `let` variables can (keep in mind that this does not stop you from changing properties inside a class of a `const` declaration, just the object itself). To keep you variables constant, use const unless you have to have the capability to change a value. The `var` declaration also exists, but I avoid using it and recommend similarly.  Lines almost always should end in semicolons (I recommend installing a linter like ESLint, which should be good about telling you when the semi-colons are unnecessary, and will have the added ability of enforcing good code styles on you. I use the AirBnb style).

```js
let x = 14;
// This is ok
x = x / 7;

const y = 14;
// This is not ok
y = y / 7;

```

## Functions

Functions can be declared in two ways: one is using the `function` keyword, and the other is with the `=>` notation. Regardless of the syntax used, they can be called in the same way. Functions are very powerful in JavaScript and more time will be spent on them later.

```js
function add(x, y) {
  return x + y;
}

const subtract = (x, y) => {
  return x - y;
}

add(10, 12);
// 22

subtract(18, 6);
// 12
```

## Data Structures

The two basic data structures of JavaScript are arrays and objects, which are more or less equivalent to Python lists and dictionaries, or Java arrays and hashmaps. Arrays are linear, defined using `[]`, and can be accessed by position index using a `[<index>]` syntax; objects are key-value pairs, defined using `{}`, and indexed into using strings in a `['<key>']` syntax. 

Object keys are always strings, so they are defined without using quotations, and can accessed without using quotations using the `.<key>` syntax. We tend to only use the `['<key>']` syntax when we need to access a dynamic position in the object, but we rarely do this; objects are typically treated like structs and classes, where their entries are assumed to be static. 

```js
const myArr = ['a', 'b', 'c'];
const myObj = {a: 'hello', b: 'world'};

console.log(myArr[2]); // => 'c'
console.log(myObj['a']); // => 'hello'
console.log(myObj.b); // => 'world'

```

Arrays can have objects, and objects can have arrays, which allows for the creation of complex structures. These also directly correspond to the structures of JSON files, which are a main way that information is shared between JavaScript and other web-based services. 


Objects can be turned into key-value pairs using the `Object.entries` function, or into just keys or just values using `Object.keys` and `Object.values`. They can also be created from an array of key-value pairs using `Object.fromEntries`.

```js
const keys = Object.keys(myObj); // => ['a']
const vals = Object.values(myObj); // => ['hello']

const pairs = [['first', 1], ['second', 2], ['third', 3]]
const pairsObj = Object.fromEntries(pairs)
```

Combined with destructuring and iteration, which will be discussed more later, objects and arrays are incredibly powerful tools.

## Classes

JavaScript has the same object-oriented capabilities as Java, though it uses the `constructor` method to define initiation, rather than using the class' name (like in Java) or some variant of `init` (e.g. Python). Default values can be provided in any function definition using a single-equals assignment operation. Functions are indicated with the keyword `function`, instance variables and methods are prefaced `this` inside the object, and static properties and methods are defined using the keyword `static`.

```js
class Vehicle {
    constructor (make, model, wheels=4) {
        this.make = make;
        this.model = model;
        this.wheels = wheels;
    }

    function toString() {
        return `The ${this.make} ${this.model} has ${this.wheels} wheels.`;
    }

    static function goVroom() {
        return 'Vroom!';
    }
}
```

Instances are instantiated using the `new` keyword, the class name, and any arguments necessary for the constructor. Static methods are accessed by calling `<class>.<method>`, while instance methods are called using `<instance>.<method>`.

```js
const truck = new Vehicle('Ford', 'F150);
console.log(Vehicle.goVroom()) // 'Vroom!'
console.log(truck.toString()) // 'The Ford F150 has 4 wheels'

const cycle = new Vehicle('Harley-Davidson', 'Street Glide', 2)
console.log(cycle.toString()) // 'The Harley-Davidson Street Glide has 2 wheels.
```

## Strings

String literals can be surrounded in either `'single quotes'` or `"double quotes"`; template strings are surrounded in `backticks` and are called 'templates' because you can place dynamic content inside of them, within a `${}` structure, such as `${x}`. This can be variables, but can also be more complex content, like equations or function calls. Strings can be printed to the console using `console.log()` for debugging purposes, or used in various other ways.

```js
const x = 14;
const y = 12;
const template = `${x} ${y / 2}` 

console.log(template)
// Prints out "14 7"
```

## Comparisons

JavaScript is built for the web; because of this, it does its best not to crash, and to do what it thinks you want. Because of this, it is built around a concept of 'truthiness': it wants things to mostly match, unless you require them to perfectly match. The `==` operator, and the class of related operators (like `!=`, `<=`, `>=`) use this truthiness, wherease the `===` operator and its relatives (like `!==`, `<==`, `>==`) use strict equality. JavaScript also has two  values of 'null' or 'none': one is `undefined`, and is intended for things that are either not yet declared, or have not yet been initialized. The second is `null`, and is intended as an empty return type. I highly recommend using only `===` so behavior is more predictable, because some truthy rules can be counterintuitive.

```js
let x;
// x is equal to undefined
const y = null;
// y is equal to null;

console.log(x == y) // true; undefined and null are 'truthily' the same
console.log(x === y) // false; undefined and null are not strictly the same
console.log(2 == '2') // true; the string '2' and the number 2 are truthily the same
console.log(2 === '2') // false; the string '2' and the number 2 are not strictly the same
console.log(2 === 2) // true; the number 2 strictly equals the number 2.
console.log('false' == true) // true; the string 'false' exists, so it is truthly equal to the value true
console.log('0' == false) // true; the string '0' is truthily equal to the number 0 which is truthily equal to false
```

## If-Else and Ternary

Like in most languages, if-statements let control flow be changed on the basis of conditions. JavaScript also has 'ternary operators,' which allow if-statements to be compressed into single-line expressions for briefer uses; these can often be useful in template strings or when switching between binary state. Ternaries use a `?` to indicate the end of the conditional and a `:` to seperate the `if` action from the `else` action.

```js
if (x === 2) {
    return 12;
} else if (x > 2) {
    return 11;
} else {
    return 13;
}
const cond = true;

const val = cond ? 12 : 13;
// Cond is conditional; if true, 12, else, 13
```
