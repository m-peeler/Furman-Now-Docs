---
layout: default
title: Time Classes
nav_order: 4
parent: Python Documentation 
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# Time Classes
## Time Range
*Arguments:*
<dl>
<dt>opening</dt>
<dd>datetime: time that the TimeRange begins and the shift opens</dd>
<dt>closing</dt>
<dd>str: time that the TimeRange ends and the shift closes</dd>
</dl>

Represents a range of time using an `opening` and `closing` datetime; can also represent a time when a location is `Closed` all day, and when a scraper `Failed` to scrape a valid time range.

*Attributes:*
<dl>
<dt>opn</dt>
<dd>datetime: opening time</dd>
<dt>close</dt>
<dd>datetime: closing time</dd>
</dl>

### \_\_str\_\_
*Returns:*
<dl>
<dt>timeRangeString</dt>
<dd>str: represents time range as a string</dd>
</dl>

### \_\_repr\_\_
*Returns:*
<dl>
<dt>timeRangeRepresentation</dt>
<dd>str: string represent of the current object</dd>
</dl>

### \_\_eq\_\_
*Arguments:*
<dl>
<dt>othr</dt>
<dd>TimeRange: a second time range to compare against</dd>
</dl>

*Returns:*
<dl>
<dt>areEqual</dt>
<dd>boolean: boolean indicating if the two time ranges' opening and closing are each <tt>_timeEquals</tt>.</dd>
</dl>

### _timeEquals
*Arguments:*
<dl>
<dt>first</dt>
<dd>datetime: a first datetime</dd>
<dt>second</dt>
<dd>datetime: a second datetime</dd>
</dl>

*Returns:*
<dl>
<dt>areEqual</dt>
<dd>boolean: the two datetimes have the same hours and minutes values.</dd>
</dl>

### openingStr

*Returns:*
<dl>
<dt>opening</dt>
<dd>str: string representation of the opening time.</dd>
</dl>

### closingStr

*Returns:*
<dl>
<dt>closing</dt>
<dd>str: string representation of the closing time.</dd>
</dl>

### Closed

*Returns:*
<dl>
<dt>Closed</dt>
<dd>TimeRange: returns an instance of a Closed <tt>TimeRange</tt>.</dd>
</dl>

### Failed

*Returns:*
<dl>
<dt>Failed</dt>
<dd>TimeRange: returns an instance of a Failed <tt>TimeRange</tt>.</dd>
</dl>

### isClosed

*Returns:*
<dl>
<dt>isClosed</dt>
<dd>boolean: returns true if the instance is an instance of Closed.</dd>
</dl>

### isFailed

*Returns:*
<dl>
<dt>isFailed</dt>
<dd>boolean: returns true if the instance is an instance of Failed.</dd>
</dl>


## Schedule
*Arguments:*
<dl>
<dt>name</dt>
<dd>str: name of building schedule is for</dd>
</dl>

Holds an open-closed schedule. Each schedule can store various "time periods" with different names, when different hours are applicable; the default period is "Regular Operation".

### \_\_post_init\_\_
Initializes a default schedule once the `dataclass` values are all initialized. 

### _emptyTimePeriod

*Returns:*
<dl>
<dt>emptyTimePeriod</dt>
<dd>dict: dictionary representing a default time period, where the schedule is closed every day..</dd>
</dl>

### _timePeriodStr
*Arguments:*
<dl>
<dt>dct</dt>
<dd>dict: dictionary representing a time period</dd>
</dl>

*Returns:*
<dl>
<dt>stringRep</dt>
<dd>str: representation of the timePeriod as a string</dd>
</dl>

### \_\_repr\_\_
*Returns:*
<dl>
<dt>stringRep</dt>
<dd>str: representation of the Schedule as a string</dd>
</dl>

### \_\_str\_\_
*Returns:*
<dl>
<dt>schedString</dt>
<dd>str: string of the Schedule</dd>
</dl>

### dayNameOf [static]
*Arguments:*
<dl>
<dt>day</dt>
<dd>str: string of a day name or some form of abbreviation for the day.</dd>
</dl>

