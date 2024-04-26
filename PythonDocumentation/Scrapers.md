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
**Inherits from `Scraper`** \\

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

# NewsScrapers.py

## Article
**Inherits from `Insertable`** \\
*Arguments:*
<dl>
<dt>title</dt>
<dd>str: title of article</dd>
<dt>author</dt>
<dd>str: author of article</dd>
<dt>description</dt>
<dd>str: description of article</dd>
<dt>mediatype</dt>
<dd>str: media type of article, link or video</dd>
<dt>link</dt>
<dd>str: link to article</dd>
<dt>publisherID</dt>
<dd>int: id of the news source / publisher of the article</dd>
<dt>section</dt>
<dd>str: optional section name for article</dd>
<dt>publishDate</dt>
<dd>datetime: optional date that the article was published</dd>
<dt>imagelink</dt>
<dd>str: optional link to header image for the article </dd>
</dl>

### insertInto
*Arguments:*
<dl>
<dt>table</dt>
<dd>str: name of table article is being inserted into</dd>
<dt>connection</dt>
<dd>pymysql.connection: connection to the database</dd>
<dt>commit</dt>
<dd>bool: if true, automatically commits the insertion</dd>
</dl>

Inserts the article into the database.

### structTimeToDatetime
*Arguments:*
<dl>
<dt>st_tm</dt>
<dd>struct_time: datetime in the struct_time format</dd>
</dl>

*Returns:*
<dl>
<dt>dt_tm</dt>
<dd>datetime: datetime converted into datetime format</dd>
</dl>

### \_\_lt\_\_
*Arguments:*
<dl>
<dt>other</dt>
<dd>Article: a second article</dd>
</dl>

*Returns:*
<dl>
<dt>less_than</dt>
<dd>bool: whether the object's publish date is less than the other's publish date.</dd>
</dl>

## NewsScraper
**Inherits from `Scraper`** \\
### getTableID (abstract method)
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of news source in database tables</dd>
</dl>

### youTubeFilterForVideos
*Arguments:*
<dl>
<dt>req</dt>
<dd>requests.response: response from request to YouTube API request</dd>
</dl>

*Returns:*
<dl>
<dt>entries</dt>
<dd>list: the request response filtered to only include the entries which are video posts (i.e. 'uploads')</dd>
</dl>

### parseYouTubeToArticle
*Arguments:*
<dl>
<dt>entry</dt>
<dd>any: single-video entry from the YouTube API's response </dd>
<dt>authName</dt>
<dd>str: name of the video's author</dd>
<dt>tableID</dt>
<dd>int: id of the news publisher </dd>
<dt>section</dt>
<dd>str: optional section name for video; defaults to None</dd>
</dl>

*Returns:*
<dl>
<dt>video</dt>
<dd>Article: the provided video parsed into an Article format</dd>
</dl>

### getPDFintoPNG
*Arguments:*
<dl>
<dt>source</dt>
<dd>str: weblink of PDF to convert into PNG </dd>
<dt>fileName</dt>
<dd>str: name of desired file/file path within the '~/www/FUNow/articleImages/' directory.</dd>
</dl>

*Returns:*
<dl>
<dt>imageLink</dt>
<dd>str: public link on the cs.furman.edu website for the converted image.</dd>
</dl>

## ChristoScraper
**Inherits from `NewsScraper`** \\

Scrapes articles from the Christo et Doctrinae website. 

### getTableID (abstract method)
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of Christo et Doctrinae in database tables</dd>
</dl>

### getImage
*Arguments:*
<dl>
<dt>entry</dt>
<dd>any: single article entry from Christo RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>link</dt>
<dd>str: url to article's header image</dd>
</dl>

### getImage
*Arguments:*
<dl>
<dt>description</dt>
<dd>str: description from Christo article</dd>
</dl>

*Returns:*
<dl>
<dt>description</dt>
<dd>str: cleaned description</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all Christo et Doctrinae Articles</dd>
</dl>