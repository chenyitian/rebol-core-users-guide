# Clear - Function Summary

## Summary:

Removes all values from the current index to the tail. Returns at tail.

## Usage:

**clear series**

## Arguments:

**series** - The series argument. (must be: series port bitset none)

## Description:

CLEAR is similar to REMOVE but removes through the end of the series rather than just a single value.

```
str: copy "with all things considered"
clear skip str 8
print str
with all
```

```
str: copy "get there quickly"
clear find str "qui"
print str
get there
```

## Related:

[**append**](http://www.rebol.com/docs/words/wappend.html) - Appends a value to the tail of a series and returns the series head.
[**change**](http://www.rebol.com/docs/words/wchange.html) - Changes a value in a series and returns the series after the change.
[**insert**](http://www.rebol.com/docs/words/winsert.html) - Inserts a value into a series and returns the series after the insert.
[**remove**](http://www.rebol.com/docs/words/wremove.html) - Removes value(s) from a series and returns after the remove.
[**sort**](http://www.rebol.com/docs/words/wsort.html) - Sorts a series.