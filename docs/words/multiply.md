# Multiply - Function Summary

## Summary:

Returns the first value multiplied by the second.

## Usage:

**multiply value1 value2**

## Arguments:

**value1** - The value1 argument. (must be: number pair char money time tuple)

**value2** - The value2 argument. (must be: number pair char money time tuple)

## Description:

The datatype of the second value may be restricted to INTEGER or DECIMAL, depending on the datatype of the first value (e.g. the first value is a time).

```
print multiply 123 10
1230
```

```
print multiply 3:20 3
10:00
```

```
print multiply 0:01 60
1:00
```

## Related:

[*****](http://www.rebol.com/docs/words/wm.html) - Returns the first value multiplied by the second.
[**/**](http://www.rebol.com/docs/words/wd.html) - Returns the first value divided by the second.
[**//**](http://www.rebol.com/docs/words/wdd.html) - Returns the remainder of first value divided by second.
[**divide**](http://www.rebol.com/docs/words/wdivide.html) - Returns the first value divided by the second.