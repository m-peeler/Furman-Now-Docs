---
layout: default
title: Hooks
parent: Intro to React Native
nav_order: 1
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

# React Hooks

## Basics of Hooks

Components, as we have discussed them so far, are not able to share information between each function call, or 'render.' Without the ability to share this information, we would be unable to know how many times a button has been pressed, or where a moving object was last located, or how long something has been occuring. Thus, React and React Native use something called hooks to allow the sharing of this information, which is typically called 'state'.

React Native has 6 basic types of hooks, which other hooks are build using. Furman Now!'s codebase uses 3 of these hooks, which will be discussed here.

All hooks are, by convention, begun with the word `use`; any time a function begins with the word `use`, it indicates that it is a hook, and any time a custom hook is created, it should be named following the `use` naming scheme.

Hooks can only be called in two spaces. First, within a component; second, by another hook. 

## useState

The most basic hook is the `useState` hook. `useState` allows you to store a specific state across renders, and each time the state is change, a re-render will occur. Calling `useState` returns an array with two items; the first is the state, and the second is a `setter` function for the state. We typically seperate these two return values out using array decomposition, and name the setter something which begins with `set`.

Any time you wish to change the value of the state, the `set` function should be used (instead of direct assignment) so that re-rendering is triggered. 

`useState` can take a single argument, which is the initial value of the state; if it is not provided, the state defaults to `undefined`.

```jsx
function Component() {
    const [state, setState] = useState("Hello, World");
    setState("Goodbye, World");

    return (
        <Text>
            {state}
        </Text>
    )
}

```

`useState` is useful when dealing with things like user input; the Furman Now! codebase often will create a state and make color dependent on that state, changing the state (and thus the color) when the a button is pressed.

The setter for `useState` is asynchronous. This means that it can take time - at least one full render, and sometimes longer - for the value of `state` to update to reflect what has been assigned through `setState`. sometimes values can get out of date either inside the render, or potentially in memory if you are reassigning many times rapidly. 

`setState` can take in a value which is directly assigned to the `state`, but also take in an anonymous function which is provided as input the current value of the state and then operate on the value as defined. This can ensure that multiple assignments within the same render are updated in the correct order and to the right value, especially when doing things like incrementing.

```jsx
function Component() {
    const [state, setState] = useState(0);
    setState(1);
    setState(st => st + 1);

    return (
        <Text>
            {state}
        </Text>
    )
}
```