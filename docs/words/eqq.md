# =? - Function Summary

------

## Summary:

Returns TRUE if the values are identical.

## Usage:

**=? value1 value2**

## Arguments:

**value1** - The value1 argument.

**value2** - The value2 argument.

## Description:

This function returns true if two values are the same. That is, there is no way to distinguish between them. For instance, in the case of a string, they would occupy the same memory.

```
a: "apple"
b: a
print a =? b
true
```

```
b: tail a
print a =? (head b)
true
```

```
print "apple" =? "apple"
false
```

## Related:

[**=**](http://www.rebol.com/docs/words/weq.html) - Returns TRUE if the values are equal.
[**==**](http://www.rebol.com/docs/words/weqeq.html) - Returns TRUE if the values are equal and of the same datatype.
[**same?**](http://www.rebol.com/docs/words/wsameq.html) - Returns TRUE if the values are identical.