# Forever - Function Summary

## Summary:

Evaluates a block endlessly.

## Usage:

**forever body**

## Arguments:

**body** - Block to evaluate each time (must be: block)

## Description:

Evaluates a block continuously, or until a break or error condition is met.

```
forever [
	if (random 10) > 5 [break]
]
```

## Related:

[**loop**](http://www.rebol.com/docs/words/wloop.html) - Evaluates a block a specified number of times.
[**until**](http://www.rebol.com/docs/words/wuntil.html) - Evaluates a block until it is TRUE. 
[**while**](http://www.rebol.com/docs/words/wwhile.html) - While a condition block is TRUE, evaluates another block.