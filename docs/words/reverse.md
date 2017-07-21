# Reverse - Function Summary

## Summary:

Reverses a series.

## Usage:

**reverse value**

## Arguments:

**value** - The value argument. (must be: series tuple pair)

## Refinements:

**/part** - Limits to a given length or position.

**range** - The range argument. (must be: integer series)

## Description:

Reverses the order of elements in a series or tuple.

```
blk: [1 2 3 4 5 6]
reverse blk
print blk
6 5 4 3 2 1
```

The /PART refinement reverses the specified number of elements from the current index forward. If the number of elements specified exceeds the number of elements left in the series or tuple, the elements from the current index to the end will be reversed.

```
text: "It is possible to reverse one word in a sentence."
reverse/part (find text "reverse") (length? "reverse")
print text
It is possible to esrever one word in a sentence.
```

Note that reverse returns the position just past the reverse operation.

```
blk: [1 2 3 4 5 6]
print reverse/part blk 4
5 6
```

For tuple values the current index cannot be moved so the current index is always the beginning of the tuple.

```
print reverse 1.2.3.4
4.3.2.1
```

```
print reverse/part 1.2.3.4 2
2.1.3.4
```

## Related:

[**find**](http://www.rebol.com/docs/words/wfind.html) - Finds a value in a series and returns the series at the start of it.
[**insert**](http://www.rebol.com/docs/words/winsert.html) - Inserts a value into a series and returns the series after the insert.
[**replace**](http://www.rebol.com/docs/words/wreplace.html) - Replaces the search value with the replace value within the target series.
[**sort**](http://www.rebol.com/docs/words/wsort.html) - Sorts a series.