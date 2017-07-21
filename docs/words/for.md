# For - Function Summary

## Summary:

Repeats a block over a range of values.

## Usage:

**for word start end bump body**

## Arguments:

**word** - Variable to hold current value (must be: word)

**start** - Starting value (must be: number series money time date char)

**end** - Ending value (must be: number series money time date char)

**bump** - Amount to skip each time (must be: number money time char)

**body** - Block to evaluate (must be: block)

## Description:

The first argument is used as a local variable to keep track of the current value. It is initially set to the START value and after each evaluation of the block the BUMP value is added to it until the END value is reached (inclusive).

```
for num 0 30 10 [ print num ]
0
10
20
30
```

```
for num 4 -37 -15 [ print num ]
4
-11
-26
```

## Related:

[**forall**](http://www.rebol.com/docs/words/wforall.html) - Evaluates a block for every value in a series.
[**foreach**](http://www.rebol.com/docs/words/wforeach.html) - Evaluates a block for each value(s) in a series.
[**forever**](http://www.rebol.com/docs/words/wforever.html) - Evaluates a block endlessly.
[**forskip**](http://www.rebol.com/docs/words/wforskip.html) - Evaluates a block for periodic values in a series.