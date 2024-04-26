---
layout: default
title: News Scrapers
nav_order: 6
parent: Python Documentation 
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

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

### getTableID
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

### cleanDescription
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

## PaladinScraper
**Inherits from `NewsScraper`** \\

Scrapes articles from the Paladin website. 

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of the Paladin in database tables</dd>
</dl>

### getSection
*Arguments:*
<dl>
<dt>entry</dt>
<dd>any: single article entry from Paladin RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>section</dt>
<dd>str: article's section</dd>
</dl>

### getImage
*Arguments:*
<dl>
<dt>entry</dt>
<dd>any: single article entry from Paladin RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>link</dt>
<dd>str: url to article's header image</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of The Paladin's Articles</dd>
</dl>

## PresidentScraper
**Inherits from `NewsScraper`** \\

Scrapes articles from the President's Page website. 

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of the President's Page in database tables</dd>
</dl>

### getImage
*Arguments:*
<dl>
<dt>entry</dt>
<dd>any: single article entry from the President's Page RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>link</dt>
<dd>str: url to article's header image</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of The President's Page Articles</dd>
</dl>

## FurmanNewsScraper
**Inherits from `NewsScraper`** \\

Scrapes articles from the Furman in the News website. 

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of the Furman in the News in database tables</dd>
</dl>

### getImage
*Arguments:*
<dl>
<dt>entry</dt>
<dd>any: single article entry from the Furman in the News RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>link</dt>
<dd>str: url to article's header image</dd>
</dl>

### getSummary
*Arguments:*
<dl>
<dt>entry</dt>
<dd>any: single article entry from the Furman in the News RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>summary</dt>
<dd>str: cleaned summary of article</dd>
</dl>

### getLink
*Arguments:*
<dl>
<dt>entry</dt>
<dd>any: single article entry from the Furman in the News RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>link</dt>
<dd>str: url to article</dd>
</dl>

Many Furman in the News articles have multiple links in them; this function determines the best one to save for the article. If the piece is short and only links one place, the link it directs to is used; otherwise, the article's link is used.

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Furman in the News Articles</dd>
</dl>

## FUNCScraper
**Inherits from `NewsScraper`** \\

Scrapes articles from the FUNC on YouTube. 

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of FUNC in database tables</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the FUNC Articles</dd>
</dl>

## KnightlyNewsScraper
**Inherits from `NewsScraper`** \\

Scrapes articles from the Furman in the News website. 

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of Knightly News in database tables</dd>
</dl>

### cleanDescription
*Arguments:*
<dl>
<dt>description</dt>
<dd>str: raw description of video </dd>
</dl>

*Returns:*
<dl>
<dt>description</dt>
<dd>str: cleaned description of video</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Knightly News Articles</dd>
</dl>

## TocquevilleScraper
**Inherits from `NewsScraper`** \\

Scrapes articles from the Tocqueville Center's blog and YouTube channel.

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of Tocqueville Center in database tables</dd>
</dl>

### getSummary
*Arguments:*
<dl>
<dt>blogEntry</dt>
<dd>any: entry from Tocqueville blog RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>summary</dt>
<dd>str: cleaned summary</dd>
</dl>

### getImage
*Arguments:*
<dl>
<dt>blogEntry</dt>
<dd>any: entry from Tocqueville blog RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>link</dt>
<dd>str: image url link</dd>
</dl>

Gets the header image from a blog entry

### _pullYoutube
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Tocqueville Center's YouTube channel's Articles</dd>
</dl>

### _pullBlog
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Tocqueville Center's blog's Articles</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Tocqueville Center Articles</dd>
</dl>

## RileyScraper
**Inherits from `NewsScraper`** \\

Scrapes articles from the Riley Institute's blog and YouTube channel.

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of Riley Institute in database tables</dd>
</dl>

### getSummary
*Arguments:*
<dl>
<dt>blogEntry</dt>
<dd>any: entry from Riley Institute blog RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>summary</dt>
<dd>str: cleaned summary</dd>
</dl>

### getImage
*Arguments:*
<dl>
<dt>blogEntry</dt>
<dd>any: entry from Riley Institute blog RSS feed</dd>
</dl>

*Returns:*
<dl>
<dt>link</dt>
<dd>str: image url link</dd>
</dl>

Gets the header image from a blog entry.

### _pullYoutube
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Riley Institute's YouTube channel's Articles</dd>
</dl>

### _pullBlog
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Riley Institute's blog's Articles</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Riley Institute's Articles</dd>
</dl>

## FUSEScraper (abstract base class)
Abstract base class with helper methods for parsing articles from Furman University Scholar Exchange.

### cleanParseTime(date):
*Arguments:*
<dl>
<dt>date</dt>
<dd>str: date</dd>
</dl>

*Returns:*
<dl>
<dt>date</dt>
<dd>datetime: date parsed into a datetime object and converted to EST time zone.</dd>
</dl>

### articleAssembler
*Arguments:*
<dl>
<dt>rssEntry</dt>
<dd>any: entry from a FUSE RSS feed</dd>
<dt>defaultAuthor</dt>
<dd>str: name to use if RSS entry does not have an author</dd>
</dl>

*Returns:*
<dl>
<dt>article</dt>
<dd>Article: parsed Article of rss entry</dd>
</dl>

Assembles an `Article` given the RSS entry from the FUSE RSS feed.

## EchoScraper
**Inherits from `FUSEScraper`** \\

Scrapes all of the articles from the last edition of the Echo. 

<dl>
<dt>grabCover</dt>
<dd>bool: if true, finds the cover page pdf and saves it as a PNG; default to true</dd>
</dl>

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of the Echo in database tables</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Echo's articles from the last edition.</dd>
</dl>

## FHRScraper
**Inherits from `FUSEScraper`** \\

Scrapes all of the articles from the last edition of the Furman Humanities Review.

<dl>
<dt>grabCover</dt>
<dd>bool: if true, finds the cover page pdf and saves it as a PNG; default to true</dd>
</dl>

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of the FHR in database tables</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the FHR's articles from the last edition.</dd>
</dl>

## HillScraper
**Inherits from `NewsScraper`** \\

Scrapes all of the articles from the Hill Institute's podcast.

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of the Hill Institute in database tables</dd>
</dl>

### _pullPodcasts
*Returns:*
<dl>
<dt>podcasts</dt>
<dd>list: list of all of the Hill Institue's latest podcasts.</dd>
</dl>

### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Hill Institue's articles.</dd>
</dl>

## ShiScraper
**Inherits from `NewsScraper`** \\

Scrapes all of the articles from the Shi Institute's blog.

### getTableID
*Returns:*
<dl>
<dt>tableID</dt>
<dd>int: id of the Shi Institute in database tables</dd>
</dl>

### _getImageLink
*Arguments:*
<dl>
<dt>links</dt>
<dd>list of any: list of RSS feed's article links</dd>
</dl>

*Returns:*
<dl>
<dt>link</dt>
<dd>str: link to header image for article</dd>
</dl>


### _pull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of all of the Shi Institute's articles.</dd>
</dl>

## purgeOldEvents
*Arguments:*
<dl>
<dt>connection</dt>
<dd>pymysql.connection: connection to database</dd>
<dt>publisherID</dt>
<dd>int: id for news publisher whose articles will be deleted</dd>
</dl>

Deletes all existing articles from the provided news source.