---
layout: default
title: Utilities
nav_order: 5
parent: React Native Documentation
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# Utilities

## Array Functions
### arrayPartition
*Arguments:*
<dl>
<dt>array</dt>
<dd>Array: an array of objects</dd>
<dt>partitionOn</dt>
<dd>String or Function: Either a string that corresponds to a key in each element of the <tt>array</tt>, or a callback function that when provided with an element from <tt>array</tt> returns the category that it should be sorted into.</dd>
</dl>

Splits an array into a series of arrays containing a key-value pairs on the basis of the `partitionOn` field/return for each element. If `partitionOn` is a string, `array[0][partitionOn]` will become the key for the first key-value pair, and the value will be a list of all elements in `array` that have the same value for `array[n][partitionOn]`. If `partitionOn` is a function, elements will similarly be group based on equivalent `partitionOn(array[n])` values. 

```js
const partition = arrayPartition(
    [{name: 'alice', grade: 'senior'},
     {name: 'bob', grade: 'senior'},
     {name: 'charlie', grade: 'junior'}],
    'grade'
);

console.log(partition);
/*
 * [['senior', 
     [{name: 'alice', grade: 'senior'},
      {name: 'bob', grade: 'senior'}]
    ],
    ['junior',
     [{name: 'charlie', grade: 'junior'}]
    ]]
 */
```

## Article Functions
### MediaTypes
An enum of differnt types of article that can be made. `VIDEO` is a YouTube video, `LINK` is a URL.

### Article
*Arguments:*
<dl>
<dt>title</dt>
<dd>String: article headline</dd>
<dt>link</dt>
<dd>String: link to article</dd>
<dt>date</dt>
<dd>Date: publication date</dd>
<dt>publisherID</dt>
<dd>String: id for publication</dd>
<dt>media</dt>
<dd>MediaType: a string representing the type of media the <tt>Article</tt> is storing.</dd>
<dt>author</dt>
<dd>String: author name</dd>
<dt>section</dt>
<dd>String: optional section within publication</dd>
<dt>imagelink</dt>
<dd>String: optional image for the article's display</dd>
<dt>description</dt>
<dd>String: optional description of the article</dd>
</dl>

A dataclass representing a single news article. Stores a `title`, a `link` to the content, the `date` of publication, the `publisherID` of its publisher, a `media` type equal to the value of a `MediaType` enum, an `author` for the piece, an optional `section` of the publication that the article is published in, an `imageLink` that will be displayed for the image, and a `description` of the article like a deck.

## Contact Functions
### formatPhoneNumber
*Arguments:*
<dl>
<dt>phone</dt>
<dd>String: a 10-digit phone number with no additional formatting.</dd>
</dl>

