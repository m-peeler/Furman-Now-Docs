---
layout: default
title: SQL Classes
nav_order: 1
parent: Python Documentation 
has_children: false
---
## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---
# SQL Classes
The SQL classes are a set of abstract classes which can be inherited from to provide helper methods for SQL queries. 

## Queriable
### query
<dl>
<dt>connection</dt>
<dd>pymysql.connection: A connection to the mysql server</dd>
<dt>query</dt>
<dd>tuple: A tuple that will be unpacked, which contains the string query as its first argument, and a tuple of all arguments that will be cleaned and inserted into the query</dd>
<dt>commit</dt>
<dd>bool: whether the connection should immediately commit its query.</dd>
</dl>

```py
Queriable.query(connection, ("FROM %s SELECT name=%s", ('table', 'Victor')))
```
## Insertable
### _formulateInsert
*Attributes:*
<dl>
<dt>table</dt>
<dd>str: name of the table being inserted into</dd>
<dt>attrs</dt>
<dd>list: a list of key-value pairs</dd>
</dl>

Creates a tuple with an insert statement and a tuple of values to insert an entry with the attributes of `attrs` into `table`, in the style required by `Queriable.query`.

### _insertIntoHelper
*Attributes:*
<dl>
<dt>table</dt>
<dd>str: name of the table being inserted into</dd>
<dt>connection</dt>
<dd>pymysql.connection</dd>
<dt>attrs</dt>
<dd>list: a list of key-value pairs</dd>
<dt>commit</dt>
<dd>bool: if query should be immediately committed.</dd>
</dl>

### insertInto
*Attributes:*
<dl>
<dt>table</dt>
<dd>str: name of the table being inserted into</dd>
<dt>connection</dt>
<dd>pymysql.connection</dd>
<dt>commit</dt>
<dd>bool: if query should be immediately committed.</dd>
</dl>

Abstract method to insert the object inheriting from `Insertable` into the `table` using the provided `connection`.  

## Selector
<dl>
<dt>table</dt>
<dd>str: name of the table being selected from</dd>
<dt>attrs</dt>
<dd>list or str: either a list of attrs to be selected, or the string 'All" to select all attributes.</dd>
<dt>conds</dt>
<dd>A list of conditions, which can be provided in one of three formats:<br/>
    1. [a, b] where the statement will be "a = b OR"<br/>
    2. [a, b, c] where b is an operateor and the statement will be "a b c OR" <br/>
    3. [a, b, c, d]  where d is "AND" or "OR" and the query will be "a b c d"
</dd>
</dl>

## Clearable



