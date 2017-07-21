# Sign? - Function Summary

## Summary:

Returns sign of number as 1, 0, or -1 (to use as multiplier).

## Usage:

**sign? number**

## Arguments:

**number** - The number argument. (must be: number money time)

## Description:

The SIGN? function returns a positive, zero, or negative integer based on the sign of its argument.

```
print sign? 1000
1
```

```
print sign? 0
0
```

```
print sign? -1000
-1
```

The sign is returned as an integer to allow it to be used as a multiplication term within an expression:

```
val: -5
new: 2000 * sign? val
print new
-2000
```

```
size: 20
num: -30
if size > 10 [xy: 10x20 * sign? num]
print xy
-10x-20
```

## Related:

[**abs**](http://www.rebol.com/docs/words/wabs.html) - Returns the absolute value.
[**negate**](http://www.rebol.com/docs/words/wnegate.html) - Changes the sign of a number.