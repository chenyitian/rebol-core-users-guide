# Unset - Function Summary

## Summary:

Unsets the value of a word.

## Usage:

**unset word**

## Arguments:

**word** - Word or block of words (must be: word block)

## Description:

Using UNSET, the word's current value will be lost. If a block is specified, all the words within the block will be unset.

```
    test: "a value"
    unset 'test
    print value? 'test
    false
```

## Related:

[**set**](http://www.rebol.com/docs/words/wset.html) - Sets a word or block of words to specified value(s).