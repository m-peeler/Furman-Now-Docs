---
layout: default
title: Hooks
nav_order: 3
parent: React Native Documentation
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# Hooks
Furman Now! uses a number of custom hooks, extracted into this function so that they can be reused if necessary. 

## useDataLoadFetchCache

**Arguments:**
<dl>
<dt>fetchFrom</dt>
<dd>String: Website that JSON is being fetched from</dd>
<dt>cacheTo</dt>
<dd>String: Name of the cache space that the fetched website will be cached to</dd>
<dt>processFetch</dt>
<dd>Anonymous function: Provided with the data fetched from fetchFrom, or the cache of it saved, and returns the processed form of the data. Defaults to no processing.</dd>
<dt>discardCache</dt>
<dd>Anonymous function: Provided with the result after <tt>processFetch</tt> has been called on the cached data. If it returns true, the cache will be deleted, and its value will not be used in the app. Defaults to never discard cache.</dd>
</dl>

**Returns:**
<dl>
<dt>data</dt>
<dd>Object (state): Most recent fetch (including potentially cached value) of the requested data.</dd>
<dt>loading</dt>
<dd>Boolean (state): Indicates whether data is currently being loaded from cache; true indicates async cache access has not yet finished.</dd>
<dt>fetching</dt>
<dd>Boolean (state): Indicates whether data is currently being fetched from the web; true indicates asynch fetch has not yet finished.</dd>
<dt>exists</dt>
<dd>Boolean (state): Indicates whether there has been a successful fetch or load yet; if true, <tt>data</tt> has information within it.</dd>
<dt>refresh</dt>
<dd>Anonymous Function: Invokable to re-fetch data from the provided.</dd>
</dl>

`useDataLoadFetchCache` does three things: it loads the last-recieved result from the asynchronous storage cache, it fetches a new result from a specified website, and it caches the result the fetch is successful. Newly fetched data will replace cached data when it is recieved. 

Since loading from cache and fetching from web are both asynchronous, but the former tends to be faster, both are called. Once cache has been accessed, cached data is provided in the `data` state until fetched data has been recieved.

Every other custom hook in Furman Now! is effectively a wrapper for `useDataLoadFetchCache`, providing specific parameters to the function to pull information from a specified site and process it in the intended way.

## useAthleticsCalendar
**Returns:** *Same as `useDataLoadFetchCache`*
<dl>
<dt>data</dt>
<dd>String || Object: Either a string heading, or an object with data for an event. Event data is provided unchanged from the server pull, with the exception of <tt>eventdate</tt> which is parsed into a <tt>Date</tt> object, and <tt>allDay</tt>, which is a boolean of true if the time of <tt>eventdate</tt> is midnight.</dd>
</dl>

Provides a list of either string headings or objects representing recent and upcoming athletics events. Events are fetched from the server and partitioned into either `Recent` (if they have already finished), `Today`, `Tomorrow`, `This`(ie This Week) and `Next` (ie Next Week) using `arrayPartition`. Events within each partition are sorted in order by their time. 

## useBuildingHours
**Returns:** 
<dl>
<dt>data</dt>
<dd>Array (state): contains an array of arrays with information about campus buildings with hours and their hours of operation. Each entry in the array is of the form <tt>[buildingName, {schedule, lastUpdated, ...buildingData[key]}}</tt></dd>
<dt>dataExists</dt>
<dd>Boolean (state): indicates whether or not information has been successfully loaded/fetched and joined together, meaning that the <tt>data</tt> state is defined.</dd>
</dl>

Accesses both the list of buildings on campus, and the list of hours for buildings with hours. Hours are partitioned based on building, then each partition is combined into a `schedule` object, which is then added to the object in each entry's list in addition to the building's name. Other fields inside the entry are proided directly from the server fetch.

```js
const [data] = useBuildingHours();

console.log(data[0]);
/* ['PAC',
 *  {
 *   schedule: <Schedule>,
 *   lastUpdated: '12:34:56 2024-03-19',
 *   name: 'PAC',
 *   ... 
 *  }
 * ]
 */
```

## useBuildingInformation
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches information on campus buildings from the server using `useDataLoadFetchCache`, returning it unaltered save for parsing `latitude` and `longitude` as floats and assembling them into a `coordinate` of: 
```js
const obj = { coordinate : 
    { 
        latitude: parseFloat(result.latitude), 
        longitude: parseFloat(result.longitude)
    }};
```

## useCampusEvents
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches the events and partitions them into `CLPs` and `Other Events`, with the `CLPs` partition always first in the list.

## useContacts
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches contacts and then partitions into highest priority (ie FUPO) and all others. The partition list is returned as an ordered set of key-value pairs.

## useDiningMenu
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches and returns the Dining Hall menu, partitioned based on meal and within each meal partitioned based on station. 

## useHealthSafetyLinks
**Returns:** *Same as `useDataLoadFetchCache`*
*To-Do: Rename method 

Returns all health and safety data, filtering to make sure only links, phone numbers, and emails are accepted.

## useImportantDates
**Returns:** 
<dl>
<dt>dates</dt>
<dd>Array: An array of arrays storying key-value pairs, where the key is the name of the category of dates, and the value is a list of dates within the category ordered chronologically.</dd>
</dl>

Returns an array of partitions of dates (partitioned on the basis of `category`), stored as key-value pairs ordered alphabetically by `category`. Within each partition, dates are ordered chronologically. Each entry's `date` is parsed into `Date` objects, and start and end times are parsed into an `HourRange` object stored as `timeRange`. 

## useImportantLinks
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches important links and other content, filters to ensure that only links, emails, and phone numbers are included, and returns the unaltered data from the web.

## useNewsArticles
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches all recent articles from the web, parses them into `Article` objects, then collates entries together if a single source has released pieces back-to-back in the news feed within several hours. For example, if The Paladin releases two pieces in 30 minutes, and no other news organization releases in the same period of time, these will be placed in a list together and added to the news feed combined together. The `data` state thus is an array of both `Articles` and arrays of `Articles`:

```js
console.log(data);
/*
 * [
 *  <Article>,
 *  <Article>,
 *  [<Article>, <Article>, <Article>],
 *  <Article>,
 * ]
 */
```

## useNewsPublishers
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches all publishers of campus news, and returns them as a list of key-value pairs where the key is the `publisherID` and the value is all other information about the publisher.

## useTransitLocations
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches current locations of vehicles, filtering to ensuring that the locations have been updated within the past 3 minutes, and then parsing the `latitude` and `longitude` into a `coordinate` and the `heading` as an integer. `data` is a list of objects representing vehicles with current positions.

## useTransitNames
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches information about each of the transit routes.

## useTransitStops
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches information about each stop, parsing integers, floats and times for positions, distances, headings, stops until arrival, and updated times, and assembling `latitude` and `longitude` into a `coordinate`. `data` is a list of these stops. 

## useWeatherReport
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches information about the current weather report.

## useWeatherWidgetImages
**Returns:** *Same as `useDataLoadFetchCache`*

Fetches a list of display images for the weather widget.