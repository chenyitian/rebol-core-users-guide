# If - Function Summary

## Summary:

If condition is TRUE, evaluates the block.

## Usage:

**if condition then-block**

## Arguments:

**condition** - The condition argument.

**then-block** - The then-block argument. (must be: block)

## Refinements:

**/else** - If not true, evaluate this block

**else-block** - The else-block argument. (must be: block)

## Description:

Skip the block if the value is FALSE. To select an alternate result (else) use the EITHER function. IF returns the value of the block it evaluated or NONE otherwise.

```
age: 4
if age > 3 [print "wine is ready"]
wine is ready
```

```
print if age > 2 ["ready"]
ready
```

```
print if age < 2 ["not ready"]
none
```

A common error is to add a block without specifying /else or without using the EITHER function. The extra block gets ignored.

## Related:

[**either**](http://www.rebol.com/docs/words/weither.html) - If condition is TRUE, evaluates the first block, else evaluates the second.
[**select**](http://www.rebol.com/docs/words/wselect.html) - Finds a value in the series and returns the value or series after it.
[**switch**](http://www.rebol.com/docs/words/wswitch.html) - Selects a choice and evaluates what follows it.