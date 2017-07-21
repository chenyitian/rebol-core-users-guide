# Help - Function Summary

## Summary:

Prints information about words and values.

## Usage:

**help word**

## Arguments:

**word** - The word argument. (must be: any-type)

## Description:

The HELP function provides a simple way to get information about words and values. To use HELP, supply a word or a value as its argument:

```
help quit
USAGE:
	QUIT 

DESCRIPTION:
	Stops evaluation and exits the interpreter. 
    QUIT is a native value.
```

Other examples:

```
help now
USAGE:
	NOW /year /month /day /time /zone /date /weekday /precise 

DESCRIPTION:
	Returns the current local date and time. 
	NOW is a native value.

REFINEMENTS:
	/year -- Returns the year only.
	/month -- Returns the month only.
	/day -- Returns the day of the month only.
	/time -- Returns the time only.
	/zone -- Returns the time zone offset from GMT only.
	/date -- Returns date only.
	/weekday -- Returns day of the week as integer (Monday is day 1).
	/precise -- Use nanosecond precision
```

```
help insert
USAGE:
	INSERT series value /part range /only /dup count 

DESCRIPTION:
	Inserts a value into a series and returns the series after the insert. 
	INSERT is an action value.

ARGUMENTS:
	series -- Series at point to insert (Type: series port bitset)
	value -- The value to insert (Type: any-type)

REFINEMENTS:
	/part -- Limits to a given length or position.
	range -- (Type: number series port pair)
	/only -- Inserts a series as a series.
	/dup -- Duplicates the insert a specified number of times.
	count -- (Type: number pair)
```

You can also use HELP to find all the words that match a substring. To do so, provide a string in quotes:

```
help "path"
Found these words: 
	clean-path      function! Cleans-up '.' and '..' in path; returns the cleane... 
	link-relative-path function! Remove link-root from a file path 
	lit-path!       datatype! lit-path! 
	lit-path?       action!   Returns TRUE for lit-path values. 
	path            file!     %/C/rebol/link/ranch/projects/manuals/dictionary/u... 
	path!           datatype! path! 
	path-thru       function! Return a path relative to the disk cache. 
	path?           action!   Returns TRUE for path values. 
	set-browser-path native!  Path to default web browser. 
	set-path!       datatype! set-path! 
	set-path?       action!   Returns TRUE for set-path values. 
	split-path      function! Splits a file or URL path. Returns a block contain... 
	to-lit-path     function! [value] 
	to-path         function! [value] 
	to-set-path     function! [value]
```

```
help "to-"
Found these words: 
	caret-to-offset native!   Returns the offset position relative to the face o... 
	hsv-to-rgb      native!   Converts HSV (hue, saturation, value) to RGB 
	offset-to-caret native!   Returns the offset in the face's text correspondin... 
	rgb-to-hsv      native!   Converts RGB value to HSV (hue, saturation, value) 
	to-binary       function! [value] 
	to-bitset       function! [value] 
	to-block        function! [value] 
	to-char         function! [value] 
	to-datatype     function! [value] 
	to-date         function! [value] 
	to-decimal      function! [value] 
	to-email        function! [value] 
	to-error        function! [value] 
	to-file         function! [value] 
	to-get-word     function! [value] 
	to-hash         function! [value] 
	to-hex          native!   Converts an integer to a hex issue!. 
	to-idate        function! Returns a standard Internet date string. 
	to-image        function! [value] 
	to-integer      function! [value] 
	to-issue        function! [value] 
	to-library      function! [value] 
	to-list         function! [value] 
	to-lit-path     function! [value] 
	to-lit-word     function! [value] 
	to-local-file   native!   Converts a REBOL file path to the local system fil... 
	to-logic        function! [value] 
	to-money        function! [value] 
	to-none         function! [value] 
	to-pair         function! [value] 
	to-paren        function! [value] 
	to-path         function! [value] 
	to-port         function! [value] 
	to-rebol-file   native!   Converts a local system file path to a REBOL file ... 
	to-refinement   function! [value] 
	to-set-path     function! [value] 
	to-set-word     function! [value] 
	to-string       function! [value] 
	to-tag          function! [value] 
	to-time         function! [value] 
	to-tuple        function! [value] 
	to-url          function! [value] 
	to-word         function! [value]
```

You can view all words that are of a specific datatype by specifying the datatype. The example:

