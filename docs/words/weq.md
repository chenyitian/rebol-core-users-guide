# = - Function Summary

## Summary:

Returns TRUE if the values are equal.

## Usage:

**= value1 value2**

## Arguments:

**value1** - The value1 argument.

**value2** - The value2 argument.

## Description:

String-based datatypes are considered equal when they are identical or differ only by character casing (uppercase = lowercase). Use == or find/match/case to compare strings by casing.

```
print 123 = 123
true
print "abc" = "abc"
true
print [1 2 3] = [1 2 4]
false
print 12-june-1998 = 12-june-1999
false
print 1.2.3.4 = 1.2.3.0
false
print 1:23 = 1:23
true
```

## Related:

[**<>**](http://www.rebol.com/docs/words/wltgt.html) - Returns TRUE if the values are not equal.
[**==**](http://www.rebol.com/docs/words/weqeq.html) - Returns TRUE if the values are equal and of the same datatype.
[**equal?**](http://www.rebol.com/docs/words/wequalq.html) - Returns TRUE if the values are equal.