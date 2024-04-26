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
<dd>bool: if true, automatically commits the insertion of the data</dd>
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