```
help tuple!
Found these words: 
	aqua            tuple!    40.100.130 
	bar-color       tuple!    180.180.250 
	base-color      tuple!    143.127.111 
	beige           tuple!    255.228.196 
	black           tuple!    0.0.0 
	blue            tuple!    0.0.255 
	brick           tuple!    178.34.34 
	brown           tuple!    139.69.19 
	button-color    tuple!    44.80.132 
	coal            tuple!    64.64.64 
	coffee          tuple!    76.26.0 
	crimson         tuple!    220.20.60 
	cyan            tuple!    0.255.255 
	forest          tuple!    0.48.0 
	gold            tuple!    255.205.40 
	gray            tuple!    128.128.128 
	green           tuple!    0.255.0 
	ivory           tuple!    255.255.240 
	khaki           tuple!    179.179.126 
	leaf            tuple!    0.128.0 
	linen           tuple!    250.240.230 
	magenta         tuple!    255.0.255 
	main-color      tuple!    175.155.120 
	maroon          tuple!    128.0.0 
	mint            tuple!    100.136.116 
	navy            tuple!    0.0.128 
	oldrab          tuple!    72.72.16 
	olive           tuple!    128.128.0 
	orange          tuple!    255.150.10 
	over-color      tuple!    44.80.132 
	papaya          tuple!    255.80.37 
	pewter          tuple!    170.170.170 
	pink            tuple!    255.164.200 
	purple          tuple!    128.0.128 
	reblue          tuple!    38.58.108 
	rebolor         tuple!    142.128.110 
	red             tuple!    255.0.0 
	sienna          tuple!    160.82.45 
	silver          tuple!    192.192.192 
	sky             tuple!    164.200.255 
	snow            tuple!    240.240.240 
	tan             tuple!    222.184.135 
	teal            tuple!    0.128.128 
	violet          tuple!    72.0.90 
	water           tuple!    80.108.142 
	wheat           tuple!    245.222.129 
	white           tuple!    255.255.255 
	yellow          tuple!    255.255.0
```

would list all tuple functions. Other examples: type "help function!" to list all REBOL defined functions, or even:

```
help datatype!
Found these words: 
	action!         datatype! action! 
	any-block!      datatype! any-block! 
	any-function!   datatype! any-function! 
	any-string!     datatype! any-string! 
	any-type!       datatype! any-type! 
	any-word!       datatype! any-word! 
	binary!         datatype! binary! 
	bitset!         datatype! bitset! 
	block!          datatype! block! 
	char!           datatype! char! 
	datatype!       datatype! datatype! 
	date!           datatype! date! 
	decimal!        datatype! decimal! 
	email!          datatype! email! 
	error!          datatype! error! 
	event!          datatype! event! 
	file!           datatype! file! 
	function!       datatype! function! 
	get-word!       datatype! get-word! 
	hash!           datatype! hash! 
	image!          datatype! image! 
	integer!        datatype! integer! 
	issue!          datatype! issue! 
	library!        datatype! library! 
	list!           datatype! list! 
	lit-path!       datatype! lit-path! 
	lit-word!       datatype! lit-word! 
	logic!          datatype! logic! 
	money!          datatype! money! 
	native!         datatype! native! 
	none!           datatype! none! 
	number!         datatype! number! 
	object!         datatype! object! 
	op!             datatype! op! 
	pair!           datatype! pair! 
	paren!          datatype! paren! 
	path!           datatype! path! 
	port!           datatype! port! 
	refinement!     datatype! refinement! 
	routine!        datatype! routine! 
	series!         datatype! series! 
	set-path!       datatype! set-path! 
	set-word!       datatype! set-word! 
	string!         datatype! string! 
	struct!         datatype! struct! 
	symbol!         datatype! symbol! 
	tag!            datatype! tag! 
	time!           datatype! time! 
	tuple!          datatype! tuple! 
	unset!          datatype! unset! 
	url!            datatype! url! 
	word!           datatype! word!
```

## Related:

[**?**](http://www.rebol.com/docs/words/wq.html) - Prints information about words and values.
[**??**](http://www.rebol.com/docs/words/wqq.html) - Prints a variable name followed by its molded value. (for debugging)
[**what**](http://www.rebol.com/docs/words/wwhat.html) - Prints a list of globally-defined functions.