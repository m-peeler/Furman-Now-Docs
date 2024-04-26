---
layout: default
title: Transit Scrapers & DataClasses
nav_order: 7
parent: Python Documentation 
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# RouteScraper.py
## RouteScraper
**Inherits from `Scraper` and `Queriable`**\\
Scrapes a transit route and stores it internally.
*Arguments:*
<dl>
<dt>lineName</dt>
<dd>str: publically-displayed name of the route</dd>
<dt>lineIdentifier</dt>
<dd>str: name of route in systems being scraped from</dd>
<dt>idInTable</dt>
<dd>int: id number of route in the table</dd>
</dl>

### updateInto
*Arguments:*
<dl>
<dt>table</dt>
<dd>str: name of table to update into</dd>
<dt>connection</dt>
<dd>pymysql.connection: connection to database</dd>
<dt>commit</dt>
<dd>bool: if true, automatically commits the updating of the data</dd>
</dl>

### saveRouteToJSONFile
*Arguments:*
<dl>
<dt>filepath</dt>
<dd>str: path to file where json should be saved</dd>
</dl>

Creates json representation of current route and all `LinePoints` in it, and saves it to provided `filepath`

### loadRouteFromJSONFile
*Arguments:*
<dl>
<dt>filepath</dt>
<dd>str: path to file where json should be loaded from</dd>
</dl>

Loads json representation of a route and all `LinePoints` in it from `filepath`, and parses it into a route.

### distToStops
*Arguments:*
<dl>
<dt>vehic</dt>
<dd>Directioned: position and direction of vehicle which distance to stops is being measured for</dd>
</dl>

*Returns:*
<dl>
<dt>stopDists</dt>
<dd>list: list of key-value pairs, with key being the <tt>LineStop</tt> and value being the distance from the start to that stop.</dd>
</dl>


Calculates the distance from `vehic` to each of the `LineStops` in the current route.

### setStopsTable
*Arguments:*
<dl>
<dt>stopsTable</dt>
<dd>str: name of table where stops will be saved into</dd>
</dl>

## ShuttleRouteScraper
**Inherits from `RouteScraper`**

Scrapes the route of the Furman campus trolly.

### _getLineRoute
*Arguments:*
<dl>
<dt>page_json</dt>
<dd>dict: parsed json dictionary of shuttle website</dd>
</dl>

*Returns:*
<dl>
<dt>route</dt>
<dd>list of LinePoints: shuttle route parsed into LinePoints</dd>
</dl>

Finds all points in the route, then parses them into `LineStops` or `LinePoints` as is appropriate. Calculates distance from start and corrects heading, then returns the list of `LinePoints`.

### _getRouteNumber
*Returns:*
<dl>
<dt>routeID</dt>
<dd>any: the external website's internal number for the route</dd>
</dl>

Parses the Campus Shuttle ID page and finds the current shuttle's ID number based on its `lineIdentifier`.

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all pulled LinePoints and LineStops</dd>
</dl>

## BusRouteScraper
**Inherits from `RouteScraper`**

Scrapes the Greenlink website for the route of the specified bus.
### _getRouteSegs
*Arguments:*
<dl>
<dt>page_json</dt>
<dd>dict: parsed json dictionary of Greenlink website</dd>
</dl>

*Returns:*
<dl>
<dt>route</dt>
<dd>list of list of LinePoints: A list of all segments of the line, each of which is made up of a number of LinePoints.</dd>
</dl>

Finds all the partial segments of the route, and creates lists of each of the points that make them up.

### _segsToRoute
*Arguments:*
<dl>
<dt>segs</dt>
<dd>List of List of LinePoint: each of the segments of the Greenlink route, with the main route (assumedly the longest) first, and all additional segments progressing in an order such that the second segment starts closest to the main segment's end, and the last segment starts closes to the main segment's beginning, with each segment in between getting progressivley closer </dd>
</dl>

*Returns:*
<dl>
<dt>route</dt>
<dd>List of LinePoint: circuit of the route</dd>
</dl>

The Greenlink represents the 503 route as the main route, and then any deviations which occur on the return loop. This turns the route into a circuit loop by duplicating the main route and then 'stiching in' the additional spurs where it can.

