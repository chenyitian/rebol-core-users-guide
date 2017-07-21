# While - Function Summary

## Summary:

While a condition block is TRUE, evaluates another block.

## Usage:

**while cond-block body-block**

## Arguments:

**cond-block** - The cond-block argument. (must be: block)

**body-block** - The body-block argument. (must be: block)

## Description:

The first block will be executed each time, and if it returns true the second block will be executed. Both blocks can include any number of expressions.

```
str: "string"
while [not tail? str: next str] [
	print ["length of" str "is" length? str]
]
length of tring is 5
length of ring is 4
length of ing is 3
length of ng is 2
length of g is 1
```

The most common mistake is to forget to provide a block for the first argument (the condition argument).

BREAK can be used to escape from the WHILE loop at any point.

## Related:

[**for**](http://www.rebol.com/docs/words/wfor.html) - Repeats a block over a range of values.
[**loop**](http://www.rebol.com/docs/words/wloop.html) - Evaluates a block a specified number of times.
[**repeat**](http://www.rebol.com/docs/words/wrepeat.html) - Evaluates a block a number of times or over a series.
[**until**](http://www.rebol.com/docs/words/wuntil.html) - Evaluates a block until it is TRUE. 