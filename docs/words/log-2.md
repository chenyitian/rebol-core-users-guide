# Log-2 - Function Summary

## Summary:

Return the base-2 logarithm.

## Usage:

**log-2 value**

## Arguments:

**value** - The value argument. (must be: number)

## Description:

The LOG-10 function returns the base-2 logarithm of the number provided. The argument must be a positive value, otherwise an error will occur (which can be trapped with the TRY function).

```
print log-2 2
1.0
```

```
print log-2 4
2.0
```

```
print log-2 256
8.0
```

```
print log-2 1234
10.2691266791494
```

## Related:

[**exp**](http://www.rebol.com/docs/words/wexp.html) - Raises E (natural number) to the power specified.
[**log-10**](http://www.rebol.com/docs/words/wlog-10.html) - Returns the base-10 logarithm.
[**log-e**](http://www.rebol.com/docs/words/wlog-e.html) - Returns the base-E (natural number) logarithm.
[**power**](http://www.rebol.com/docs/words/wpower.html) - Returns the first number raised to the second number.