# Change - Function Summary

## Summary:

Changes a value in a series and returns the series after the change.

## Usage:

**change series value**

## Arguments:

**series** - Series at point to change (must be: series port)

**value** - The new value (must be: any-type)

## Refinements:

**/part** - Limits the amount to change to a given length or position.

**range** - The range argument. (must be: number series port pair)

**/only** - Changes a series as a series.

**/dup** - Duplicates the change a specified number of times.

**count** - The count argument. (must be: number pair)

## Description:

If the second argument is a simple value, it will replace the value at the current position in the first series. If the second argument is a series compatible with the first (block or string-based datatype), all of its values will replace those of the first argument or series.

The /PART refinement changes a specified number of elements within the target series.

For the convenience of cascading multiple changes the CHANGE function returns the series position just past the change.

```
probe head change "bog" "d"
"dog"
```

```
probe head change [123 "test"] "the"
["the" "test"]
```

```
probe head change/dup "abc" "->" 5
"->->->->->"
```

```
probe head change/part "abcde" "1234" 2
"1234cde"
```

```
probe head change [1 4 5] [1 2 3]
[1 2 3]
```

```
title: copy "how it REBOL"
change title "N"
probe title
"Now it REBOL"
```

```
change find title "t" "s"
probe title
"Now is REBOL"
```

```
blk: copy ["now" 12:34 "REBOL"]
change next blk "is"
probe blk
["now" "is" "REBOL"]
```

```
probe head change/only [1 4 5] [1 2 3]
[[1 2 3] 4 5]
```

```
probe head change/only [1 4 5] [[1 2 3]]
[[[1 2 3]] 4 5]
```

```
string: copy "crush those grapes"
change/part string "eat" find/tail string "crush"
probe string
"eat those grapes"
```

## Related:

[**append**](http://www.rebol.com/docs/words/wappend.html) - Appends a value to the tail of a series and returns the series head.
[**clear**](http://www.rebol.com/docs/words/wclear.html) - Removes all values from the current index to the tail. Returns at tail.
[**insert**](http://www.rebol.com/docs/words/winsert.html) - Inserts a value into a series and returns the series after the insert.
[**remove**](http://www.rebol.com/docs/words/wremove.html) - Removes value(s) from a series and returns after the remove.
[**sort**](http://www.rebol.com/docs/words/wsort.html) - Sorts a series.