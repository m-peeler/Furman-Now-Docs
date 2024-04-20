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
<dd>String: encoded polyline of the building's perimeter shape, if the building's shape on the map is preferable to a pin.</dd>
<dt>locationText</dt>
<dd>String: summary of building's location</dd>
<dt>category</dt>
<dd>String: category to decide color of element.</dd>
<dt>onPress</dt>
<dd>Function: triggered when building is clicked on.</dd>
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

An overlay that includes information about the building that has been clicked on. Additionally, the overlay includes buttons which link to directions to the location on the system's maps (using `linkForDirections` to generate the link), and to the building's website (if it has one). Holding down on the former allows location to be shared, holding on the latter allows the website to be shared. 

## News Components
### NewsCardWrapper 
*Props:*
<dl>
<dt>children</dt>
<dd>Array or node: Either one node or an array of nodes</dd>
<dt>height</dt>
<dd>Number: card's height</dd>
<dt>width</dt>
<dd>Number: card's width</dd>
<dt>headline</dt>
<dd>String: article's headline</dd>
<dt>link</dt>
<dd>String: link to article's website.</dd>
<dt>color</dt>
<dd>String: hex code of card's background color</dd>
<dt>publisher</dt>
<dd>String: name of publication of article</dd>
<dt>publisherLink</dt>
<dd>String: link to publication website</dd>
</dl>

Adds a context menu to wrap `NewsItemCard`s with, allowing for sharing of content and accessing links to the site. 

### NewsItemCard
*Props:*
<dl>
<dt>height</dt>
<dd>Number: card's height</dd>
<dt>width</dt>
<dd>Number: card's width</dd>
<dt>article</dt>
<dd>Article</dd>
<dt>publisher</dt>
<dd>String: name of publication of article</dd>
<dt>publisherLink</dt>
<dd>String: link to publication website</dd>
<dt>publisherImageLink</dt>
<dd>String: link to default display image for articles from the publisher without an image link.</dd>
</dl>

Provided with attributes for an `Article` and seperates it into a specific type of NewsCard based on its `MediaType`.

### NewsLinkCard
*Props:*
<dl>
<dt>height</dt>
<dd>Number: card's height</dd>
<dt>width</dt>
<dd>Number: card's width</dd>
<dt>article</dt>
<dd>Article</dd>
<dt>publisher</dt>
<dd>String: name of publication of article</dd>
<dt>publisherLink</dt>
<dd>String: link to publication website</dd>
<dt>publisherImageLink</dt>
<dd>String: link to default display image for articles from the publisher without an image link.</dd>
<dt>onPress</dt>
<dd>Function: function called when card is pressed, allowing an external function to know it has been pressed</dd>
<dt>touchState</dt>
<dd>
    <dl>
    <dt>state</dt>
    <dd>boolean: if card is currently being pressed. Allows an external function to know when the card has been pressed. </dd>
    <dt>setter</dt>
    <dd>Function: sets state to value provided.</dd>
    <dt></dt>
    </dl>
</dd>
</dl>

NewsCard for `LINK` `MediaType`. Displays image, as well as headline, author, publication, section, and publication date. Clicking send the reader to the article.

### NewsYoutubeCard
*Props:*
<dl>
<dt>height</dt>
<dd>Number: card's height</dd>
<dt>width</dt>
<dd>Number: card's width</dd>
<dt>article</dt>
<dd>Article</dd>
<dt>publisher</dt>
<dd>String: name of publication of article</dd>
<dt>publisherLink</dt>
<dd>String: link to publication website</dd>
<dt>publisherImageLink</dt>
<dd>String: link to default display image for articles from the publisher without an image link.</dd>
</dl>

NewsCard for `VIDEO` `MediaType`. Before click, it displays a `NewsLinkCard` for the video with the video's thumbnail as the image, as well as headline, author, publication, section, and publication date. Clicking activates the YouTube embed, playing the video.

### NewsCardStack
*Props:*
<dl>
<dt>cardWidth</dt>
<dd>Number: card's width</dd>
<dt>cardHeigh</dt>
<dd>Number: card's height</dd>
<dt>articles</dt>
<dd>Array: an array of articles</dd>
<dt>sources</dt>
<dd>Object: an object containing information on the various publishers with publisherID as the key</dd>
</dl>

`Carousel` of multiple articles, with a `NewsStackFrontCard` on top. 

### NewsStackFrontCard
*Props:*
<dl>
<dt>cardWidth</dt>
<dd>Number: card's width</dd>
<dt>cardHeigh</dt>
<dd>Number: card's height</dd>
<dt>articles</dt>
<dd>Array: an array of articles</dd>
<dt>publisher</dt>
<dd>Object: an object of publisher information</dd>
<dt>onPress</dt>
<dd>Function: a function called with no arguments when the stack front card is pressed.</dd>
</dl>

Front card of a `NewsCardStack` that displays a message about reading articles and cycles through the photos/titles of articles within its list.

## Transit Components
### BusMarker
*Props:*
<dl>
<dt>name</dt>
<dd>String: bus' name</dd>
<dt>color</dt>
<dd>String: hex color to tint the bus icon</dd>
<dt>rotation</dt>
<dd>Number: the angle of rotation of the bus. Android can do flat icons, so a compass heading is preferred; iOS cannot do flat icons, so the compass heading should have the <tt>Map</tt>'s current heading subtracted from it to get the bus' relative heading on the map.</dd>
<dt>coordinate</dt>
<dd><dl>
    <dt>latitude</dt>
    <dd>Number: Building's latitude</dd>
    <dt>longitude</dt>
    <dd>Number: Building's longitude.</dd>
</dl></dd>
</dl>

Marker to show transit vehicles' current location and directional heading.

### BusRoute
*Props:*
<dl>
<dt>route</dt>
<dd>String: encoded polyline of the route</dd>
<dt>color</dt>
<dd>String: hex color to color the route line & stop markers</dd>
<dt>website</dt>
<dd>String: route's website</dd>
<dt>vehicleName</dt>
<dd>String: name of the vehicle</dd>
<dt>stops</dt>
<dd>Array of objects of
    <dl>
    <dt>name</dt>
    <dd>String: stop's name</dd>
    <dt>coordinate</dt>
    <dd><dl>
        <dt>latitude</dt>
        <dd>Number: Building's latitude</dd>
        <dt>longitude</dt>
        <dd>Number: Building's longitude.</dd>
    </dl></dd>
    <dt>vehicleStopsUntil</dt>
    <dd>Number: number of stops that the vehicle will stop at before it gets to this stop.</dd>
    <dt>distFromVehicle</dt>
    <dd>Number: number of miles that the vehicle is from the stop, assuming it follows the route.</dd>
    <dt>updated</dt>
    <dd>Date: the last time that information on vehicle distance and stopsUntil was calculated.</dd>
    </dl>
</dd>
</dl>

### BusStopMarker
<dl>
<dt>title</dt>
<dd>String: stop's name</dd>
<dt>coordinate</dt>
<dd><dl>
    <dt>latitude</dt>
    <dd>Number: Building's latitude</dd>
    <dt>longitude</dt>
    <dd>Number: Building's longitude.</dd>
</dl></dd>
<dt>eta</dt>
<dd>String: message indicated the estimated time of arrival.</dd>
<dt>color</dt>
<dd>String: hex color to color the route line & stop markers</dd>
<dt>website</dt>
<dd>String: route's website</dd>
<dt>vehicleName</dt>
<dd>String: name of the vehicle</dd>
</dl>

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