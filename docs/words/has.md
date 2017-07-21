# Has - Function Summary

## Summary:

A shortcut to define a function that has local variables but no arguments.

## Usage:

**has locals body**

## Arguments:

**locals** - The locals argument. (must be: block)

**body** - The body argument. (must be: block)

## Description:

Defines a function that consists of local variables only. This is a shortcut for FUNC and FUNCTION.

For example:

```
ask-name: has [name] [
	name: ask "What is your name?"
	print ["Hello" name]
]
```

```
ask-name
What is your name?Hello test
```

The example above is a shortcut for:

```
ask-name: func [/local name] [...]
```

## Related:

[**does**](http://www.rebol.com/docs/words/wdoes.html) - A shortcut to define a function that has no arguments or locals.
[**exit**](http://www.rebol.com/docs/words/wexit.html) - Exits a function, returning no value.
[**func**](http://www.rebol.com/docs/words/wfunc.html) - Defines a user function with given spec and body.
[**function**](http://www.rebol.com/docs/words/wfunction.html) - Defines a user function with local words.
[**return**](http://www.rebol.com/docs/words/wreturn.html) - Returns a value from a function.
[**use**](http://www.rebol.com/docs/words/wuse.html) - Defines words local to a block.