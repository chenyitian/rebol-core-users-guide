# Source - Function Summary

## Summary:

Prints the source code for a word.

## Usage:

**source word**

## Arguments:

**word** - The word argument. (must be: word)

## Description:

Displays the source code for a function by molding it in a formatted manner from the internal loaded block strucures. Only provides the source code to REBOL defined functions, not native (machine code) functions.

This function is useful for learning how mezzanine (higher level) functions are defined.

```
source source
source: func [
	"Prints the source code for a word." 
	'word [word!]][
	prin join word ": " 
	if not value? word [print "undefined" exit] 
	either any [native? get word op? get word action? get word] [
		print ["native" mold third get word]] [print mold get word]]
```

If the function specified is a native, SOURCE returns the function's argument specification.

```
source copy
copy: native [
	"Returns a copy of a value." 
	value [series! port! bitset!] "Usually a series" 
	/part "Limits to a given length or position." 
	range [number! series! port! pair!] 
	/deep "Also copies series values within the block."
]
```

## Related:

[**?**](http://www.rebol.com/docs/words/wq.html) - Prints information about words and values.
[**help**](http://www.rebol.com/docs/words/whelp.html) - Prints information about words and values.