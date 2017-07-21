# Replace - Function Summary

## Summary:

Replaces the search value with the replace value within the target series.

## Usage:

**replace target search replace**

## Arguments:

**target** - Series that is being modified. (must be: series)

**search** - Value to be replaced.

**replace** - Value to replace with.

## Refinements:

**/all** - Replace all occurrences.

**/case** - Case-sensitive replacement.

## Description:

Searches target block or series for specified data and replaces it with data from the replacement block or series. Block elements may be of any datatype.

The /ALL refinement replaces all occurrences of the searched data in the target block or series.

```
str: "a time a spec a target"
replace str "a " "on "
print str
on time a spec a target
```

```
replace/all str "a " "on "
print str
on time on spec on target
```

```
fruit: ["apples" "lemons" "bananas"]
replace fruit "lemons" "oranges"
print fruit
apples oranges bananas
```

```
numbers: [1 2 3 4 5 6 7 8 9]
replace numbers [4 5 6] ["four" "five" "six"]
print numbers
1 2 3 four five six 7 8 9
```

## Related:

[**change**](http://www.rebol.com/docs/words/wchange.html) - Changes a value in a series and returns the series after the change.
[**insert**](http://www.rebol.com/docs/words/winsert.html) - Inserts a value into a series and returns the series after the insert.
[**remove**](http://www.rebol.com/docs/words/wremove.html) - Removes value(s) from a series and returns after the remove.