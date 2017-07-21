# Log-e - Function Summary

## Summary:

Returns the base-E (natural number) logarithm.

## Usage:

**log-e value**

## Arguments:

**value** - The value argument. (must be: number)

## Description:

The LOG-E function returns the natural logarithm of the number provided. The argument must be a positive value, otherwise an error will occur (which can be trapped with the TRY function).

```
print log-e 1234
7.11801620446533
```

```
print exp log-e 1234
1234.0
```

## Related:

[**exp**](http://www.rebol.com/docs/words/wexp.html) - Raises E (natural number) to the power specified.
[**log-10**](http://www.rebol.com/docs/words/wlog-10.html) - Returns the base-10 logarithm.
[**log-2**](http://www.rebol.com/docs/words/wlog-2.html) - Return the base-2 logarithm.
[**power**](http://www.rebol.com/docs/words/wpower.html) - Returns the first number raised to the second number.