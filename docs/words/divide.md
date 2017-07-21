# Divide - Function Summary

## Summary:

Returns the first value divided by the second.

## Usage:

**divide value1 value2**

## Arguments:

**value1** - The value1 argument. (must be: number pair char money time tuple)

**value2** - The value2 argument. (must be: number pair char money time tuple)

## Description:

If the second value is zero, an error will occur. When dividing values of different datatypes, they must be compatible.

```
print divide 123.1 12
10.2583333333333
```

```
print divide 10:00 4
2:30
```

## Related:

[*****](http://www.rebol.com/docs/words/wm.html) - Returns the first value multiplied by the second.
[**/**](http://www.rebol.com/docs/words/wd.html) - Returns the first value divided by the second.
[**//**](http://www.rebol.com/docs/words/wdd.html) - Returns the remainder of first value divided by second.
[**multiply**](http://www.rebol.com/docs/words/wmultiply.html) - Returns the first value multiplied by the second.