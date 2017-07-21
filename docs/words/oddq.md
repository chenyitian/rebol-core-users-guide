# Odd? - Function Summary

## Summary:

Returns TRUE if the number is odd.

## Usage:

**odd? number**

## Arguments:

**number** - The number argument. (must be: number char date money time)

## Description:

Returns TRUE only if the argument is an odd integer value. If the argument is a decimal, only its integer portion is examined.

```
print odd? 3
true
```

```
print odd? 100
false
```

```
print odd? 0
false
```

## Related:

[**even?**](http://www.rebol.com/docs/words/wevenq.html) - Returns TRUE if the number is even.