# Return - Function Summary

## Summary:

Returns a value from a function.

## Usage:

**return value**

## Arguments:

**value** - The value argument. (must be: any-type)

## Description:

Exits the current function immediately, returning a value as the result of the function. To return no value, use the EXIT function.

```
fun: make function! [this-time] [
	return either this-time >= 12:00 ["after noon"]["before noon"]
]
print fun 9:00
before noon
```

```
print fun 18:00
after noon
```

## Related:

[**break**](http://www.rebol.com/docs/words/wbreak.html) - Breaks out of a loop, while, until, repeat, foreach, etc.
[**catch**](http://www.rebol.com/docs/words/wcatch.html) - Catches a throw from a block and returns its value.
[**exit**](http://www.rebol.com/docs/words/wexit.html) - Exits a function, returning no value.