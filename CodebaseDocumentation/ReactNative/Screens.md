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
## HomeScreen.jsx
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
Dates includes a `react-native-reanimed-carousel` of four types of important dates - CLPs, on-campus events, undergraduate academic calendar, and graduate calendar (the first two with the `useCampusEvents` hook, the later two using the `useImportantDates` hook). The "events" include a description, which is fully displayed if the button is clicked on; the "dates" do not include descriptions. If any additional types of dates are desired to be added, it can be done serverside by adding them to the CLP or ImportantEvents tables with a unique eventType.

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

## Hours

## Links

## Map

## Parking

## Safety

## Transit