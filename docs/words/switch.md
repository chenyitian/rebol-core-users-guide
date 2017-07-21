# Switch - Function Summary

## Summary:

Selects a choice and evaluates what follows it.

## Usage:

**switch value cases**

## Arguments:

**value** - Value to search for.

**cases** - Block of cases to search. (must be: block)

## Refinements:

**/default** - The default refinement.

**case** - Default case if no others are found.

## Description:

Switch also returns the value of the block it executes. The cases can be any datatype. If none of the other cases match, use the /DEFAULT refinement to specify a default case.

```
switch 22 [
	11 [print "here"]
	22 [print "there"]
]
there
```

```
person: 'mom
switch person [    ; words
	dad [print "here"]
	mom [print "there"]
	kid [print "everywhere"]
]
there
```

```
file: %user.r
switch file [
	%user.r [print "here"]
	%rebol.r [print "everywhere"]
	%file.r [print "there"]
]
here
```

```
url: ftp://ftp.rebol.org
switch url [  
	http://www.rebol.com [print "here"]
	http://www.cnet.com [print "there"]
	ftp://ftp.rebol.org [print "everywhere"]
]
everywhere
```

```
html-tag: <TITLE>
print switch html-tag [
	<PRE>   ["Preformatted text"]
	<TITLE> ["Page title"]
	<LI>    ["Bulleted list item"]
]
Page title
```

```
time: 12:30
switch time [
	 8:00 [send wendy@domain.dom "Hey, get up"]
	12:30 [send cindy@dom.dom "Join me for lunch."]
	16:00 [send group@every.dom "Dinner anyone?"]
]
```

```
car: pick [Ford Chevy Dodge] random 3
print switch car [
	Ford [351 * 1.4]
	Chevy [454 * 5.3]
	Dodge [154 * 3.5]
]
491.4
```

## Related:

[**find**](http://www.rebol.com/docs/words/wfind.html) - Finds a value in a series and returns the series at the start of it.
[**select**](http://www.rebol.com/docs/words/wselect.html) - Finds a value in the series and returns the value or series after it.