*Returns:*
<dl>
<dt>phoneNumber</dt>
<dd>String: a phone number in the form (###) ###-####</dd>
</dl>

Formats a phone number into the desired formatting for better display.

### Contact
*Arguments:*
<dl>
<dt>name</dt>
<dd>String: contact's name</dd>
<dt>content</dt>
<dd>object: 
    <dl>
    <dt>email</dt>
    <dd>String: optional email address for contact</dd>
    <dt>phone</dt>
    <dd>Number: optional 10-digit American phone number</dd> 
    </dl>
</dd>
<dt>company</dt>
<dd>String: contact's company; default value is 'Furman University'</dd>

A class that stores a person's contact information, including their `name`, either an `email` address or a numeric phone `number`, and optionally a `company` they work for. 

### InsertableContact
*Arguments:*
<dl>
<dt>contact</dt>
<dd>Contact: a Contact whose information will be used in the InsertableContact</dd>
</dl>

Implementation of `NativeContact.Contact` interface from `expo-contacts`, which allows the `Contact` to be saved to the device's contacts.

### saveContact
*Arguments:*
<dl>
<dt>contact</dt>
<dd>Contact: a contact being saved to the contacts book</dd>
</dl>

If the app has the correct permissions, saves `contact` into the contact book.

### requestAddAlert
*Arguments:*
<dl>
<dt>contact</dt>
<dd>Contact: a contact the user is being asked if they would like to save into their contacts book</dd>
</dl>

An alert that asks the user if they would like to save the `contact` to their contact book. If the user approves, calls the `saveContact` function with the provided `contact`. 

## DateTimeFunctions
### parseDate
*Arguments:*
<dl>
<dt>date</dt>
<dd>String: a date of the format <tt>YYYY-MM-DD</tt></dd>
</dl>

*Returns:*
<dl>
<dt>date</dt>
<dd>Date: a parsed version of the provided date.</dd>
</dl>

Parses a provided date into a `Date` object.

### parseTime
*Arguments:*
<dl>
<dt>time</dt>
<dd>String: a time of the format <tt>HH:mm:ss</tt></dd>
</dl>

*Returns:*
<dl>
<dt>time</dt>
<dd>Date: a parsed version of the provided time.</dd>
</dl>

Parses a provided time into a `Date` object.

### parseDatetime
*Arguments:*
<dl>
<dt>datetime</dt>
<dd>String: a time of the format <tt>YYYY-MM-DD HH:mm:ss</tt></dd>
</dl>

*Returns:*
<dl>
<dt>datetime</dt>
<dd>Date: a parsed version of the provided datetime.</dd>
</dl>

Parses a provided string containing both a date and a time into a `Date` object.

### isAllDay
*Arguments:*
<dl>
<dt>datetime</dt>
<dd>Date: a date and time for an event</tt></dd>
</dl>

*Returns:*
<dl>
<dt>isAllDay</dt>
<dd>bool: boolean indicating if the time of the <tt>Date</tt> is midnight, and the event should be assumed to last all day.</dd>
</dl>

If an event starts at midnight, it is assumed to last all day, and `true` is returned.

### getDateSuffix
*Arguments:*
<dl>
<dt>date</dt>
<dd>Date: a date</tt></dd>
</dl>

*Returns:*
<dl>
<dt>suffix</dt>
<dd>String: 'st', 'th', 'nd' and 'rd', as appropriate for the number of the event's day.</dd>
</dl>

### directToSettings
Informs the user that Furman Now! does not have access to edit their calendar and directs them to change the value in settings if they wish to allow them to be saved.

### getDefaultCalendarSource
*Returns:*
<dl>
<dt>source</dt>
<dd>Calendar.Source: the source on the system's default calendar, required for Calendar.Calendar implementation.</dd>
</dl>

### Cal
*Arguments:*
<dl>
<dt>title</dt>
<dd>String: title of the calendar</dd>
<dt>source</dt>
<dd>Calendar.Source: source of the calendar</dd>
<dt>sourceId</dt>
<dd>String: optional id for the calendar</dd>
</dl>

Implementation of `Calendar.Calendar` from `expo-calendar`, allowing the creation of a calendar on the system. 

### createFUNowCalendar
*Arguments:*
<dl>
<dt>calendarTitle</dt>
<dd>String: title of the calendar created</dd>
</dl>

*Returns:*
<dl>
<dt>calendarID</dt>
<dd>String: system-generated ID of the created calendar.</dd>
</dl>

Creates a calendar on the system with a title of `calendarTitle` if the app has the permissions to do so. 

### findCalendarByTitle
*Arguments:*
<dl>
<dt>calendarTitle</dt>
<dd>String: title of the calendar being searched for</dd>
</dl>

*Returns:*
<dl>
<dt>calendarID</dt>
<dd>String: system ID of the calendar with the name provided</dd>
</dl>

Searches for a calendar with th eprovided `calendarTitle` and returns its `calendarId`. If no calendar exists with the `calendarTitle`, a new one is created and its `calendarId` is returned.

### Status
Status type indicating whether or not the app has permission to add to the calendar.

### addToCalendar
*Arguments:*
<dl>
<dt>event</dt>
<dd>Event: event being added to the calendar</dd>
<dt>status</dt>
<dd>Status: current permissions of whether or not the calendar can be edited.</dd>
<dt>requestPermissions</dt>
<dd>Function: callback which requests the permission to edit the calendar</dd>
<dt>calendarName</dt>
<dd>String: name/title of the calendar being added to</dd>
</dl>

### Event
Dataclass storing information about a specific event.

### requestAddEvent
*Arguments:*
<dl>
<dt>event</dt>
<dd>Event: event user is being requested if they would like to add</dd>
<dt>status</dt>
<dd>Status: current permissions of whether or not the calendar can be edited.</dd>
<dt>requestPermissions</dt>
<dd>Function: callback which requests the permission to edit the calendar</dd>
</dl>

### basicStringDate
*Arguments:*
<dl>
<dt>date</dt>
<dd>Date: date string is being created for</dd>
</dl>

Creates string representation of `date` in the format `January 1st, 1970`.

## Page
The `Page` class stores information for a page that needs to be generated in `navigator.jsx`. Pages are ordered by `id`, traveled to using `name`, represented on `HomeScreenNavButton` by `icon`, part of the `category` provided, and can be specified to show their name or not using a boolean of `showName`. 

## Scheduling
### DaysOfWeek
An enum of the days of the week. Strings are represented in title case, enum names in all capitals.

### Schedule
Object tracking weekly hours of operation.

#### DAYORDER [static]
A list of the `DaysOfWeek` in order, starting on `SUNDAY`.

#### dayToNum [static]
Turns a `DaysOfWeek` into its position in the week, with `SUNDAY` equal to 0.

#### getDOWFromString [static]
Converts a string of the name of a day of the week into a `DaysOfWeek` enum.

#### short [static]
Converts a `DaysOfWeek` enum into a short version of the name in English, eg. `WEDNESDAY` becomes 'Wed.'.

#### getDOWFromDate [static]
Takes as input a `Date` and returns the `DaysOfWeek` day that corresponds to the day of the week the date represents.

#### addHourRangeToDay
*Arguments:*
<dl>
<dt>day</dt>
<dd>DaysOfWeek: day that will have hours applied to it</dd>
<dt>hourRange</dt>
<dd>HourRange: time that the schedule will be open during</dd>
</dl>

Stores in the schedule that the location will be open on `day` during the duration of `hourRange`.

#### makeHoursString
*Arguments:*
<dl>
<dt>day</dt>
<dd>DaysOfWeek: day that will have hours applied to it</dd>
</dl>

*Returns:*
<dl>
<dt>hoursString</dt>
<dd>String: String representing hours of operation on the provided day, or closed if the schedule is never open that day.</dd>
</dl>

Returns a string showing what the hours of operation will be on the provided `day`.

#### isOpened
*Arguments:*
<dl>
<dt>time</dt>
<dd>Date: time that the user wants to know if the building will be opened</dd>
</dl>

*Returns:*
<dl>
<dt>isOpened</dt>
<dd>Boolean: indicates if schedule shows building will be open during the time provided.</dd>
</dl>

#### isClosingWithin
*Arguments:*
<dl>
<dt>time</dt>
<dd>Date: time that the user wants to know about</dd>
<dt>minsWithin</dt>
<dd>number: Checks if closing will occur within this many minutes of the time provided</dd>
</dl>

*Returns:*
<dl>
<dt>isClosingWithin</dt>
<dd>Boolean: indicates if schedule shows building will be closing at some point within the timerange requested.</dd>
</dl>

#### dailySchedules
*Arguments:*
<dl>
<dt>onlyToday</dt>
<dd>Boolean: true if the user only ways the current day's schedule</dd>
</dl>

*Returns:*
<dl>
<dt>schedules</dt>
<dd>Array: a list of arrays that are key-value pairs, with the key being the day's name and the value being the schedule string generated by <tt>makeHoursString</tt> for the day; if successive days have the same schedules, the key will instead show which range of days the schedule is applicable for.</dd>
</dl>

Returns a list of strings of hours of operation for all days of the week, or for the current day if `onlyToday` is set to true.

### timeWithinMinutes
*Arguments:*
<dl>
<dt>first</dt>
<dd>Date: Earlier time</dd>
<dt>second</dt>
<dd>number: Later time</dd>
<dt>mins</dt>
<dd>Number: number of minutes that the two times should be within</dd>
</dl>

*Returns:*
<dl>
<dt>within</dt>
<dd>boolean: true if the times are within the minute length of each other.</dd>
</dl>

Checks if `second` will occur no more than `mins` minutes after `first`, regardless of date of `second` or `first` (If `first` is 2:00 am on Jan 1 1970, `second` is 2:15 am on June 15 2030, and `mins` is 30, the return will be `true`, as date is ignored). 23:45 and 0:15 are similarly considered within 30 minutes of eachother.

### timeSubtractionMinutes
*Arguments:*
<dl>
<dt>first</dt>
<dd>Date: Later time</dd>
<dt>second</dt>
<dd>number: Earlier time</dd>
</dl>

*Returns:*
<dl>
<dt>minutes</dt>
<dd>number: number of minutes that first is after second; 02:15 - 01:15 is 60, as is 00:15 - 23:15.</dd>
</dl>

Subtracts `first` from `second` (ignoring date) and returns the number of minutes between the two. If `first` is earlier than `second`, `second` is assumed to have occured on the previous day.

### HourRange
Class representing a range of time with a start and an end. If the `start` time is after the `end` time (checkable with `rangeIsOrdered`), the end time is assumed to be on the next day. Several utility methods are included, including `isInRange` which checks if a `time` falls within the range, `mergeRange` which merges a second ranges that intersect with the current one into the time of the current range, and `formatStartEnd` which formats the time range into a displayable form. `hoursToAm`, `hoursToStr` and `formatTimeNums` are static methods that inform whether a provided `time` is 'am' or 'pm', convert military time into the standard 1-12 range, and turn a `time` into a standard 'HH:mm' format, respectively.

### datetimeCompare
*Arguments:*
<dl>
<dt>first</dt>
<dd>Date: First datetime</dd>
<dt>second</dt>
<dd>number: Second datetime</dd>
</dl>

*Returns:*
<dl>
<dt>comparison</dt>
<dd>number: 0 if first and second are the same date and time, 1 if first is a later date and time than second, -1 if it is an earlier date and time.</dd>
</dl>


### timeCompare
*Arguments:*
<dl>
<dt>first</dt>
<dd>Date: First time</dd>
<dt>second</dt>
<dd>number: Second time</dd>
</dl>

*Returns:*
<dl>
<dt>comparison</dt>
<dd>number: 0 if first and second are the same time, 1 if first is a later time than second, -1 if it is an earlier time.</dd>
</dl>

Compares two objects for differences in time, ignoring differences in date.

### dateCompare
*Arguments:*
<dl>
<dt>first</dt>
<dd>Date: First date</dd>
<dt>second</dt>
<dd>number: Second date</dd>
</dl>

*Returns:*
<dl>
<dt>comparison</dt>
<dd>number: 0 if first and second are the same date, 1 if first is a later date than second, -1 if it is an earlier date.</dd>
</dl>

Compares two objects for differences in date, ignoring differences in time.
