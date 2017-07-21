# Get - Function Summary

## Summary:

Gets the value of a word.

## Usage:

**get word**

## Arguments:

**word** - Word to get (must be: any-word none)

## Refinements:

**/any** - Allows any type of value, even unset.

## Description:

The argument to GET must be a word, so the argument must be quoted or extracted from a block. To get the value of a word residing in an object, use the IN function.

```
value: 123
print get 'value
123
```

```
print get second [the value here]
123
```

```
print get in system/console 'prompt
>>
```

## Related:

[**in**](http://www.rebol.com/docs/words/win.html) - Returns the word in the object's context.
[**set**](http://www.rebol.com/docs/words/wset.html) - Sets a word or block of words to specified value(s).
[**value?**](http://www.rebol.com/docs/words/wvalueq.html) - Returns TRUE if the word has been set.