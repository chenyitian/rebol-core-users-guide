# Remove - Function Summary

## Summary:

Removes value(s) from a series and returns after the remove.

## Usage:

**remove series**

## Arguments:

**series** - The series argument. (must be: series port bitset none)

## Refinements:

**/part** - Removes to a given length or position.

**range** - The range argument. (must be: number series port pair)

## Description:

Normally removes just a single value from the current position. However, you can remove any number of values with the /PART refinement.

```
str: copy "send it here"
remove str
print str
end it here
```

```
remove/part str find str "it"
print str
it here
```

```
remove/part str 3
print str
here
```

```
blk: copy [red green blue]
remove next blk
probe blk
[red blue]
```

## Related:

[**append**](http://www.rebol.com/docs/words/wappend.html) - Appends a value to the tail of a series and returns the series head.
[**change**](http://www.rebol.com/docs/words/wchange.html) - Changes a value in a series and returns the series after the change.
[**clear**](http://www.rebol.com/docs/words/wclear.html) - Removes all values from the current index to the tail. Returns at tail.
[**insert**](http://www.rebol.com/docs/words/winsert.html) - Inserts a value into a series and returns the series after the insert.
[**sort**](http://www.rebol.com/docs/words/wsort.html) - Sorts a series.