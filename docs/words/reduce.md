# Reduce - Function Summary

## Summary:

Evaluates an expression or block expressions and returns the result.

## Usage:

**reduce value**

## Arguments:

**value** - The value argument.

## Description:

When given a block, evaluates each of its expressions and returns a block with all of the results. Very useful for composing blocks of values.

```
values: reduce [1 + 2 3 + 4]
probe values
[3 7]
```

The REDUCE function is a major element of the REBOL language because it allows you to initialize blocks with values that must be computed. For example:

```
file: %comments.r
info: reduce [now/date size? file modified? file]
probe info
[9-Mar-2004 2966 24-Jan-2003/22:53:58-8:00]
```

## Related:

[**compose**](http://www.rebol.com/docs/words/wcompose.html) - Evaluates a block of expressions, only evaluating parens, and returns a block.
[**do**](http://www.rebol.com/docs/words/wdo.html) - Evaluates a block, file, URL, function, word, or any other value.
[**foreach**](http://www.rebol.com/docs/words/wforeach.html) - Evaluates a block for each value(s) in a series.