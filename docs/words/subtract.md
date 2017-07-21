# Subtract - Function Summary

## Summary:

Returns the second value subtracted from the first.

## Usage:

**subtract value1 value2**

## Arguments:

**value1** - The value1 argument. (must be: number pair char money date time tuple)

**value2** - The value2 argument. (must be: number pair char money date time tuple)

## Description:

When subtracting values of different datatypes the values must be compatible.

```
print subtract 123 1
122
```

```
print subtract 1.2.3.4 1.0.3.0
0.2.0.4
```

```
print subtract 12:00 11:00
1:00
```

```
print subtract 1-Jan-2000 1
31-Dec-1999
```

## Related:

[**+**](http://www.rebol.com/docs/words/w+.html) - Returns the result of adding two values.
[**-**](http://www.rebol.com/docs/words/w-.html) - Returns the second value subtracted from the first.
[**absolute**](http://www.rebol.com/docs/words/wabsolute.html) - Returns the absolute value.
[**add**](http://www.rebol.com/docs/words/wadd.html) - Returns the result of adding two values.