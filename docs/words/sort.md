# Sort - Function Summary

## Summary:

Sorts a series.

## Usage:

**sort series**

## Arguments:

**series** - The series argument. (must be: series port)

## Refinements:

**/case** - Case sensitive sort.

**/skip** - Treat the series as records of fixed size.

**size** - Size of each record. (must be: integer)

**/compare** - Comparator offset, block or function.

**comparator** - The comparator argument. (must be: integer block function)

**/part** - Sort only part of a series.

**length** - Length of series to sort. (must be: integer)

**/all** - Compare all fields

**/reverse** - Reverse sort order

## Description:

If you are sorting records of a fixed size, you will need to use the /SKIP refinement to specify how many elements to ignore.

Normally sorting is not sensitive to character cases, but you can make it sensitive with the /CASE refinement.

A /COMPARE function can be specified to perform the comparison. This allows you to change the ordering of the SORT.

Sorting will modify the series passed as the argument.

```
blk: [799 34 12 934 -24 0]
print sort blk
-24 0 12 34 799 934
```

```
names: ["Fred" "fred" "FRED"]
print sort/case names
FRED Fred fred
```

```
name-ages: [
	"Larry" 45
	"Curly" 50
	"Mo" 42
]
print sort/skip name-ages 2
Curly 50 Larry 45 Mo 42
```

```
names: [
	"Larry"
	"Curly"
	"Mo"
]
print sort/compare names func [a b] [a < b]
Curly Larry Mo
```

```
print sort "edcba"
abcde
```

The ALL refinement will force the entire record to be passed to the compare function. This is useful if you need to compare one or more fields of a record while also doing a skip operation.

## Related:

[**append**](http://www.rebol.com/docs/words/wappend.html) - Appends a value to the tail of a series and returns the series head.
[**change**](http://www.rebol.com/docs/words/wchange.html) - Changes a value in a series and returns the series after the change.
[**clear**](http://www.rebol.com/docs/words/wclear.html) - Removes all values from the current index to the tail. Returns at tail.
[**insert**](http://www.rebol.com/docs/words/winsert.html) - Inserts a value into a series and returns the series after the insert.
[**remove**](http://www.rebol.com/docs/words/wremove.html) - Removes value(s) from a series and returns after the remove.