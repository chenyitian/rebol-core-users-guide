# Add - Function Summary

## Summary:

Returns the result of adding two values.

## Usage:

**add value1 value2**

## Arguments:

**value1** - The value1 argument. (must be: number pair char money date time tuple)

**value2** - The value2 argument. (must be: number pair char money date time tuple)

## Description:

When adding values of different datatypes, the values must be compatible.

```
print add 123 1
124
```

```
print add 1.2.3.4 4.3.2.1
5.5.5.5
```

```
print add 3:00 -4:00
-1:00
```

```
print add 31-Dec-1999 1
1-Jan-2000
```

## Related:

[**+**](http://www.rebol.com/docs/words/w+.html) - Returns the result of adding two values.
[**-**](http://www.rebol.com/docs/words/w-.html) - Returns the second value subtracted from the first.
[**subtract**](http://www.rebol.com/docs/words/wsubtract.html) - Returns the second value subtracted from the first.