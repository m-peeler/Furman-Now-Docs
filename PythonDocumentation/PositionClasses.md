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
# Position Classes
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
