# Loop - Function Summary

## Summary:

Evaluates a block a specified number of times.

## Usage:

**loop count block**

## Arguments:

**count** - Number of repetitions (must be: integer)

**block** - Block to evaluate (must be: block)

## Description:

Repeatedly executes a block for the given number of times. When finished, the LOOP function returns the value of the final execution of the block.

```
loop 40 [prin "*"]
print ""
****************************************
```

The BREAK function can be used to stop the loop at any time (but no value is returned).

The REPEAT function is similar to LOOP, except that it keeps track of the current loop count with a variable.

The LOOP function is very efficient, and should be used if no loop counter is required.

## Related:

[**break**](http://www.rebol.com/docs/words/wbreak.html) - Breaks out of a loop, while, until, repeat, foreach, etc.
[**for**](http://www.rebol.com/docs/words/wfor.html) - Repeats a block over a range of values.
[**repeat**](http://www.rebol.com/docs/words/wrepeat.html) - Evaluates a block a number of times or over a series.
[**until**](http://www.rebol.com/docs/words/wuntil.html) - Evaluates a block until it is TRUE. 
[**while**](http://www.rebol.com/docs/words/wwhile.html) - While a condition block is TRUE, evaluates another block.