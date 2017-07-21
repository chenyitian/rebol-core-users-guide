# Xor - Function Summary

## Summary:

Returns the first value exclusive ORed with the second.

## Usage:

**xor value1 value2**

## Arguments:

**value1** - The value1 argument. (must be: logic number char tuple binary image)

**value2** - The value2 argument. (must be: logic number char tuple binary image)

## Description:

For integers, each bit is exclusively-or'd. For logic values, this is the same as the not-equal function.

```
print 122 xor 1
123
```

```
print true xor false
true
```

```
print false xor false
false
```

```
print 1.2.3.4 xor 1.0.0.0
0.2.3.4
```

## Related:

[**and**](http://www.rebol.com/docs/words/wand.html) - Returns the first value ANDed with the second.
[**not**](http://www.rebol.com/docs/words/wnot.html) - Returns the logic complement.
[**or**](http://www.rebol.com/docs/words/wor.html) - Returns the first value ORed with the second.