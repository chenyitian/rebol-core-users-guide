# Break - Function Summary

## Summary:

Breaks out of a loop, while, until, repeat, foreach, etc.

## Usage:

**break**

## Refinements:

**/return** - Forces the loop function to return a value.

**value** - The value argument. (must be: any-type)

## Description:

The current loop is immediately terminated and evaluation resumes after the LOOP function. This function can be placed anywhere within the block being repeated, even within a sub block or function.

```
repeat n 5 [
	print n
	if n > 3 [break]
]
1
2
3
4
```

## Related:

[**catch**](http://www.rebol.com/docs/words/wcatch.html) - Catches a throw from a block and returns its value.
[**exit**](http://www.rebol.com/docs/words/wexit.html) - Exits a function, returning no value.
[**for**](http://www.rebol.com/docs/words/wfor.html) - Repeats a block over a range of values.
[**forall**](http://www.rebol.com/docs/words/wforall.html) - Evaluates a block for every value in a series.
[**foreach**](http://www.rebol.com/docs/words/wforeach.html) - Evaluates a block for each value(s) in a series.
[**forever**](http://www.rebol.com/docs/words/wforever.html) - Evaluates a block endlessly.
[**forskip**](http://www.rebol.com/docs/words/wforskip.html) - Evaluates a block for periodic values in a series.
[**loop**](http://www.rebol.com/docs/words/wloop.html) - Evaluates a block a specified number of times.
[**repeat**](http://www.rebol.com/docs/words/wrepeat.html) - Evaluates a block a number of times or over a series.
[**return**](http://www.rebol.com/docs/words/wreturn.html) - Returns a value from a function.
[**until**](http://www.rebol.com/docs/words/wuntil.html) - Evaluates a block until it is TRUE. 
[**while**](http://www.rebol.com/docs/words/wwhile.html) - While a condition block is TRUE, evaluates another block.