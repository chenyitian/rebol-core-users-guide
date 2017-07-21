# Remove-each - Function Summary

## Summary:

Removes a value from a series for each block that returns TRUE.

## Usage:

**remove-each word data body**

## Arguments:

**word** - Word or block of words to set each time (will be local) (must be: get-word word block)

**data** - The series to traverse (must be: series)

**body** - Block to evaluate. Return TRUE to remove. (must be: block)

## Description:

REMOVE-EACH is similar to FOREACH, but removes values as it moves through a series. For each value in the series, a comparison block is executed. If the block returns true, then the value will be removed.

```
values: [12 test 30 "C" "D" 10]
remove-each value values [word? value]
probe values
[12 30 "C" "D" 10]
```

```
remove-each value values [all [integer? value value > 11]]
probe values
["C" "D" 10]
```

Using REMOVE-EACH for removing values provides much greater performance than using a WHILE or FORALL loop.

This function is not available in older versions of REBOL.

## Related:

[**foreach**](http://www.rebol.com/docs/words/wforeach.html) - Evaluates a block for each value(s) in a series.
[**remove**](http://www.rebol.com/docs/words/wremove.html) - Removes value(s) from a series and returns after the remove.