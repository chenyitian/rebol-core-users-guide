# Min - Function Summary

## Summary:

Returns the lesser of the two values.

## Usage:

**min value1 value2**

## Arguments:

**value1** - The value1 argument. (must be: number pair char money date time tuple series)

**value2** - The value2 argument. (must be: number pair char money date time tuple series)

## Description:

Returns the minimum of two values.

```
print min 0 100
0
```

```
print min 0 -100
-100
```

```
print min 4.56 4.2
4.2
```

The minimum value is computed by comparison, so MIN can also be used for non-numeric datatypes as well.

```
print min 1.2.3 1.2.8
1.2.3
```

```
print min "abc" "abd"
abc
```

```
print min 12:00 11:00
11:00
```

```
print min 1-Jan-1920 20-Feb-1952
1-Jan-1920
```

Using min on XY pairs will return the minimum of each X and Y coordinate separately.

```
print min 100x10 200x20
100x10
```

## Related:

[**<**](http://www.rebol.com/docs/words/wlt.html) - Returns TRUE if the first value is less than the second value.
[**>**](http://www.rebol.com/docs/words/wgt.html) - Returns TRUE if the first value is greater than the second value.
[**max**](http://www.rebol.com/docs/words/wmax.html) - Returns the greater of the two values.
[**maximum-of**](http://www.rebol.com/docs/words/wmaximum-of.html) - Finds the largest value in a series
[**minimum-of**](http://www.rebol.com/docs/words/wminimum-of.html) - Finds the smallest value in a series