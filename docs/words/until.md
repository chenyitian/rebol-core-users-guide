# Until - Function Summary

## Summary:

Evaluates a block until it is TRUE.

## Usage:

**until block**

## Arguments:

**block** - The block argument. (must be: block)

## Description:

Evaluates a block until the block returns a TRUE value (that is, the last expression in the block is TRUE).

```
str: "string"
until [
	print str
	tail? str: next str
]
string
tring
ring
ing
ng
g
```

## Related:

[**for**](http://www.rebol.com/docs/words/wfor.html) - Repeats a block over a range of values.
[**repeat**](http://www.rebol.com/docs/words/wrepeat.html) - Evaluates a block a number of times or over a series.
[**while**](http://www.rebol.com/docs/words/wwhile.html) - While a condition block is TRUE, evaluates another block.