*Returns:*
<dl>
<dt>day</dt>
<dd>str: standardized full name of the input day, or None if the abbreviation does not match any known ones.</dd>
</dl>

### noFails
*Returns:*
<dl>
<dt>noFails</dt>
<dd>boolean: true if no TimeRanges in the Schedule are Failed.</dd>
</dl>

### addDayRangeTime
*Arguments:*
<dl>
<dt>days</dt>
<dd>list or str: single, or list of, string of standardized, full-length day names that <tt>ranges</tt> will be added to.</dd>
<dt>ranges</dt>
<dd>list or TimeRange: single, or list of,TimeRanges that schedule will be open during on days in <tt>days</tt>.</dd>
</dl>

### _updatePeriodSchedule
*Arguments:*
<dl>
<dt>cursor</dt>
<dd>pymysql.cursors.Cursor: cursor used to add Schedule to database</dd>
<dt>insertTable</dt>
<dd>str: name of table data will be inserted into.</dd>
<dt>buildingID</dt>
<dd>str or int: id number of building Schedule is for.</dd>
<dt>sched</dt>
<dd>dict: timeperiod dictionary with day name as key and a list of TimeRanges when the building is open as value.</dd>
<dt>period</dt>
<dd>str: name of time period.</dd>
</dl>

Using the `cursor`, inserts the provided `sched` for the `period` into the `insertTable`, using `buildingID` to attach it to its table.

**Note**: Currently, the function does not clear old schedules for the same building ID, nor does it have a field to differentiate `period` in the table, meaning that only the last-provided schedule is saved.

### selectBuildingIDFrom
*Arguments:*
<dl>
<dt>namesIDTable</dt>
<dd>str: name of table in database that building ID will be drawn from</dd>
<dt>cursor</dt>
<dd>pymysql.cursors.Cursor: cursor used to query building ID from database</dd>
</dl>

*Returns:*
<dl>
<dt>buildingID</dt>
<dd>int: id number of schedule's building in thedatabase</dd>
</dl>

Using the `cursor`, selects the `self.name`'s `buildingID` from `namesIDTable` and returns it for use in inserting.

### updateInto
*Arguments:*
<dl>
<dt>insertTable</dt>
<dd>str: table to insert the information into</dd>
<dt>buildingIDTable</dt>
<dd>str: id of the table that connects building name with id</dd>
<dt>connection</dt>
<dd>pymysql.connection: connection used to insert data into table</dd>
<dt>onlyMainSchedule</dt>
<dd>bool: if true, only inserts the main schedule into the database. Defaults to true.</dd>
</dl>

Using `connection`, finds the `Schedule`'s `buildingID` from the `buildingIDTable`, clears all old schedules with that `buildingID` from the `insertTable`, and updates new hours; if `onlyMainSchedule` is true, then only the `Schedule._defaultPeriod` schedule will be inserted.

## Event
*Arguments:*
<dl>
<dt>title</dt>
<dd>str: name of the event</dd>
<dt>date</dt>
<dd>datetime: date of the event</dd>
<dt>timeRange</dt>
<dd>TimeRange: time that the event runs</dd>
<dt>description</dt>
<dd>str: description of the event</dd>
<dt>category</dt>
<dd>str: category of events / type of calendar that this event falls under</dd>
<dt>term</dt>
<dd>str: which academic term the event occurs during</dd>
</dl>

Models an on-campus event.

### \_\_str\_\_
*Returns:*
<dl>
<dt>string</dt>
<dd>str: string representation of the event</dd>
</dl>

### insertInto
<dl>
<dt>table</dt>
<dd>str: name of the table event is being inserted into</dd>
<dt>connection</dt>
<dd>pymysql.connection: connection to connect with database</dd>
<dt>commit</dt>
<dd>bool: if true, automatically commits queries to database</dd>
</dl>

Inserts the `Event`'s data into the database connected to by `connection` in the `table` provided. Commits insertion if `commit` is true.