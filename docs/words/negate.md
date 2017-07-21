# Negate - Function Summary

## Summary:

Changes the sign of a number.

## Usage:

**negate number**

## Arguments:

**number** - The number argument. (must be: number pair money time bitset)

## Description:

Returns the negative of the value provided.

```
print negate 123
-123
```

```
print negate -123
123
```

```
print negate 123.45
-123.45
```

```
print negate -123.45
123.45
```

```
print negate 10:30
-10:30
```

```
print negate 100x20
-100x-20
```

```
print negate 100x-20
-100x20
```

## Related:

[**+**](http://www.rebol.com/docs/words/w+.html) - Returns the result of adding two values.
[**-**](http://www.rebol.com/docs/words/w-.html) - Returns the second value subtracted from the first.
[**negative?**](http://www.rebol.com/docs/words/wnegativeq.html) - Returns TRUE if the number is negative.
[**positive?**](http://www.rebol.com/docs/words/wpositiveq.html) - Returns TRUE if the value is positive.