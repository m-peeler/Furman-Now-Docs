---
layout: default
title: Position Classes
nav_order: 3
parent: Python Documentation 
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# PositionClasses.py
These clases are used for elements positioned in the world, primarily transit vehicles and their stops.
## Positioned
*Arguments:*
<dl>
<dt>lat</dt>
<dd>float: latitude coordinate</dd>
<dt>lon</dt>
<dd>float: longitude coordinate</dd>
</dl>

### distBetween
*Arguments:*
<dl>
<dt>first</dt>
<dd>Positioned</dd>
<dt>second</dt>
<dd>Positioned</dd>
</dl>

*Returns:*
<dl>
<dt>distance</dt>
<dd>float</dd>
</dl>

Calculates the distance between two `Positioned` items, in miles.

### headingBetween
*Arguments:*
<dl>
<dt>first</dt>
<dd>Positioned</dd>
<dt>second</dt>
<dd>Positioned</dd>
</dl>

*Returns:*
<dl>
<dt>heading</dt>
<dd>int</dd>
</dl>
Calculates the heading/bearing from the first `Positioned` to the second `Positioned`, in degrees, floored to the nearest int.

## Directioned
*Arguments:*
<dl>
<dt>lat</dt>
<dd>float: latitude coordinate</dd>
<dt>lon</dt>
<dd>float: longitude coordinate</dd>
<dt>heading</dt>
<dd>int: compass heading of object</dd>
</dl>

### isRightOf
*Arguments:*
<dl>
<dt>self</dt>
<dd>Directioned</dd>
<dt>other</dt>
<dd>Directioned</dd>
</dl>

*Returns:*
<dl>
<dt>isRight</dt>
<dd>bool: Is self to the right of other?</dd>
</dl>

### isBetweenAndRight
*Arguments:*
<dl>
<dt>self</dt>
<dd>Directioned</dd>
<dt>first</dt>
<dd>Directioned: earlier point</dd>
<dt>second</dt>
<dd>Directioned: later point</dd>
</dl>

*Returns:*
<dl>
<dt>isRight</dt>
<dd>bool: Is self to the right of other?</dd>
</dl>

Checks if `self` is a point that, if you were traveling from the first point to the second point, would at some point be on your right.

# RouteScraper.py
## LinePoint
**Inherits from `Directioned`**

Represents a single point within a line on a route. 

*Arguments:*
<dl>
<dt>orderID</dt>
<dd>int: position in the order of the line</dd>
<dt>lat</dt>
<dd>float: latitude</dd>
<dt>lon</dt>
<dd>float: longitude</dd>
<dt>lineTableID</dt>
<dd>int: ID of route/bus line within the database table</dd>
<dt>isStop</dt>
<dd>bool: if true, the LinePoint represents a bus stop; defaults to false.</dd>
<dt>heading</dt>
<dd>int: direction / compass heading that vehicle would have if traveling through this point on the route.</dd>
<dt>distance</dt>
<dd>float: distance from the starting stop to this point.</dd>
</dl>

### correctHeading
*Arguments:*
<dl>
<dt>after</dt>
<dd>Positioned: the point after this LinePoint in line</dd>
</dl>

Calculates the heading if you are moving from the `LinePoint` to `after` and sets the `LinePoint`'s heading to this value.

### distFromStart
*Arguments:*
<dl>
<dt>before</dt>
<dd>Positioned: the point before this LinePoint in line</dd>
</dl>

Calculates the distance from the start of the route to the current point by calculating the distance to the `before` point and adding this to the `before` point's distance to the start.

### toJSONdict
*Returns:*
<dl>
<dt>jsonDict</dt>
<dd>str: String representation of a json dictionary of the current LinePoint</dd>
</dl>

### fromJSONdict
*Arguments:*
<dl>
<dt>dct</dt>
<dd>dict: dictionary parse of a JSON representation of a LinePoint</dd>
</dl>

*Returns:*
<dl>
<dt>point</dt>
<dd>LinePoint: a parsed LinePoint from the data in the JSON dict</dd>
</dl>

## LineStop
**Inherits from `LinePoint`, `Insertable`, `Clearable`**
Represents a stop on a route. 

**NOTE: `clearFrom` and `insertInto` are not current implemented**

*Arguments:*
<dl>
<dt>orderID</dt>
<dd>int: position in the order of the line</dd>
<dt>lat</dt>
<dd>float: latitude</dd>
<dt>lon</dt>
<dd>float: longitude</dd>
<dt>lineTableID</dt>
<dd>int: ID of route/bus line within the database table</dd>
<dt>stopName</dt>
<dd>str: name of stop on the line.</dd>
<dt>stopOrderID</dt>
<dd>int: position of stops in the order of the route.</dd>
<dt>heading</dt>
<dd>int: heading of a vehicle on the route at the stop; defaults to None.</dd>
<dt>distance</dt>
<dd>float: distance from the start of the route to this stop; defaults to None.</dd>
</dl>

### toJSONdict
*Returns:*
<dl>
<dt>jsonDict</dt>
<dd>str: String representation of a json dictionary of the current LineStop</dd>
</dl>

### fromJSONdict
*Arguments:*
<dl>
<dt>dct</dt>
<dd>dict: dictionary parse of a JSON representation of a LineStop</dd>
</dl>

*Returns:*
<dl>
<dt>point</dt>
<dd>LinePoint: a parsed LineStop from the data in the JSON dict</dd>
</dl>

### clearFrom
*Arguments:*
<dl>
<dt>table</dt>
<dd>str: name of table to clear from</dd>
<dt>connection</dt>
<dd>pymysql.connection: connection to database</dd>
<dt>commit</dt>
<dd>bool: if true, automatically commits the clearing of the data</dd>
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