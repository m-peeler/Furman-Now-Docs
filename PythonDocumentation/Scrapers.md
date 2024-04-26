---
layout: default
title: Scrapers & DataClasses
nav_order: 5
parent: Python Documentation 
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# Scrapers & DataClasses
Various scrapers and dataclasses are used to collect information for the app. 

# Needing Attention
## dhmenu.py
*This scraper, which collects dining hall meals and is functional, is in the original state from the 2020 version of the project; it is in need of rewrite to conform with current scraper standards.*

## diningHours.py
*This scraper, which collects dining hall hours, is in the original state from the 2020 version of the project. It has been deprecated in favor of the `BonAppetitScraper`, though has not been removed because no potential for side effects from this removal been investigated.*

## eventsScraping.py
*This scraper, which collects CLPs and events from SyncDin and is functional, is in the original state from the 2020 version of the project; it is in need of rewrite to conform with current scraper standards.*

## ImportantDateScraper.py
*This scraper, which collects academic schedules from 25Live and is functional, has been modified and improved in 2024, but does not conform to the current standards of the project; it is in need of rewrite.*

# AthleticsScraper.py
## AthleticsEvent
*Arguments:*
<dl>
<dt>date</dt>
<dd>datetime: date of event</dd>
<dt>start</dt>
<dd>str: string representation of start time, or "All Day" if the event lasts all day.</dd>
<dt>sport</dt>
<dd>str: string name of sport</dd>
<dt>sportAbbrev</dt>
<dd>str: abbreviated name of sport</dd>
<dt>opponent</dt>
<dd>str: name of opponent.</dd>
<dt>locIndicator</dt>
<dd>str: character indication 'h' (home) or 'a' (away)</dd>
<dt>location</dt>
<dd>str: location of event</dd>
<dt>conference</dt>
<dd>bool: true if event is in-conference</dd>
<dt>noplayText</dt>
<dd>str: if game is cancelled, explination of why</dd>
<dt>resultStatus</dt>
<dd>str: character indicating win ('w'), loss ('l') or neither ('n')</dd>
<dt>resultFurScore</dt>
<dd>str: Furman's score</dd>
<dt>resultOppScore</dt>
<dd>str: Opponent's score</dd>
<dt>prescoreInfo</dt>
<dd>str: information before the game</dd>
<dt>postscoreInfo</dt>
<dd>str: information after the game</dd>
<dt>sportURL</dt>
<dd>str: url to the game's recap</dd>
</dl>

### insertInto
<dl>
<dt>table</dt>
<dd>str: name of table data is being inserted into</dd>
<dt>connection</dt>
<dd>pymysql.connection: connection to database that athletic event will be added to.</dd>
<dt>commit</dt>
<dd>bool: if true, automatically commits insert</dd>
</dl>

Inserts the `AthleticsEvent` into the database.

## AthleticsScraper
**Inherits from `Scraper`** 
### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all AthleticsEvents pulled</dd>
</dl>

### _processEvent
*Arguments:*
<dl>
<dt>event</dt>
<dd>dict: dictionary of raw result for athetics event from Furman Athletics API</dd>
</dl>

*Returns:*
<dl>
<dt>event</dt>
<dd>AthleticsEvent: parsed event for the game</dd>
</dl>

# HoursOpenScrapers.py

## TimesScraper (abstract base class) 
**Inherits from `Scraper`** \\
Base class for various scrapes that collect times.

### parseDaysFromRange
*Arguments:*
<dl>
<dt>dayRange</dt>
<dd>str: a string representing a range of days (eg 'Mon-Fri').</dd>
</dl>

*Returns:*
<dl>
<dt>dayList</dt>
<dd>list: a list with all days included in the day range.</dd>
</dl>

Turns a string range of days of the week into a list of the days of the week that it applies to.

### parseTimeOpened
*Arguments:*
<dl>
<dt>timeRanges</dt>
<dd>str: a string representing the range of times a building is opened, or several ranges of open time.</dd>
</dl>

*Returns:*
<dl>
<dt>times</dt>
<dd>list of TimeRange: a list with all TimeRanges that the provided time indicates the building will be opened.</dd>
</dl>

## TroneScraper
**Inherits from `TimesScraper`** \\
Parses open hours from the Trone Center's website for various shops inside Trone, primarily the P2X and Trone itself.

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all Schedules pulled for businesses inside of Trone</dd>
</dl>

### parseTroneTitle
*Arguments:*
<dl>
<dt>container</dt>
<dd>any: an HTML tag container</dd>
</dl>

*Returns:*
<dl>
<dt>title</dt>
<dd>str: name of the business whose information is in the container</dd>
</dl>

## EarleScraper
**Inherits from `TimesScraper`** \\
Scrapes times of operation for the Earle Health Center
### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all Schedules pulled for the Earle Health Center</dd>
</dl>

