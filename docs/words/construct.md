# Construct - Function Summary

## Summary:

Creates an object, but without evaluating its specification.

## Usage:

**construct block**

## Arguments:

**block** - Object specification block (must be: block)

## Refinements:

**/with** - Provide a default base object

**object** - The object argument. (must be: object)

## Description:

This function creates new objects but without evaluating the object's specification (as is done in the MAKE and CONTEXT functions).

When you CONSTRUCT an object, only literal types are accepted. Functional evaluation is not performed. This allows your code to directly import objects (such as those sent from unsafe external sources such as email, cgi, etc.) without concern that they may include "hidden" side effects using executable code.

CONSTRUCT is used in the same way as the CONTEXT function:

```
obj: construct [
	name: "Fred"
	age: 27
	city: "Ukiah"
]
probe obj

make object! [
	name: "Fred"
	age: 27
	city: "Ukiah"
]
```

But, very limited evaluation takes place. That means object specifications like:

```
obj: construct [
	name: uppercase "Fred"
	age: 20 + 7
	time: now
]
probe obj

make object! [
	name: 'uppercase
	age: 20
	time: 'now
]
```

do not produce evaluated results.

The CONSTRUCT function only performs evaluation on the words TRUE, FALSE, NONE, ON, and OFF to produce their expected values. Literal words and paths will also be evaluated to produce their respective words and paths. For example:

```
obj: construct [
	a: true
	b: none
	c: 'word
]
probe obj

make object! [
	a: true
	b: none
	c: 'word
]
```

The CONSTRUCT function is useful for importing external objects, such as preference settings from a file, CGI query responses, encoded email, etc.

To provide a template object that contains default variable values (similar to MAKE), use the /WITH refinement. The example below would use an existing object called standard-prefs as the template.

```
;prefs: construct/with load %prefs.r standard-prefs
```

## Related:

[**context**](http://www.rebol.com/docs/words/wcontext.html) - Defines a unique (underived) object.
[**make**](http://www.rebol.com/docs/words/wmake.html) - Constructs and returns a new value.