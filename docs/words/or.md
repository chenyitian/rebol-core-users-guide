# Or - Function Summary

## Summary:

Returns the first value ORed with the second.

## Usage:

**or value1 value2**

## Arguments:

**value1** - The value1 argument. (must be: logic number char tuple binary image)

**value2** - The value2 argument. (must be: logic number char tuple binary image)

## Description:

An infix-operator. For LOGIC values, both must be FALSE to return FALSE; otherwise a TRUE is returned. For integers, each bit is separately affected. Because it is an infix operator, OR must be between the two values.

```
print true or false
true
```

```
print (10 > 20) or (20 < 100)
true
```

```
print 122 or 1
123
```

```
print 1.2.3.4 or 255.255.255.0
255.255.255.4
```

## Related:

[**and**](http://www.rebol.com/docs/words/wand.html) - Returns the first value ANDed with the second.
[**not**](http://www.rebol.com/docs/words/wnot.html) - Returns the logic complement.
[**xor**](http://www.rebol.com/docs/words/wxor.html) - Returns the first value exclusive ORed with the second.