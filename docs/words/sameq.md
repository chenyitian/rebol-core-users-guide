# Same? - Function Summary

------

## Summary:

Returns TRUE if the values are identical.

## Usage:

**same? value1 value2**

## Arguments:

**value1** - The value1 argument.

**value2** - The value2 argument.

## Description:

Returns TRUE if the values are identical objects, not just in value. For example, a TRUE would be returned if two strings are the same string (occupy the same location in memory). Returns FALSE for all other values.

```
a: "apple"
b: a
print same? a b
true
```

```
print same? a "apple"
false
```

## Related:

[**=?**](http://www.rebol.com/docs/words/weqq.html) - Returns TRUE if the values are identical.
[**equal?**](http://www.rebol.com/docs/words/wequalq.html) - Returns TRUE if the values are equal.