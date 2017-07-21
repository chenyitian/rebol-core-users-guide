# Halt - Function Summary

## Summary:

Stops evaluation and returns to the input prompt.

## Usage:

**halt**

## Description:

Useful for program debugging.

```
div: 10
if error? try [100 / div] [
	print "math error"
	halt
]
```

## Related:

[**break**](http://www.rebol.com/docs/words/wbreak.html) - Breaks out of a loop, while, until, repeat, foreach, etc.
[**catch**](http://www.rebol.com/docs/words/wcatch.html) - Catches a throw from a block and returns its value.
[**exit**](http://www.rebol.com/docs/words/wexit.html) - Exits a function, returning no value.
[**quit**](http://www.rebol.com/docs/words/wquit.html) - Stops evaluation and exits the interpreter.