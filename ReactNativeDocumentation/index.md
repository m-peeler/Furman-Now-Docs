---
layout: default
title: React Native Documentation
nav_order: 4
has_children: true
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# React Native Documentation
## Dependencies
The Furman Now! app is built using the [Expo] developers environment on top of React Native, which includes some improved components (the codebase uses Expo's `Image` component rather than the default `react-native` one), as well easier dependency handling, platform-specific disclosures, cloud-based building of the mobile app bundles and over-the-air releases of small changes. Various Expo libraries are used within the app, such as its user location library, its font importation library, and its libraries to access calendar and contact information.

Furman Now! also uses several libraries for easier construction, improved performance, and nice animations. 

The [Shopify FlashList] is used as a more performant alternative to `react-native`'s `FlatList` for scrollable lists of elements. 

[react-native-maps] are used for the `MapView` component to show Apple/Google Maps for the campus map and the shuttle map. 

[react-native-reanimated-carousel] is used for the carousel views in the News section, the Dining Section, and the Events section; because of this dependency [react-native-reanimated] is used for animations when needed.

[react-native-context-menu-view] is used to display context menus when buttons are pressed down, such as those that allow calendar events to be saved or news stories to be shared. 

[react-navigation] is used to move between screens, as well as to share themes throughout the app using the `useTheme` hook.

Remaining dependencies can be found in the `packages.json` file in the root directory of the Furman Now! React Native codebase. 

## Dev Tools
Furman Now! uses Node.js, and thus `npm` is the main package manager.

The [Expo CLI] is primarily used for installing packages, as well as running the development server. This is effectively a way of calling `npx [package] --save`, in addition to several other housekeeping techniques. 

[EAS], the Expo Application Services, is used for the over-the-air updates and remote building mentioned above. It can also handle submission to the App Store and Play Store, so long as the account information stored in the `eas.json` `submit` field are accurate and working. 

The [eslint] extension to VS Code is used as a linter for the project, utilizing the AirBNB style guide and several plugins that allow the linter to work with React Native in addition to pure JavaScript.

The [prop-types] package, explained in more detail in the [Intro to React Native] section, is a package for enforcing typing requirements on components. The AirBNB style guide requires usage for all components which recieve props. 



---
[Expo]: https://expo.dev/
[EAS]: https://expo.dev/eas
[Shopify FlashList]: https://shopify.github.io/flash-list/
[react-native-maps]: https://github.com/react-native-maps/react-native-maps
[react-native-reanimated-carousel]: https://reanimated-carousel.dev/
[react-native-reanimated]: https://docs.swmansion.com/react-native-reanimated/
[react-native-context-menu-view]: https://github.com/mpiannucci/react-native-context-menu-view
[Expo CLI]: https://docs.expo.dev/more/expo-cli/
[eslint]: https://eslint.org/
[prop-types]: https://www.npmjs.com/package/prop-types
[Intro to React Native]: https://m-peeler.github.io/FurmanNowDocs/ReactNative/Components.html