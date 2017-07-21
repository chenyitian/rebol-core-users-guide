# Not - Function Summary

## Summary:

Returns the logic complement.

## Usage:

**not value**

## Arguments:

**value** - (Only FALSE and NONE return TRUE)

## Description:

Function returns TRUE if the value is FALSE, and FALSE if it is TRUE. To bitwise complement an INTEGER, use the COMPLEMENT function.

```
print not true
false
```

```
print not (10 = 1)
true
```

## Related:

[**and**](http://www.rebol.com/docs/words/wand.html) - Returns the first value ANDed with the second.
[**or**](http://www.rebol.com/docs/words/wor.html) - Returns the first value ORed with the second.
[**xor**](http://www.rebol.com/docs/words/wxor.html) - Returns the first value exclusive ORed with the second.