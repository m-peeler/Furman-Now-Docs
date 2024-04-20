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
<dd><dl>
    <dt>accessible</dt>
    <dd>Boolean: indicates if the title of the card is accessible</dd>
    <dt>accessibilityRole</dt>
    <dd>String: If provided, should be 'adjustable', which means a swipe up or down on the object can increment or decrament and move to the next one.</dd>
    <dt>accessibilityActions</dt>
    <dd>Array: array of objects with one key-value; should be {name: "increment"} and {name: "decrement"}</dd>
    <dt>onAccessibilityAction</dt>
    <dd>Function: takes as input the names of the provided accessibilityAction invoked and causes change based on it; an 'increment' should move the carriage one card to the right and a 'decrement' one card to the left.</dd>
</dl></dd>
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
<dd><dl>
    <dt>accessible</dt>
    <dd>Boolean: indicates if the title of the card is accessible</dd>
    <dt>accessibilityRole</dt>
    <dd>String: If provided, should be 'adjustable', which means a swipe up or down on the object can increment or decrament and move to the next one.</dd>
    <dt>accessibilityActions</dt>
    <dd>Array: array of objects with one key-value; should be {name: "increment"} and {name: "decrement"}</dd>
    <dt>onAccessibilityAction</dt>
    <dd>Function: takes as input the names of the provided accessibilityAction invoked and causes change based on it; an 'increment' should move the carriage one card to the right and a 'decrement' one card to the left.</dd>
</dl></dd>
<dt>onRotateButtons</dt>
<dd>Function: called with either a 1 (right arrow) or a -1 (left arrow) if either of the arrow navigation buttons are pressed, causing the carraige to rotate in the pressed direction</dd>
<dt>isFirst</dt>
<dd>Boolean: set true for the first card in a carraige; if true, the left arrow will be hidden</dd>
<dt>isLast</dt>
<dd>Boolean: set true for the last card in a carraige; if true, the right arrow will be hidden</dd>
</dl>

Display card for ImportantDates buttons; angled arrow buttons at the top can be pressed to rotate the carriage of events cards.

## Map Components
### FUNowMapView
*Props:*
<dl>
<dt>children</dt>
<dd>Array or React node: An array of React Native nodes, or a single node, which will be displayed as children of the MapView.</dd>
<dt>zoom</dt>
<dd>Number: the desired magnification level of the map from its base position.</dd>
<dt>accessibilityProps</dt>
<dt>onPress</dt>
<dd>Function: called when the map is pressed on.</dd>
<dt>onRegionChange</dt>
<dd>Function: function called when the map's region changes</dd>
<dt>overlayElements</dt>
<dd>Array or React node: either a single, or an array of, React nodes which will be displayed as children of the MapView's border views. This is necessary because the MapView can have issues rendering updates to components that are not from the <tt>react-native-maps</tt> package.</dd>
</dl>

This custom map view centers the map on Furman and draws a standard border around it. 

Since the `ref` from the `FUNowMapView` is necessary for moving the map, as well as keeping the transit vehicle icons flat, it must be attachable; however, since we are using function components, this normally wouldn't be possible. Using the `forwardRef` method lets us pass the props as well as an attached ref into the original `MapView`.

### BuildingMarker
*Props:*
<dl>
<dt>name</dt>
<dd>String: name of building</dd>
<dt>nickname</dt>
<dd>String: optional nickname of building</dd>
<dt>coordinate</dt>
<dd><dl>
    <dt>latitude</dt>
    <dd>Number: Building's latitude</dd>
    <dt>longitude</dt>
    <dd>Number: Building's longitude.</dd>
</dl></dd>
<dt>polyline</dt>
<dd>String: encoded polyline of the building's perimeter shape, if the building's shape on the map is preferable to a pin.
<dt>locationText</dt>
<dd>String: summary of building's location</dd>
<dt>category</dt>
<dd>String: category to decide color of element</dd>
<dt>onPress</dt>
<dd>Function: triggered when building is clicked on</dd>
</dl>

Displays the building on a map. Must be a direct child of the `MapView`, i.e. cannot be a grandchild inside of a `View`. 

### MapInfoOverlay
*Props:*
<dl>
<dt>displayInfo</dt>
<dd><dl>
    <dt>coordinate</dt>
    <dd>Object: a number <tt>latitude</tt> and a <tt>longitude</tt></dd>
    <dt>name</dt>
    <dd>String: name of the building.</dd>
    <dt>nickname</dt>
    <dd>String: an optional briefer/better known nickname, which is given priority in display.</dd>
    <dt>website</dt>
    <dd>String: a link to a website for the building.</dd>
    <dt>description</dt>
    <dd>String: a description of the building.</dd>
</dl></dd>
</dl>


An overlay that includes information about the building that has been clicked on.

## News Components
### NewsCardWrapper

### NewsItemCard

### NewsLinkCard

### NewsYoutubeCard

### NewsCardStack

### NewsStackFrontCard


## Transit Components
### BusMarker

### BusRoute

### BusStopMarker

### ModifiedPolyline


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