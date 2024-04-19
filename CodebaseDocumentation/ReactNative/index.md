---
layout: default
title: React Native Documentation
nav_order: 1
parent: Codebase Documentation
has_children: true
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# React Native Documentation
## Dependencies
The Furman Now! app is built using the [Expo] developers environment on top of React Native, which includes some improved components (the codebase uses Expo's `Image` component rather than the default `react-native` one), as well easier dependency handling, platform-specific disclosures, cloud-based building of the mobile app bundles and over-the-air releases of small changes. 

Furman Now! also uses several libraries for easier construction, improved performance, and nice animations. 

The [Shopify FlashList] is used as a more performant alternative to `react-native`'s `FlatList` for scrollable lists of elements. 

`[react-native-maps]` are used for the `MapView` component to show Apple/Google Maps for the campus map and the shuttle map. 

`[react-native-reanimated-carousel]` is used for the carousel views in the News section, the Dining Section, and the Events section; because of this dependency `[react-native-reanimated]` is used for animations when needed.



---
[Expo]: https://expo.dev/
[Shopify FlashList]: https://shopify.github.io/flash-list/
[react-native-maps]: https://github.com/react-native-maps/react-native-maps
[react-native-reanimated-carousel]: https://reanimated-carousel.dev/
[react-native-reanimated]: https://docs.swmansion.com/react-native-reanimated/
