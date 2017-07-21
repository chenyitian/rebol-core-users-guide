# Function - Function Summary

## Summary:

Defines a user function with local words.

## Usage:

**function spec vars body**

## Arguments:

**spec** - Optional help info followed by arg words (and optional type and string) (must be: block)

**vars** - List of words that are local to the function (must be: block)

**body** - The body block of the function (must be: block)

## Description:

FUNCTION is identical to FUNC but includes a block in which you can name words considered LOCAL to the function.

```
average: function [block] [total] [
	total: 0
	foreach number block [total: number + total]
	total / (length? block)
]
print average [1 10 12.34]
7.78
```

## Related:

[**does**](http://www.rebol.com/docs/words/wdoes.html) - A shortcut to define a function that has no arguments or locals.
[**exit**](http://www.rebol.com/docs/words/wexit.html) - Exits a function, returning no value.
[**func**](http://www.rebol.com/docs/words/wfunc.html) - Defines a user function with given spec and body.
[**function?**](http://www.rebol.com/docs/words/wfunctionq.html) - Returns TRUE for function values.
[**has**](http://www.rebol.com/docs/words/whas.html) - A shortcut to define a function that has local variables but no arguments.
[**make**](http://www.rebol.com/docs/words/wmake.html) - Constructs and returns a new value.
[**return**](http://www.rebol.com/docs/words/wreturn.html) - Returns a value from a function.
[**use**](http://www.rebol.com/docs/words/wuse.html) - Defines words local to a block.