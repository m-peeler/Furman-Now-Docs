---
layout: default
title: Destructuring
parent: Intro to JavaScript
nav_order: 2
---

# Destructuring

Object decomposition is one of the most powerful recent features of JavaScript, and is used extensively throughout the Furman Now! codebase. 

## Basic Idea

When working with objects and arrays, we often want to pull a specific entry out of the structure and use its value somewhere else in our code. We could do this by saying `<array>[<index>]` or `<object>.<key>`, but that can become tedious and repetative. Similarly, we could assign these values to variables doing something like `const val = <object>.<key>`, but we would have to repeat this for every value we want to take out of the object. Destructuring allows us to pull out and assign many values at once from the same object. Destructuring is done through normal asssignment operations, with the object or array being destructured on the right, and syntax to indicate how the object should be destructured on the left.

```js

```
