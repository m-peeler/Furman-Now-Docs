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
*Props:*
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
<dd>String: hex color to color the stop marker</dd>
<dt>website</dt>
<dd>String: route's website</dd>
<dt>vehicleName</dt>
<dd>String: name of the vehicle</dd>
</dl>

Places a marker at the location provided. When clicked, shows a callout with the estimated time of arrival and a button to the route's website.

### ModifiedPolyline
*Props:*
<dl>
<dt>encodedCoordinates</dt>
<dd>String: encoding of polyline route's coordinates</dd>
<dt>strokeWidth</dt>
<dd>Number: width of composite polyline</dd>
<dt>strokeColor</dt>
<dd>String: central color of polyline</dd>
<dt>onPress</dt>
<dd>Function: called with no arguments when polyline is pressed</dd>
</dl>

Creates a double-colored polyline following the coordinates of `encodedCoordinates`, with a white polyline of width `strokeWidth` under a polyline of the color `strokeColor` with a width of 5 less. When the polyline is pressed on, `onPress` is called.

## AthleticsButton

### AthleticsButton
*Props:*
<dl>
<dt>event</dt>
<dd>
    <dl>
    <dt>location_indication</dt>
    <dd>String: "H" or "A" indicating if a game is "Home" or "Away."</dd>
    <dt>eventdate</dt>
    <dd>Date: Date and time of event.</dd>
    <dt>noplayText</dt>
    <dd>String: message indicating if the game has been cancelled.</dd>
    <dt>resultStatus</dt>
    <dd>String: "W", "L" or "N" indicating who won.</dd>
    <dt>sportTitle</dt>
    <dd>String: name of the sport being played.</dd>
    <dt>url</dt>
    <dd>String: optional link to a game recap.</dd>
    </dl>
</dd>
</dl>

A button that displays information on an athletics game. Holding down on the button shows a context menu that allows saving to calendar or sharing information on the event. If a recap link is present, clicking on the button will open the link. 

### AthleticsHeading
*Props:*
<dl>
<dt>heading</dt>
<dd>String: name on the heading</dd>
<dt>date</dt>
<dd>Date: optional date included on the heading</dd>
</dl>

Makes a heading for the list of athletics event on the `Athletics` screen.

## Button
*Props:*
<dl>
<dt>behind</dt>
<dd>Node: React node that will be displayed as the back of the button.</dd>
<dt>front</dt>
<dd>Node or Function: React node that will be displayed as the front of the button. If a function, frontResponsive should be true, and front will be called with the <tt>front</tt> styling of <tt>styles</tt> as its argument.</dd>
<dt>under</dt>
<dd>Node: React node that will be displayed in the space lower on the screen beneath the button<dd>
<dt>styles</dt>
<dd>Object or Function: Contains various optional styling components for different parts of the button. If it is a function, it should take as input a boolean representing whether or not the button is being pressed, and return an object matching the same specifications.
    <dl>
    <dt>cells</dt>
    <dd>Object: styles that are applied to the whole cell of the button; this is the largest possible division of the button and encapsulates the <tt>under</tt> elements as well.</dd>
    <dt>button</dt>
    <dd>Object: styles that are applied to the view containing <tt>front</tt> and <tt>behind</tt> but not <tt>under</tt>.</dd>
    <dt>front</dt>
    <dd>Object: styling provided as argument to the <tt>front</tt> element if <tt>frontResponsive</tt> is true.</dd>
    </dl>
</dd>
<dt>frontResponsive</dt>
<dd>Boolean: indicates whether or not the front's styling is a function that takes in a boolean indicating if the button is pressed and returns a styling object. This allows the front to be response to presses if they are clicked on</dd>
<dt>...rest</dt>
<dd>All remaining arguments are provided to the component where the <tt>button</tt> styling are applied.</dd>
</dl>

A basic button component.

## ButtonList
*Props:*
<dl>
<dt>data</dt>
<dd>Array: List of data in the list</dd>
<dt>style</dt>
<dd>Object: style properties applied to the bounding container of the FlashList</dd>
<dt>...rest</dt>
<dd>All remaining arguments pass to the FlashList</dd>
</dl>

