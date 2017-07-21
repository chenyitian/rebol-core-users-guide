# Dump-face - Function Summary

## Summary:

Print face info for entire pane. (for debugging)

## Usage:

**dump-face face**

## Arguments:

**face** - The face argument. (must be: object)

## Description:

This function provides an easy way to view the structure of a face object and its sub-faces. It is an alternative to MOLD and PROBE which may display far too much information.

```
out-face: layout [
	h2 "Testing"
]
print dump-face out-face
Style: none Offset: 25x25 Size: 103x63 Text: none
	Style: h2 Offset: 20x20 Size: 63x23 Text: Testing
```

## Related:

[**?**](http://www.rebol.com/docs/words/wq.html) - Prints information about words and values.
[**??**](http://www.rebol.com/docs/words/wqq.html) - Prints a variable name followed by its molded value. (for debugging)
[**dump-obj**](http://www.rebol.com/docs/words/wdump-obj.html) - Returns a block of information about an object.
[**help**](http://www.rebol.com/docs/words/whelp.html) - Prints information about words and values.