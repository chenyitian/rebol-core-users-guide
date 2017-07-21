# Strict-not-equal? - Function Summary

## Summary:

Returns TRUE if the values are not equal and not of the same datatype.

## Usage:

**strict-not-equal? value1 value2**

## Arguments:

**value1** - The value1 argument.

**value2** - The value2 argument.

## Description:

A FALSE is returned if the values differ by datatype (so 1 would not be equal to 1.0) nor by character casing (so "abc" would not be equal to "ABC").

```
print strict-not-equal? 124 123
false
```

```
print strict-not-equal? 12-sep-98 10:30
true
```

## Related:

[**<>**](http://www.rebol.com/docs/words/wltgt.html) - Returns TRUE if the values are not equal.
[**=**](http://www.rebol.com/docs/words/weq.html) - Returns TRUE if the values are equal.
[**==**](http://www.rebol.com/docs/words/weqeq.html) - Returns TRUE if the values are equal and of the same datatype.