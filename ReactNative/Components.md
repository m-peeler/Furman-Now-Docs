---
layout: default
title: Components
parent: Intro to React Native
nav_order: 1
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

# Components

React Native works within a component-based system that mimics HTML. Consider a basic HTML element on a website. It would be built in the following way:

```html
<div>
    Hello, World!
</div>
```

In React Native, we would construct a component in a similar fashion. However, some slight adjustments are needed. React Native components need to be included in some sort of function that can be called by JavaScript, and the elements to construct the document object must be returned from the function. Thus, elements are typically written as a function which returns the tags building the component. This has an added benefit of allowing additional JavaScript code to be executed within the body of the function as is needed. Second, we need specific indications that there will be text elements inside that should be rendered as text. Thus, we write our component like this.

```jsx
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



