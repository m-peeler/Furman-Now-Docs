---
layout: default
title: Components
nav_order: 4
parent: React Native Documentation
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# Components
## Dates Components
### DateButton
*Props:*
<dl>
<dt>event</dt>
<dd>
    <dl>
    <dt>timeRange</dt>
    <dd>HourRange: time the event is occuring</dd>
    <dt>date</dt>
    <dd>Date: date of the event</dd>
    <dt>title</dt>
    <dd>String: title of the event</dd>
    <dt>term</dt>
    <dd>String: which term of the school year the event is during</dd>
    </dl>
</dd>
</dl>

Button which displays information about a date. If the button is held down, users can save it to calendar or share it. 

### EventButton
*Props:*
<dl>
<dt>title</dt>
<dd>String: title of the event</dd>
<dt>description</dt>
<dd>String: description of the event</dt>
<dt>start</dt>
<dd>Date: start time of the event</dd>
<dt>end</dt>
<dd>Date: end time of the event</dd>
<dt>date</dt>
<dd>Date: date of the event</dd>
<dt>organize</dt>
<dd>String: organizer of the event</dd>
<dt>location</dt>
<dd>String: location of the event</dd>
</dd>
</dl>

Button which displays information about an event. If the button is held down, users can save it to calendar or share it. 

### EventsDisplay
*Props:*
<dl>
<dt>name</dt>
<dd>String: name displayed on top of display card</dd>
<dt>events</dt>
<dd>Array: list of events</dd>
<dt>accessibilityProps</dt>
<dl>
    <dt>accessible</dt>
    <dd>Boolean: indicates if the title of the card is accessible</dd>
    <dt>accessibilityRole</dt>
    <dd>String: If provided, should be 'adjustable', which means a swipe up or down on the object can increment or decrament and move to the next one.</dd>
    <dt>accessibilityActions</dt>
    <dd>Array: array of objects with one key-value; should be {name: "increment"} and {name: "decrement"}</dd>
    <dt>onAccessibilityAction</dt>
    <dd>Function: takes as input the names of the provided accessibilityAction invoked and causes change based on it; an 'increment' should move the carriage one card to the right and a 'decrement' one card to the left.</dd>
</dl>
<dt>onRotateButtons</dt>
<dd>Function: called with either a 1 (right arrow) or a -1 (left arrow) if either of the arrow navigation buttons are pressed, causing the carraige to rotate in the pressed direction</dd>
<dt>isFirst</dt>
<dd>Boolean: set true for the first card in a carraige; if true, the left arrow will be hidden</dd>
<dt>isLast</dt>
<dd>Boolean: set true for the last card in a carraige; if true, the right arrow will be hidden</dd>
</dl>

Display card for Events buttons; angled arrow buttons at the top can be pressed to rotate the carriage of events cards.

### ImportantDatesDisplay
*Props:*
<dl>
<dt>name</dt>
<dd>String: name displayed on top of display card</dd>
<dt>events</dt>
<dd>Array: list of events</dd>
<dt>accessibilityProps</dt>
<dl>
    <dt>accessible</dt>
    <dd>Boolean: indicates if the title of the card is accessible</dd>
    <dt>accessibilityRole</dt>
    <dd>String: If provided, should be 'adjustable', which means a swipe up or down on the object can increment or decrament and move to the next one.</dd>
    <dt>accessibilityActions</dt>
    <dd>Array: array of objects with one key-value; should be {name: "increment"} and {name: "decrement"}</dd>
    <dt>onAccessibilityAction</dt>
    <dd>Function: takes as input the names of the provided accessibilityAction invoked and causes change based on it; an 'increment' should move the carriage one card to the right and a 'decrement' one card to the left.</dd>
</dl>
<dt>onRotateButtons</dt>
<dd>Function: called with either a 1 (right arrow) or a -1 (left arrow) if either of the arrow navigation buttons are pressed, causing the carraige to rotate in the pressed direction</dd>
<dt>isFirst</dt>
<dd>Boolean: set true for the first card in a carraige; if true, the left arrow will be hidden</dd>
<dt>isLast</dt>
<dd>Boolean: set true for the last card in a carraige; if true, the right arrow will be hidden</dd>
</dl>

Display card for ImportantDates buttons; angled arrow buttons at the top can be pressed to rotate the carriage of events cards.

## Map Components

## News Components

## Transit Components

## AthleticsButton

## Button

## ButtonList

## ContactContentButtonn

## CreditsTab

## DHMenuCard

## FurmanNowSearchBar

## HomeScreenNavButton

## StyledTextButton

## Weather