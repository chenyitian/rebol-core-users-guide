# Complement - Function Summary

## Summary:

Returns the one's complement value.

## Usage:

**complement value**

## Arguments:

**value** - The value argument. (must be: logic number char tuple bitset)

## Description:

Used for bitmasking of integer numbers and inverting bitsets (charsets).

```
print complement 0
-1
```

```
print complement -1
0
```

```
chars: complement charset "ther "
print find "there it goes" chars
it goes
```

## Related:

[**negate**](http://www.rebol.com/docs/words/wnegate.html) - Changes the sign of a number.