# Catch - Function Summary

## Summary:

Catches a throw from a block and returns its value.

## Usage:

**catch block**

## Arguments:

**block** - Block to evaluate (must be: block)

## Refinements:

**/name** - Catches a named throw.

**word** - One or more names (must be: word block)

## Description:

CATCH and THROW go together. They provide a way to exit from a block without evaluating the rest of the block. To use it, provide CATCH with a block to evaluate. If within that block a THROW is evaluated, it will return from the CATCH at that point. The result of the CATCH will be whatever was passed as the argument to the THROW. When using multiple CATCH functions, provide them with a name using the /NAME refinement to identify which one will CATCH which THROW.

```
write %file.txt "i am a happy little file with no real purpose"
print catch [
	if exists? %file.txt [throw "Doc found"]
	"Doc not found"
]
Doc found
```

## Related:

[**do**](http://www.rebol.com/docs/words/wdo.html) - Evaluates a block, file, URL, function, word, or any other value.
[**throw**](http://www.rebol.com/docs/words/wthrow.html) - Throws control back to a previous catch.
[**try**](http://www.rebol.com/docs/words/wtry.html) - Tries to DO a block and returns its value or an error.