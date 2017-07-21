# Throw - Function Summary

## Summary:

Throws control back to a previous catch.

## Usage:

**throw value**

## Arguments:

**value** - Value returned from catch (must be: any-type)

## Refinements:

**/name** - Throws to a named catch.

**word** - The word argument. (must be: word)

## Description:

CATCH and THROW go together. They provide a method of exiting from a block without evaluating the rest of the block. To use it, provide CATCH with a block to evaluate. If within that block a THROW is evaluated, the script will return from the CATCH at that point. The result of the CATCH will be the value that was passed as the argument to the THROW. When using multiple CATCH functions, provide them with a name to identify which one will CATCH which THROW.

```
print catch [
	if exists? %file.txt [throw "Doc file!"]
]
Doc file!
```

## Related:

[**catch**](http://www.rebol.com/docs/words/wcatch.html) - Catches a throw from a block and returns its value.
[**exit**](http://www.rebol.com/docs/words/wexit.html) - Exits a function, returning no value.
[**return**](http://www.rebol.com/docs/words/wreturn.html) - Returns a value from a function.