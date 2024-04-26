---
layout: default
title: Web Connectors
nav_order: 2
parent: Python Documentation 
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# Web Connectors
## Scraper
Abstract base class that web scrapers inherit from.

### didFail
*Returns:*
<dl>
<dt>didFail</dt>
<dd>bool: if pulling and scrapping website failed</dd>
</dl>

### gotContent
*Returns:*
<dl>
<dt>gotContent</dt>
<dd>bool: if content was successfully returned when pulling</dd>
</dl>

### getSite
*Arguments:*
<dl>
<dt>link</dt>
<dd>str: link to website</dd>
</dl>

*Returns:*
<dl>
<dt>website</dt>
<dd>requests.Response: response to requesting website</dd>
</dl>

### getSoup
*Arguments:*
<dl>
<dt>link</dt>
<dd>str: link to website</dd>
</dl>

*Returns:*
<dl>
<dt>websiteSoup</dt>
<dd>BeautifulSoup: parsed soup of the website</dd>
</dl>

### _pull
**Abstract Method**
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of items pulled from the website</dd>
</dl>

Abstract base class which all children of Scraper must implement. Pulls the website, locates all important information, and formats each into the correct style, then returns them as the `pulled` list.

### tryPull
*Returns:*
<dl>
<dt>pulled</dt>
<dd>list: list of items pulled from the website</dd>
</dl>

Using the `_tryPull` abstract method, pulls and parses the website with error handling. Saves success status and found content status based on results.

### maybeGetValue
*Arguments:*
<dl>
<dt>dct</dt>
<dd>dict: dictionary value is being sought from</dd>
<dt>*keys</dt>
<dd>any number of successive str or int: a sequence of keys/indices which the user is attempting to find their value at the end of.</dd>
<dt>default</dt>
<dd>any: default value that will be returned if any of the keys/indices do not exist in the dictionary</dd>
</dl>

*Returns:*
<dl>
<dt>val</dt>
<dd>any: value stored in dct at the specified position, if it exists, otherwise <tt>default</tt></dd>
</dl>

Given a dictionary `dct`, checks if the value at the `keys` indices of `dct` exists and if so returns the value, otherwise `default`. `Scraper.maybeGetValue(dict, key0, key1, key2)` to doing `dct[key0][key1][key2]`, but without the risk of null pointer errors. 

## formConnection
*Returns:*
<dl>
<dt>connection</dt>
<dd>pymysql.connection: a setup connection to connect with database</dd>
</dl>

Forms a connection with the database using specified parameters and stored login information.

## youTubePullLatest
*Arguments:*
<dl>
<dt>channelID</dt>
<dd>str or int: youtube channel ID for the channel being sought</dd>
<dt>numRequested</dt>
<dd>int: number of returns requested, maximum of 50, default is set to 10</dd>
</dl>

Using API key information, returns a list of the latest `numRequested` posts from the YouTube channel with the provided `channelID`.


## getLibraryAPIToken
*Returns:*
<dl>
<dt>token</dt>
<dd>str: generated API token</dd>
</dl>


Generates an API token to access the LibCal API for the Furman Libraries using the saved secret and id.