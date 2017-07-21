# Does - Function Summary

## Summary:

A shortcut to define a function that has no arguments or locals.

## Usage:

**does body**

## Arguments:

**body** - The body block of the function (must be: block)

## Description:

DOES provides a shortcut for defining functions that have no arguments or local variables.

```
rand10: does [random 10]
print rand10
5
```

```
this-month: does [now/month]
print this-month
3
```

This function is provided as a coding convenience and it is otherwise identical to using FUNC or FUNCTION.

## Related:

[**exit**](http://www.rebol.com/docs/words/wexit.html) - Exits a function, returning no value.
[**func**](http://www.rebol.com/docs/words/wfunc.html) - Defines a user function with given spec and body.
[**function**](http://www.rebol.com/docs/words/wfunction.html) - Defines a user function with local words.
[**has**](http://www.rebol.com/docs/words/whas.html) - A shortcut to define a function that has local variables but no arguments.
[**return**](http://www.rebol.com/docs/words/wreturn.html) - Returns a value from a function.
[**use**](http://www.rebol.com/docs/words/wuse.html) - Defines words local to a block.