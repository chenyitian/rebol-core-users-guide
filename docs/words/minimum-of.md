# Minimum-of - Function Summary

## Summary:

Finds the smallest value in a series

## Usage:

**minimum-of series**

## Arguments:

**series** - Series to search (must be: series)

## Refinements:

**/skip** - Treat the series as records of fixed size

**size** - The size argument. (must be: integer)

**/case** - Perform case-sensitive comparisons

## Description:

Return the series at the position of its minimum value.

```
probe minimum-of [34 20 4 6 60]
[4 6 60]
```

```
probe minimum-of ["abc" "def" "xy" "aaaxy" "efg"]
["aaaxy" "efg"]
```

## Related:

[**max**](http://www.rebol.com/docs/words/wmax.html) - Returns the greater of the two values.
[**min**](http://www.rebol.com/docs/words/wmin.html) - Returns the lesser of the two values.