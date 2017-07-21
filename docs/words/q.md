# ? - Function Summary

## Summary:

Prints information about words and values.

## Usage:

**? word**

## Arguments:

**word** - The word argument. (must be: any-type)

## Description:

Synonym for HELP.

```
? switch
USAGE:
	SWITCH value cases /default case 

DESCRIPTION:
	Selects a choice and evaluates what follows it. 
	SWITCH is a function value.

	ARGUMENTS:
		value -- Value to search for. (Type: any)
		cases -- Block of cases to search. (Type: block)

	REFINEMENTS:
		/default
				case -- Default case if no others are found. (Type: any)

(SPECIAL ATTRIBUTES)
	throw
```

## Related:

[**help**](http://www.rebol.com/docs/words/whelp.html) - Prints information about words and values.
[**source**](http://www.rebol.com/docs/words/wsource.html) - Prints the source code for a word.
[**what**](http://www.rebol.com/docs/words/wwhat.html) - Prints a list of globally-defined functions.