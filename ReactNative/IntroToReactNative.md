---
layout: default
title: Intro to React Native
nav_order: 3
has_children: true
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

# A Basic Introduction to React Native

React Native, and React (which React Native is based on), are frameworks within JavaScript to make web and app development easier. It implements several new constructs to the langauge to improve the ability of programmers to build these systems, and implements new features that work within these constructs. 


React Native works within a component-based system that mimics HTML. Consider a basic HTML element on a website. It would be built in the following way:

```html
<div>
    <text>
        Hello, World!
    <text>
<div>
```

In React Native, we would construct similar component in this fashion:

```jsx
<View>
    <Text>
        Hello, World!
    <Text>
<View>
```

Rather than `<div>`, React Native uses `<View>`; rather than lower-case names for `<text>`, it uses `<Text>`. 

Just as CSS can apply styling to HTML components, `styles` can be applied to React Native elements.