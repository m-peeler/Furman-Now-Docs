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
import React, { useState } from 'react';

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
import React, { useState } from 'react';

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

## useRef
`useState` is used when we wish to re-render every time it changes; however, we sometimes do not wish to re-render, and additionally may wish to not have the drawbacks of async changes which `useState` requires. This necessitates the use of `useRef`. 

`useRef` is primarily used to get internal information from a component; if you assign the `ref` property on a component to the `ref` recieved from `useRef`, you will be able to access internal methods and states. `ref`s always store their value within the attribute `ref.current`, so to access these attributes you would use `ref.current.` followed by their name. 


```jsx
import React, { useRef } from 'react';
import MapView from 'react-native-map';

function Component() {
    const ref = useRef(null);

    return (
        <MapView
            ref={ref}
        >
    );
}
```

## useEffect
`useEffect` is used to cause render-specific effects; the React documentation suggests its best use is when connecting to external systems like remote APIs or other websites. `useEffect` takes as input a function which is re-run every render. This is often more common than we would like, and thus a second argument of a 'dependency array' can be provided. If given, the `useEffect` function will only be run when a value within the dependency array is changed. Since we often only want `useEffect` to run on the first render of a component (say, when we are initally pulling information from the server) we will often provide an empty dependency array (i.e. a blank list, `[]`). 

```jsx
import React, { useEffect } from 'react';
import { Text } from 'react-native';

function Component() {
    useEffect(() => 
        console.log("Hello, World")
    , []);

    return (
        <Text>
            Hello!
        </Text>
    );
}

```
`useEffect` will sometimes need resources to be unallocated when a component is finished being used. The most common example of this would be if we are using a `setInterval`, which runs a function every `n` milliseconds. (This is helpful for, say, refreshing the weather every 20 seconds) 

To terminate this repetative calling, we must invoke the `clearInterval` function on our interval. `useEffect` builds in help for this: if this needs to be done, the `return` from the function can simply be a function that clears all resources which need to be cleared. Using `setInterval` and `clearInterval` as an example, this looks like:

```jsx
import React, { useEffect } from 'react';
import { Text } from 'react-native';

function Component() {
    useEffect(() => {
        const interval = setInterval(() => {
            console.log("Refresh");
        }, 20_000);
        return () => clearInterval(interval);
    }, []);


    return (
        <Text>
            Hello!
        </Text>
    );
}
```