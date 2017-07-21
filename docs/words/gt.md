# > - Function Summary

------

## Summary:

Returns TRUE if the first value is greater than the second value.

## Usage:

**> value1 value2**

## Arguments:

**value1** - The value1 argument.

**value2** - The value2 argument.

## Description:

Returns FALSE for all other values. The values must be of the same datatype or an error will occur. For string-based datatypes, the sorting order is used for comparison with character casing ignored (uppercase = lowercase).

```
print "abc" > "abb"
true
```

```
print 16-June-1999 > 12-june-1999
true
```

```
print 4.3.2.1 > 1.2.3.4
true
```

```
print 11:00 > 12:00
false
```

## Related:

[**<**](http://www.rebol.com/docs/words/wlt.html) - Returns TRUE if the first value is less than the second value.
[**<=**](http://www.rebol.com/docs/words/wlteq.html) - Returns TRUE if the first value is less than or equal to the second value.
[**<>**](http://www.rebol.com/docs/words/wltgt.html) - Returns TRUE if the values are not equal.
[**=**](http://www.rebol.com/docs/words/weq.html) - Returns TRUE if the values are equal.
[**>=**](http://www.rebol.com/docs/words/wgteq.html) - Returns TRUE if the first value is greater than or equal to the second value.
[**greater?**](http://www.rebol.com/docs/words/wgreaterq.html) - Returns TRUE if the first value is greater than the second value.
[**max**](http://www.rebol.com/docs/words/wmax.html) - Returns the greater of the two values.
[**min**](http://www.rebol.com/docs/words/wmin.html) - Returns the lesser of the two values.