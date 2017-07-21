# Repeat - Function Summary

## Summary:

Evaluates a block a number of times or over a series.

## Usage:

**repeat word value body**

## Arguments:

**word** - Word to set each time (must be: word)

**value** - Maximum number or series to traverse (must be: integer series)

**body** - Block to evaluate each time (must be: block)

## Description:

If the value is an integer, the word is used to keep track of the current loop count, which begins at one and continues up to and including the integer value given. If the value is a series, then the word holds the first value of each element of the series (see FOREACH). Returns the value of the final evaluation. The BREAK function can be used to stop the loop at any time (but no value is returned). The word is local to the block.

```
repeat num 5 [print num]
1
2
3
4
5
```

## Related:

[**for**](http://www.rebol.com/docs/words/wfor.html) - Repeats a block over a range of values.
[**forall**](http://www.rebol.com/docs/words/wforall.html) - Evaluates a block for every value in a series.
[**foreach**](http://www.rebol.com/docs/words/wforeach.html) - Evaluates a block for each value(s) in a series.
[**forskip**](http://www.rebol.com/docs/words/wforskip.html) - Evaluates a block for periodic values in a series.
[**loop**](http://www.rebol.com/docs/words/wloop.html) - Evaluates a block a specified number of times.
[**until**](http://www.rebol.com/docs/words/wuntil.html) - Evaluates a block until it is TRUE. 
[**while**](http://www.rebol.com/docs/words/wwhile.html) - While a condition block is TRUE, evaluates another block.