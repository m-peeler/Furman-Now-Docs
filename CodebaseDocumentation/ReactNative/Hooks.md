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
<dd>Anonymous function: Provided with the result after processFetch has been called on the cached data. If it returns true, the cache will be deleted, and its value will not be used in the app. Defaults to never discard cache.</dd>
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
<dd>Boolean (state): Indicates whether there has been a successful fetch or load yet; if true, `data` has information within it.</dd>
<dt>refresh</dt>
<dd>Anonymous Function: Invokable to re-fetch data from the provided.</dd>
</dl>

`useDataLoadFetchCache` does three things: it loads the last-recieved result from the asynchronous storage cache, it fetches a new result from a specified website, and it caches the result the fetch is successful. Newly fetched data will replace cached data when it is recieved. 

Since loading from cache and fetching from web are both asynchronous, but the former tends to be faster, both are called. Once cache has been accessed, cached data is provided in the `data` state until fetched data has been recieved.

Every other custom hook in Furman Now! is effectively a wrapper for `useDataLoadFetchCache`, providing specific parameters to the function to pull information from a specified site and process it in the intended way.

## useAthleticsCalendar
**Returns:**
*Same as `useDataLoadFetchCache`*
<dl>
<dt>data</dt>
<dd>String || Object: Either a string heading, or an object with data for an event. Event data is provided unchanged from the server pull, with the exception of `eventdate `which is parsed into a `Date` object, and `allDay`, which is a boolean if the time of `eventdate` is midnight.</dd>
</dl>

Provides a list of either string headings or objects representing recent and upcoming athletics events. Events are fetched from the server and partitioned into either `Recent` (if they have already finished), `Today`, `Tomorrow`, `This`(ie This Week) and `Next` (ie Next Week) using `arrayPartition`. Events within each partition are 