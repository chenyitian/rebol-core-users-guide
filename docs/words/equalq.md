# Equal? - Function Summary

## Summary:

Returns TRUE if the values are equal.

## Usage:

**equal? value1 value2**

## Arguments:

**value1** - The value1 argument.

**value2** - The value2 argument.

## Description:

String-based datatypes are equal when they are identical or differ only by character casing (uppercase = lowercase).

```
print equal? 123 123
true
```

```
print equal? "abc" "abc"
true
```

```
print equal? [1 2 3] [1 2 4]
false
```

```
print equal? 12-june-1998 12-june-1999
false
```

```
print equal? 1.2.3.4 1.2.3.0
false
```

```
print equal? 1:23 1:23
true
```

## Related:

[**<>**](http://www.rebol.com/docs/words/wltgt.html) - Returns TRUE if the values are not equal.
[**=**](http://www.rebol.com/docs/words/weq.html) - Returns TRUE if the values are equal.
[**==**](http://www.rebol.com/docs/words/weqeq.html) - Returns TRUE if the values are equal and of the same datatype.
[**=?**](http://www.rebol.com/docs/words/weqq.html) - Returns TRUE if the values are identical.
[**strict-equal?**](http://www.rebol.com/docs/words/wstrict-equalq.html) - Returns TRUE if the values are equal and of the same datatype.