---
layout: default
title: Component Basics
parent: Intro to React Native
nav_order: 1
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

# Component Basics
## Constructing Components
React Native works within a component-based system that mimics HTML. Consider a basic HTML element on a website. It would be built in the following way:

```html
<div>
    Hello, World!
</div>
```

In React Native, we would construct a component in a similar fashion. However, some slight adjustments are needed. React Native components need to be included in some sort of function that can be called by JavaScript, and the elements to construct the document object must be returned from the function. Thus, elements are typically written as a function which returns the tags building the component. This has an added benefit of allowing additional JavaScript code to be executed within the body of the function as is needed. Second, we need specific indications that there will be text elements inside that should be rendered as text. Thus, we write our component like this.

We import `View` and `Text` from the `'react-native'` library, and since we are building a component we also should import `React` from `'react'`.

```jsx
import React from 'react';
import { View, Text } from 'react-native';

function Component() {
    return (
        <View>
            <Text>
                Hello, World!
            </Text>
        </View>
    );
}
```

Rather than `<div>`, React Native uses `<View>`; rather than lower-case names, all components have capital letters, like in `<Text>`. 

To call a component, we would use the name of the function within angled braces; this tag must either be self closing, with a `\>` at the end, or have a closing tag which starts with `</`. 

```jsx
<Component />

// or 

<Component>
    ...
</Component>
```

## Assigning Styles

Just as CSS can apply styling to HTML components, `styles` can be applied to React Native elements. CSS typically uses names in 'kebab-case', such as `border-radius` or `background-color`; React Native styles use camelcase, typically of the exact same names, such as `borderRadius` or `backgroundColor`.

Styles are stored into an object where the key corresponds to the style being set and the value is the specific characteristic for the style.

```jsx
const style = {
    backgroundColor: 'black',
    borderRadius: 14
};
```

Styles are passed as one of the properties, or `props`, of the components. All of these props are assigned within the component's entry tags with an assignment operator. If we are directly assigning text to a prop, we can simply assign a string; however, if we want to use JavaScript, such as assigning a value we have put inside a varable, constructing an object, or using template strings, we must encapsulate these assignments inside of a pair of `{}`.


```jsx
function Component() {
    const style = {
        backgroundColor: 'black',
        borderRadius: 14
    };

    return (
        <View 
            // Direct assignment of boolean. Since
            // booleans are JS, they need to be in {}.
                // accessible indicates that a component and
                // its children should be read as a single
                // unit by a screen reader. 
            accessible={false}
            // Assignment of a variable to the property;
            // it must be within curly braces so React
            // Native knows it is a variable.
            style={style}
        >
            <Text
                // Defining the style object directly in
                // the property assignment field. The first
                // {} indicates that it is JS; the second {}
                // is the object which is being created with
                // the style attributes.
                style={{fontFamily: 'sans-serif', fontSize: 10}}
                // Boolean properties can be set to "true" by simply
                // including the name of the attrubute.
                accessible
                // Direct assignment of string literal.
                    // accessibilityLabel allows us to specify
                    // what a screen reader says for the component.
                accessibilityLabel="Main text"
            >
                Hello, World
            </Text>
        </View>
    );
}
```

## Recieving Props

When a component is called, it recieves the specified props inside of an object; the key is the prop name that has been assigned in the component creation, and the key value is the value that has been assigned. If there are components placed within the tags of the component being called, they are passed as a special component called `children`. If there are no children components within a tag, it should be "self closing" by incluidng `/>` at the end of the tag instead of a second closing `</_name_>` tag; a `<Text />` tag is equivalent to a return. 
```jsx
function HigherComponent() {
    return (
        <Box
            text="Title"
        >
            <Text>
                Hello, World
            </Text>
        </Box>
    );
}

// text is the prop assigned above;
// children are the tags inside of it.
function Box({text, children}) {
    return (
        <View>
            <Text>
                // JavaScript variables must be encapsulated inside of {}
                {text}
            </Text>
            <Text />
            {children}
        </View>
    );
}
```

## PropTypes

Furman Now! follows the AirBNB codebase styleguide in the VS Code linter for React Native. Part of their specifications include using the `propTypes` library to outline the expected props that will be provided to the component when it is called, what their type should be, and what default values should be used for non-required properties. 

`propTypes` are defined for a component by specifying the component's name followed by `propTypes`, which is then assigned an object which matches the style of the prop types. If the prop is required, we include `.isRequired` at the end of the type; if it is not required, a default value *must* be included. This is done in a second assignment, this time assigning `defaultProps` for the component.

```jsx
import PropTypes from 'prop-types';

function Component({text, nums, date, obj, arr}) {
    return (
        <Text>
            {text}
        </Text>
    )
} 
Component.propTypes = {
    text: PropTypes.string.isRequired,
    nums: PropTypes.number,
    date: PropTypes.instanceOf(Date).isRequired,
    arr: PropTypes.arrayOf(
        PropTypes.oneOfType(
            PropTypes.string,
            PropTypes.number,
            PropTypes.instanceOf(Date)
        )
    ).isRequired,
    obj: PropTypes.shape({
        age: PropTypes.number.isRequired,
        name: PropTypes.string.isRequired,
    }).isRequired,
};
Component.defaultProps = {
    nums: 10,
};

```

## Conditional Components
To only display components conditionally, we use boolean operations. If a component is placed within a `{}` and `&&`ed with a boolean `true`, then it will be shown; a `false` will hide the component. This can be a single raw boolean, or a chain of various attributes being compared together.

```jsx
function Component() {
    return (
        {true &&
            (<Text>
                Hello
            </Text>
        )}
    );
}
```













