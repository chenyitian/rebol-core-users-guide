# Maximum-of - Function Summary

## Summary:

Finds the largest value in a series

## Usage:

**maximum-of series**

## Arguments:

**series** - Series to search (must be: series)

## Refinements:

**/skip** - Treat the series as records of fixed size

**size** - The size argument. (must be: integer)

**/case** - Perform case-sensitive comparisons

## Description:

Return the series at the position of its maximum value.

```
probe maximum-of [34 6 60 59 5]
[60 59 5]
```

```
probe maximum-of ["abc" "def" "xyz" "aaa" "efg"]
["xyz" "aaa" "efg"]
```

## Related:

[**max**](http://www.rebol.com/docs/words/wmax.html) - Returns the greater of the two values.
[**min**](http://www.rebol.com/docs/words/wmin.html) - Returns the lesser of the two values.