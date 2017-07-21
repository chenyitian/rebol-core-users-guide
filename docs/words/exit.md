# Exit - Function Summary

## Summary:

Exits a function, returning no value.

## Usage:

**exit**

## Description:

EXIT is used to return from a function without returning a value.

```
test-str: make function! [str] [
    if not string? str [exit]
    print str
]
test-str 10
test-str "right"
right
```

Note: Use QUIT to exit the interpreter.

## Related:

[**break**](http://www.rebol.com/docs/words/wbreak.html) - Breaks out of a loop, while, until, repeat, foreach, etc.
[**catch**](http://www.rebol.com/docs/words/wcatch.html) - Catches a throw from a block and returns its value.
[**return**](http://www.rebol.com/docs/words/wreturn.html) - Returns a value from a function.