A simple wrapper on `FlashList` that uses a standardized height. 

## ContactContentButton
*Props:*
<dl>
<dt>name</dt>
<dd>String: display name on the button</dd>
<dt>content</dt>
<dd>String or Number: the content being contacted with the button; can be either an email address (string), a url (string), or a phone number (number).</dd>
<dt>priority</dt>
<dd>Boolean: indicates if the button is a priority button with a different color scheme</dd>
<dt>type</dt>
<dd>String: either 'email', 'phone', or 'url' indicating which type the <tt>content</tt> is.</dd>
</dl>

A button that, when clicked, opens a link, launches an email, or gives the option to call. Additionally, holding on the button allows the content to be shared, and for email and phone number, to be saved to contacts. 

## CreditsTab
*Props:*
<dl>
<dt>onPress</dt>
<dd>Function: called with no arguments when the user clicks on the dark-tinted left side of the screen while the CreditsTab is open</dd>
</dl>

Tab displaying various credit information. Version information, which is present here to help with debugging and in assisting with user issues, must be manually updated.

## DHMenuCard
*Props:*
<dl>
<dt>meal</dt>
<dd>String: name of the meal on the card</dd>
<dt>stationMenus</dt>
<dd>Array of key-value pairs, where the key is a station and the value is a list of objects of menu items where <tt>itemName</tt> is the name of a food at the station.</dd>
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

## FurmanNowSearchBar
*Props:*
<dl>
<dt>value</dt>
<dd>String (state): state which holds the text input</dd>
<dt>onChangeText</dt>
<dd>Function: Callback that is called when the text input's text changes, with the changed text passed as an argument. Should include setting the <tt>value</tt> state equal to the changed text.</dd>
<dt>placeholder</dt>
<dd>String: text displayed before any input is added.</dd>
</dl>

A stylized, reusable search bar component that is placed at the top of a screen.

## HomeScreenNavButton
*Props:*
<dl>
<dt>styles</dt>
<dd>
    <dl>
    <dt>label</dt>
    <dd>Object: styles for the text label of the button.</dd>
    <dt>buttonStyles</dt>
    <dd>Object or Function: styles passed to the <tt>Button</tt> component.</dt>
    </dl>
</dd>
<dt>onPress</dt>
<dd>Function: Called when the button is pressed.</dd>
<dt>toPage</dt>
<dd>Page: Page that the button directs to, which provides the icon of the button and the button's name</dd>
</dl>

A button that displays the icon of a `Page` on the front, and its name in text under the button, and calls a function when pressed. 

## StyledTextButton
*Props:*
<dl>
<dt>message</dt>
<dd>String: text displayed in the center of the button</dd>
<dt>onPress</dt>
<dd>Function: Callback that is called when the button is pressed.</dd>
<dt>numberOfLines</dt>
<dd>Number: optional cap on how many lines of text appear in the button.</dd>
</dl>

A pre-styled button that can display text in its center and call a function when pressed.

## Weather
*Props:*
<dl>
<dt>height</dt>
<dd>Number or String: height of the Weather component</dd>
<dt>width</dt>
<dd>Number or String: width of the Weather component</dd>
</dl>

Live weather data is accessed with `useWeatherReport` and background images are accessed using `useWeatherWidgetImages`. Weather is updated every 30 seconds, the background image updates every 20 seconds, and every 60 seconds it refreshes to see if there are new background images. Temperature and percipitation chances are shown above the image using the `TempDisplay` and `PercipDisplay` components, respectively. 

### TempDisplay
<dl>
<dt>high</dt>
<dd>String: forecasted high temperature</dd>
<dt>low</dt>
<dd>String: forecasted low temperature</dd>
<dt>current</dt>
<dd>String: current temperature</dd>
<dt>units</dt>
<dd>String: "F" for Faherenheit or "C" for Celsius</dd>
</dl>

### PercipDisplay
<dl>
<dt>chancePercipitation</dt>
<dd>String: empty string or a string with the percent chance of percipitation</dd>
<dt>weatherEmoji</dt>
<dd>String: hex value for a unicode emoji code point</dd>
</dl>
