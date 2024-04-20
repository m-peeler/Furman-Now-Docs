---
layout: default
title: Screens
nav_order: 2
parent: React Native Documentation
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# Screens
## HomeScreen
The main screen of the Furman Now! app is the home screen, which links to the other screens. It is treated as having three sections: the `WeatherWidget` at the top which displays an image and the current weather, the `buttonPanel` which is a grid of icon buttons, and the `newsFeed` button at the bottom which links to the news feed. Each section is allocated a percentage of the available screen space; the `WeatherWidget` recieves 2/7, the News Feed 1/7, and the button panel the remaining 4/7. The button panel's buttons are generated dynamically from the list provided in the `route.params.pages` prop, which is passed in when `Stack.Screen` is given an initial paramter of `pages`. 

```jsx
// Simplified example of passing an initial parameter using Stack.Screen.
const pages = [...]

function HomeScreen({ route : {params: {pages} }, navigation: { navigate } }) {
    return (
        <FlashList
            data={pages}
            renderItem={({ item: page }) => 
                // The page's name is used in navigation.jsx to define
                // the screen, so this allows us to launch it.
                onPress={() => navigate(page.name)}
                // Passes things like the icon and name to the button
                toPage={page}
            }
            {...}
        />
    )
}
HomeScreen.propTypes = {
  navigation: PropTypes.shape({
    navigate: PropTypes.func.isRequired,
  }).isRequired,
  route: PropTypes.shape({
    params: PropTypes.shape({
      pages: PropTypes.arrayOf(
        PropTypes.instanceOf(Page),
      ).isRequired,
    }).isRequired,
  }).isRequired,
};

function Navigator() {
    return (
        <Stack.Navigator
            initialRouteName="Home"
        >
            <Stack.Group>
                <Stack.Screen
                    name="Home"
                    component={HomeScreen}
                    initialParams={{
                        pages: pages
                    }}
                >
            </Stack.Group>
        </Stack.Navigator>

    )
}
```

`HomeScreen` also uses the `CreditsTab` component to display the app's credits when the `i` button in the top right corner is pressed. 

## Athletics
The Athletics screen displays recent and upcoming events. These are fetched with the `useAthleticsCalendar` custom hook, and then placed into a list which can be displayed on. The entries use the `AthleticsButton` component, as well as the `AthleticsHeading` component for the day-based headings. Buttons display various information about the games; if they are pressed and the game is finished, it will direct to a game recap. Long-pressing activates a context menu for saving to calendar or sharing.

## Contacts
Contacts are fetched from online using the `useContacts` custom hook, and displayed as a list of `ContactContentButton`s. The highest priority button - Furman Police's - is attached to the top and highlighted in a seperate color for easier use, while other buttons can be scrolled through. 

Contacts are sorted first by priority level (highest first), and then alphebetically within priority levels. 

The `emergencyThreshold` variable is used to set which levels of priority should be given the `emergencyStyle`, which primarily includes a red colored background.

## Dates
Dates includes a `react-native-reanimed-carousel` of four types of important dates - CLPs, on-campus events, undergraduate academic calendar, and graduate calendar (the first two with the `useCampusEvents` hook, the later two using the `useImportantDates` hook). The "events" include a description, which is fully displayed if the button is clicked on, as well as an organizer and a location; the "dates" do not include these three items.

The carousel view can sometimes have strange visual effects when loading multiple screens in, so only the first date screen is initially loaded, with later screens being added to their carousel 450 milliseconds later. 

Events are displayed on an `EventsDisplay` component, and dates on an `ImportantDatesDisplay`. 

In screen reader modes, `Carousel` does not have any way for a reader to move between carousel items. To ensure accessibility, `useRef` is used to create a `carouselRef` which allows access to the `scrollTo` function of the `Carousel`; these are passed along with the `accessibilityProps` to the `Display`s. This allows users to click on the title at the top of each `Display` and swipe their finger up or down to scroll between screens.

Buttons are placed at the top of each card to additionally scroll left and right, and to indicate that scrolling is an option. `isFirst` and `isLast` are used to determine which of these arrows are shown; the first element will exclude the left arrow and the last the right arrow. the `onRotateButton` function will be called when either button is pressed, and will be passed the number by which the `Carousel` should be incremented (1 or -1 for right and left, respectively). 

## Dining
Dining menus are accessed using the `useDiningMenu` custom hook. The `DHMenuCard` component renders out the menu for each meal, including divisions by station. 

Just as with `Dates`, for screen reader scrollability, `accessibilityProps` are passed to the `DHMenuCard` using a function from `carouselRef` attached to the `Carousel`.

Again in keeping with `Dates`, left and right buttons are included, and `isFirst`  `isLast` attributes indicate which should be show, and `onRotateButton` allows this screen change.

The `defaultIndex` of the `Carousel` is calculated to approximate the current, or next, meal, so that displays will be relevant to the user. `calcDefaulIndex` is called with the number of m