### _getRouteSegs
*Arguments:*
<dl>
<dt>page_json</dt>
<dd>dict: parsed json dictionary of Greenlink website</dd>
</dl>

*Returns:*
<dl>
<dt>route</dt>
<dd>list of LineStops: A list of all stops in the line, unordered.</dd>
</dl>

Finds and returns all the stops on the route.

### _stopsIntoRoute
*Arguments:*
<dl>
<dt>route</dt>
<dd>list of LinePoint: list of all points in the route's loop, with the final point looping back to the first</dd>
<dt>stops</dt>
<dd>list of LineStop: unordered list of all the stops in the route</dd>
</dl>

*Returns:*
<dl>
<dt>route</dt>
<dd>list of LinePoints: A list of all LinePoints and LineStops in the route, in order.</dd>
</dl>

Takes each stop, orders them based on where they fall within the line route and which side of the road they are on, inserts them into the route, and returns the updated route.

### _getBusRoute
*Arguments:*
<dl>
<dt>page_json</dt>
<dd>dict: parsed json dictionary of Greenlink website</dd>
</dl>

*Returns:*
<dl>
<dt>route</dt>
<dd>list of LineStops: A list of all stops in the line, unordered.</dd>
</dl>

Assembles the bus route, calculates distances and headings between each point, ensures that the route starts with a `LineStop`, and returns the final route.

### _getBusID
*Arguments:*
<dl>
<dt>page_json</dt>
<dd>dict: parsed json dictionary of Greenlink website</dd>
</dl>

*Returns:*
<dl>
<dt>lineID</dt>
<dd>int: the numeric identification number of the vehicle that drives the route within the external system</dd>
</dl>

Determines what the vehicle ID is for the bus that is driving the current route, based on `lineIdentifier`. 

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all pulled LinePoints and LineStops</dd>
</dl>

Pulls, assembles, orders, and standardizes the route.

# VehicleScraper

## Vehicle
**Inherits from `Insertable` and `Directioned`**

*Arguments:*
<dl>
<dt>lat</dt>
<dd>float: latitude</dd>
<dt>lon</dt>
<dd>float: longitude</dd>
<dt>heading</dt>
<dd>int: compass heading</dd>
<dt>name</dt>
<dd>str: name of vehicle</dd>
<dt>speed</dt>
<dd>float: speed of vehicle</dd>
<dt>nextStopDist</dt>
<dd>float: distance from current position to next stop, assuming the route is followed</dd>
<dt>nextStopID</dt>
<dd>int: stop ID number of the next stop that the vehicle will arrive at</dd>
</dl>

### \_\_post_init\_\_
Saves the time so as to know when the scraping last occurred. 

### updateInto
*Arguments:*
<dl>
<dt>table</dt>
<dd>str: name of table to update into</dd>
<dt>connection</dt>
<dd>pymysql.connection: connection to database</dd>
<dt>commit</dt>
<dd>bool: if true, automatically commits the updating of the data</dd>
</dl>

### insertInto
*Arguments:*
<dl>
<dt>table</dt>
<dd>str: name of table to insert into</dd>
<dt>connection</dt>
<dd>pymysql.connection: connection to database</dd>
<dt>commit</dt>
<dd>bool: if true, automatically commits the clearing of the data</dd>
</dl>

## ShuttleScraper
**Inherits from `Scraper`**

Scrapes the current locations for the Furman campus shuttle.

### _parseVehicle
*Arguments:*
<dl>
<dt>jsonDct</dt>
<dd>dict: parsed json representation of the shuttle</dd>
</dl>

*Returns:*
<dl>
<dt>vehic</dt>
<dd>Vehicle: Vehicle constructed from information in json dictionary</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of pulled campus shuttle Vehicles</dd>
</dl>

## BusScraper
**Inherits from `Scraper`**
Scrapes the current locations for the Greenlink bus whose ID number is provided as `busID` on initializaiton.

*Arguments:*
<dl>
<dt>busID</dt>
<dd>int: id of desired bus in Greenlink system</dd>
<dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of pulled campus shuttle Vehicles whose busID match the value privided in initialization.</dd>
</dl>
