# Log-10 - Function Summary

## Summary:

Returns the base-10 logarithm.

## Usage:

**log-10 value**

## Arguments:

**value** - The value argument. (must be: number)

## Description:

The LOG-10 function returns the base-10 logarithm of the number provided. The argument must be a positive value, otherwise an error will occur (which can be trapped with the TRY function).

```
print log-10 100
2.0
```

```
print log-10 1000
3.0
```

```
print log-10 1234
3.09131515969722
```

## Related:

[**exp**](http://www.rebol.com/docs/words/wexp.html) - Raises E (natural number) to the power specified.
[**log-2**](http://www.rebol.com/docs/words/wlog-2.html) - Return the base-2 logarithm.
[**log-e**](http://www.rebol.com/docs/words/wlog-e.html) - Returns the base-E (natural number) logarithm.
[**power**](http://www.rebol.com/docs/words/wpower.html) - Returns the first number raised to the second number.