# Remainder - Function Summary

## Summary:

Returns the remainder of first value divided by second.

## Usage:

**remainder value1 value2**

## Arguments:

**value1** - The value1 argument. (must be: number pair char money time tuple)

**value2** - The value2 argument. (must be: number pair char money time tuple)

## Description:

If the second number is zero, an error will occur.

```
print remainder 123 10
3
```

```
print remainder 10 10
0
```

```
print remainder 10.2 10
0.199999999999999
```

If the first value is positive, then the returned remainder is nonnegative.

If the first value is negative, then the returned remainder is nonpositive.

## Related:

[*****](http://www.rebol.com/docs/words/wm.html) - Returns the first value multiplied by the second.
[**/**](http://www.rebol.com/docs/words/wd.html) - Returns the first value divided by the second.
[**//**](http://www.rebol.com/docs/words/wdd.html) - Returns the remainder of first value divided by second.