## Feed
News articles and publishes are accessed using `useNewsArticles` and `useNewsPublishers`, respectively. Articles are searchable using a `FurmanNowSearchBar`, and the value typed here is searched for inside titles, descriptions, publisher name, and author name using the `searchArticles` function. Single `Articles` are shown as a `NewsItemCard` component, while collated lists (`Articles` from the same publisher released within close proximity to each other) are shown in a `NewsCardStack`. 

## Hours
Building opening hours are accessed using `useBuildingHours`. Hours are shown in a list of elements which, in the unengaged form, show the building's name and if it is currently open using the `HoursTitleBar`, as well as the hours for the current day. A single entry in the list of hours can be set `engaged` by clicking on it, and an `engaged` button can be toggled off by clicking on it again, or by clicking another set of hours you wish to engage. This is controlled through the `HoursButton` component within `Hours.jsx`. 

The `engaged` button also shows two other buttons: one which directs to the building's website, and the other which directs to its location on the `Map` screen.

### HoursButton
*Props:*
<dl>
<dt>item</dt>
<dd>Array: Key-Value pair, where key is the building name and value contains  information about the building; an entry directly from the <tt>data</tt> variable of <tt>useBuildingHours</tt>.</dd>
<dt>index</dt>
<dd>Integer: Index of the hour on the list; used to determine if the button is currently engaged.
<dt>onPress</dt>
<dd>Function: Takes as input no arguments, and called when <tt>HoursButton</tt> is pressed.</dd>
<dt>styles</dt>
<dd>Function: A function which takes as input a boolean state indicating if HoursButton is currently pressed. It returns an object with four style entries: <tt>locationText</tt>, which will be provided to the <tt>HoursTitleBar</tt> as styling; <tt>button</tt>, which is styling for the background of the button, <tt>dayText</tt>, which is styling for the text on the left of the button that shows which day of the week hours pertain to; and <tt>hoursText</tt>, which is applied to the text on the right which shows which hours the building is open each day. If the boolean provided is true, the button is being pressed, and the styles should change accordingly.  
<dt>buttonEngaged</dt>
<dd>Integer: Index of the button currently engaged, -1 if no button is.</dd>
<dt>onNavigate</dt>
<dd>Function: Function called with no parameters when user clicks on a button to show the Map view.</dd>
</dl>

Expandable button which shows information for the hours a building is open, using the `<Schedule>` object of the building's `index[1].schedule`. If the `HoursButton` is touched, it sets the `pressed` variable to true (which reverts when touch is ended), and if pressed, it becomes `engaged`, showing the hours for the whole week (where it was previously limited to the current day)

When engaged, two buttons are also visible which allow navigation to the building's website or their location on the `Map` screen. 

### HoursTitleBar
*Props:*
<dl>
<dt>styles</dt>
<dd>Object: An object containing the styles which should be applied to various parts of the HoursTitleBar. The <tt>title</tt> style is applied to the building's name, the <tt>subtitle</tt> style to the building's nickname, and the <tt>openIndicator</tt> function, which is provided with the current status of the building ("OPEN", "CLOSED", or "CLOSES SOON") and returns an object with the style for the status indicator circle.
<dt>name</dt>
<dd>String: The building's full name.</dd>
<dt>nickname</dt>
<dd>String: Shortened and common nickname for the building, displayed below the name if provided.</dt>
<dt>information</dt>
<dd>Object: Contains a <tt>schedule</tt> key whose value is a <tt>Schedule</tt> for the building.</dd>
</dl>

Displays the building's name/nickname and current open/closed/closes soon status. 

## Links
Important links are accessed using `useImportantLinks` and displayed as a list of `ContactContentButton`s. 

## Map
Building information is accessed using `useBuildingInformation` and displayed as `BuildingMarker`s on an `FUNowMapView`. These `BuildingMarkers` which are shapes (if an encoded polyline defining its perimiter is provided for the building) or pins on the map. 

If a `BuildingMarker` is clicked on, the `MapInfoOverlay` is shown, which includes information about the clicked building. Clicking on another building will change the overlay to show informaiton on that building, while clicking elsewhere on the map will dismiss the overlay. `setQualifiedDisplaying` is used to control this logic, and stop clicks from being double counted to either close the overlay immediately after opening, or cause it to flicker off before flickering back on with the new information.

A `FurmanNowSearchBar` allows user input to filter out items on the map to only those who include the information provided in their name, nickname, or description. If only a single building matches the user input, the map zooms to focus on it.

When navigating to `Map`, using the `navigate` method of `navigator`, including the parameter `name` in `initialParams` will cause `name` to be set as the initial search term when `Map` is opened, and the map will zoom to focus on its location. A slight delay is placed on setting `name` to be the search term so that this moving animation is seen.

A `mapRef` from the `useRef` hook is attached to the map to allow movement to a specific location.

## Parking

## Safety

## Transit