# Either - Function Summary

## Summary:

If condition is TRUE, evaluates the first block, else evaluates the second.

## Usage:

**either condition true-block false-block**

## Arguments:

**condition** - The condition argument.

**true-block** - The true-block argument. (must be: block)

**false-block** - The false-block argument. (must be: block)

## Description:

Evaluate either one block or the other depending on a condition. EITHER is identical to the if-else style comparison in other languages.

```
grade: 72
either grade > 60 [
    print "Passing Grade!"
][
    print "Failing Grade!"
]
Passing Grade!
```

The EITHER function also returns the result of the block that it evaluates.

```
print either grade > 60 ["Passing"]["Failing"]
Passing
```

## Related:

[**if**](http://www.rebol.com/docs/words/wif.html) - If condition is TRUE, evaluates the block.
[**pick**](http://www.rebol.com/docs/words/wpick.html) - Returns the value at the specified position in a series.