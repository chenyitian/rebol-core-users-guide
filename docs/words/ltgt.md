# <> - Function Summary

## Summary:

Returns TRUE if the values are not equal.

## Usage:

**<> value1 value2**

## Arguments:

**value1** - The value1 argument.

**value2** - The value2 argument.

## Description:

String-based datatypes are considered equal when they are identical or differ only by character casing (uppercase = lowercase). Use == or find/match/case to compare strings by casing.

```
print "abc" <> "abcd"
true
```

```
print [1 2 4] <> [1 2 3]
true
```

```
print 12-sep-98 <> 10:30
true
```

## Related:

[**=**](http://www.rebol.com/docs/words/weq.html) - Returns TRUE if the values are equal.
[**==**](http://www.rebol.com/docs/words/weqeq.html) - Returns TRUE if the values are equal and of the same datatype.
[**not-equal?**](http://www.rebol.com/docs/words/wnot-equalq.html) - Returns TRUE if the values are not equal.