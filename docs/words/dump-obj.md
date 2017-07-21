# Dump-obj - Function Summary

## Summary:

Returns a block of information about an object.

## Usage:

**dump-obj obj**

## Arguments:

**obj** - The obj argument. (must be: object)

## Refinements:

**/match** - Include only those that match a string or datatype

**pat** - The pat argument.

## Description:

This function provides an easy way to view the contents of an object. It is an alternative to MOLD and PROBE which may display too much information for deeply structured objects.

```
print dump-obj system/error
	throw           object!   [code type no-loop no-function nocatch] 
	note            object!   [code type no-load exited] 
	syntax          object!   [code type invalid missing header] 
	script          object!   [code type no-value need-value no-argexpect-arg e... 
	math            object!   [code type zero-divide overflow positive] 
	access          object!   [code type cannot-open not-open already-open alrea... 
	command         object!   [code type fmt-too-short fmt-no-struct-size fmt-no... 
	resv700         none!     none 
	user            object!   [code type message] 
	internal        object!   [code type bad-path not-here stack-overflow global...
```

## Related:

[**?**](http://www.rebol.com/docs/words/wq.html) - Prints information about words and values.
[**??**](http://www.rebol.com/docs/words/wqq.html) - Prints a variable name followed by its molded value. (for debugging)
[**help**](http://www.rebol.com/docs/words/whelp.html) - Prints information about words and values.