## PACScraper
**Inherits from `TimesScraper`** \\
Scrapes the times of operation for the PAC and the PAC's aquatics center.

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all Schedules pulled for the PAC</dd>
</dl>

### _parseTable
*Arguments:*
<dl>
<dt>table</dt>
<dd>any: parsed structure representing table of opened times at one facility.</dd>
</dl>

*Returns:*
<dl>
<dt>sched</dt>
<dd>Schedule: Schedule of times that the facility is open.</dd>
</dl>

### _parseRow
*Arguments:*
<dl>
<dt>row</dt>
<dd>any: parsed structure representing one row of the table of opened times at one facility.</dd>
<dt>sched</dt>
<dd>Schedule: Schedule that times from the row will be added to.</dd>
</dl>

## EnrollmentScraper 
**Inherits from `TimesScraper`** \\
Scrapes the times that Enrollment Services is opened. 

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all Schedules pulled for Enrollment Services</dd>
</dl>

## CounselingScraper 
**Inherits from `TimesScraper`** \\
Scrapes the times that the Counseling Center is opened.

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all Schedules pulled for the Counseling Center</dd>
</dl>

## BonAppetitScraper 
**Inherits from `TimesScraper`** \\
Scrapes the opened times from all of the Bon Appetit restaurants on campus.

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all Schedules pulled for Bon Appetit restaurants</dd>
</dl>

### _parseHours
*Arguments:*
<dl>
<dt>scheds</dt>
<dd>dict: dictionary of all business schedules</dd>
<dt>soup</dt>
<dd>BeautifulSoup: soup of the BonAppetit website.</dd>
<dt>dayOfWeek</dt>
<dd>string: Name of the day the current website is for.</dd>
</dl>

Given a website's `soup` and the `dayOfWeek`, parses it for opened hours for each of the Bon Appetit restaurants and updates the `scheds`

# LibrariesHoursScraper.py
## LibrariesScraper
**Inherits from `TimesScraper`** \\

Scrapes the opened hours for the libraries on campus, including the Duke Library, Science Library, Music Library and Special Collections/Archives. This makes use of the LibCal API.

### _getLastSunday
*Returns:*
<dl>
<dt>lastSun</dt>
<dd>datetime: date for the last Sunday that has occurred (including the current day)</dd>
</dl>

### _buildTimeRangeFromJSON
*Arguments:*
<dl>
<dt>jsonDict</dt>
<dd>dict: JSON dictionary of times that the library is opened</dd>
</dl>

*Returns:*
<dl>
<dt>ranges</dt>
<dd>list of TimeRange: time ranges that the library is open during</dd>
</dl>

Provided the time ranges from a single day in a `jsonDict` format to build the list of TimeRanges for its schedule.

### _buildLibraryScheduleFromJSON
*Arguments:*
<dl>
<dt>jsonDict</dt>
<dd>dict: JSON dictionary of times that the library is opened during some range of days</dd>
</dl>

*Returns:*
<dl>
<dt>sched</dt>
<dd>Schedule: opening schedule for library formed from jsonDict</dd>
</dl>

### _getJson
*Returns:*
<dl>
<dt>hoursJson</dt>
<dd>dict: json-based dictionary of opened hours for all campus libraries from the past Sunday to the next Saturday</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all Schedules pulled for campus libraries</dd>
</dl>

# WeatherScraper.py
## Forecast
**Inherits from `Clearable` and `Insertable`**
*Arguments:*
<dl>
<dt>idnum</dt>
<dd>int: ordered number for how close forecast is (1 is first, 2 is second, etc)</dd>
<dt>day</dt>
<dd>str: date</dd>
<dt>start</dt>
<dd>str: start time of forecast</dd>
<dt>end</dt>
<dd>str: end time of forecast</dd>
<dt>isDaytime</dt>
<dd>str: if it is daytime</dd>
<dt>currTemp</dt>
<dd>int: current temperature</dd>
<dt>highTemp</dt>
<dd>int: forecasted high temperature</dd>
<dt>lowTemp</dt>
<dd>int: forecasted low temperature</dd>
<dt>tempUnit</dt>
<dd>str: unit of temperature</dd>
<dt>precipPct</dt>
<dd>str: percent chance of precipitation</dd>
<dt>windSpeed</dt>
<dd>str: max forecasted wind speed</dd>
<dt>windDirection</dt>
<dd>str: Direction of wind</dd>
<dt>shortForecast</dt>
<dd>str: brief description of predicted weather</dd>
<dt>longForecast</dt>
<dd>str: longer verbal description of predicted weather</dd>
<dt>alert</dt>
<dd>str: weather-based alert</dd>
<dt>emoji</dt>
<dd>str: emoji describing weather conditions</dd>
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

## WeatherScraper
**Inherits from `Scraper`**
### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all weather forecasts</dd>
</dl>



