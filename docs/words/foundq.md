# Found? - Function Summary

## Summary:

Returns TRUE if value is not NONE.

## Usage:

**found? value**

## Arguments:

**value** - The value argument.

## Description:

Returns FALSE for all other values. Not usually required because most conditional function will accept a NONE as FALSE and all other values as TRUE.

```
if found? find luke@rebol.com ".com" [print "found it"]
found it
```

## Related:

[**find**](http://www.rebol.com/docs/words/wfind.html) - Finds a value in a series and returns the series at the start of it.
[**pick**](http://www.rebol.com/docs/words/wpick.html) - Returns the value at the specified position in a series.