# Comment - Function Summary

## Summary:

Ignores the argument value and returns nothing.

## Usage:

**comment value**

## Arguments:

**value** - A string, block, or any other value

## Description:

This function can be used to add comments to a script or to remove a block from evaluation. Note that this function is only effective in evaluated code and has no effect in data blocks. That is, within a data block comments will appear as data. In many cases, using COMMENT is not necessary. Placing braces around any expression will prevent if from being evaluated (so long as it is not part of another expression).

```
comment "This is a comment."
```

```
comment [print "As a comment, this is not printed"]
```

## Related:

[**do**](http://www.rebol.com/docs/words/wdo.html) - Evaluates a block, file, URL, function, word, or any other value.