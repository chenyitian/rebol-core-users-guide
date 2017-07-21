# Func - Function Summary

## Summary:

Defines a user function with given spec and body.

## Usage:

**func spec body**

## Arguments:

**spec** - Help string (opt) followed by arg words (and opt type and string) (must be: block)

**body** - The body block of the function (must be: block)

## Description:

The spec is a block that specifies the interface to the function. It can begin with an optional string which will be printed when asking for HELP on the function. That is followed by the words that specify the arguments to the function. Each of these words may include an optional block of datatypes. These specify the valid datatypes for the argument. That may be followed by a comment string which describes the argument in more detail.

The argument words may also specify a few variations on the way the argument will be evaluated. The most common is 'word which indicates that a word is expected that should not be evaluated (the function wants its name, not its value). A :word may also be given which will get the value of the argument, but not perform full evaluation.

To add refinements to a function supply a slash (/) in front of an argument's word. Within the function the refinement can be tested to determine if the refinement was present. If a refinement is followed by more arguments, they will be associated with that refinement and are only evaluated when the refinement is present.

Local variables are specified after a /LOCAL refinement.

A function returns the last expression it evaluated. You can also use RETURN and EXIT to exit the function. A RETURN is given a value to return. EXIT returns no value.

```
    sum: func [a b] [a + b]
    print sum 123 321
    444
```

```
    sum: func [nums [block!] /average /local total] [
        total: 0
        foreach num nums [total: total + num]
        either average [total / (length? nums)][total]
    ]
    print sum [123 321 456 800]
    print sum/average [123 321 456 800]
    1700
    425
```

```
    print-word: func ['word] [print form word]
    print-word testing
    testing
```

## Related:

[**does**](http://www.rebol.com/docs/words/wdoes.html) - A shortcut to define a function that has no arguments or locals.
[**exit**](http://www.rebol.com/docs/words/wexit.html) - Exits a function, returning no value.
[**function**](http://www.rebol.com/docs/words/wfunction.html) - Defines a user function with local words.
[**function?**](http://www.rebol.com/docs/words/wfunctionq.html) - Returns TRUE for function values.
[**has**](http://www.rebol.com/docs/words/whas.html) - A shortcut to define a function that has local variables but no arguments.
[**make**](http://www.rebol.com/docs/words/wmake.html) - Constructs and returns a new value.
[**return**](http://www.rebol.com/docs/words/wreturn.html) - Returns a value from a function.
[**use**](http://www.rebol.com/docs/words/wuse.html) - Defines words local to a block.