# Set - Function Summary

## Summary:

Sets a word or block of words to specified value(s).

## Usage:

**set word value**

## Arguments:

**word** - Word or words to set (must be: any-word block)

**value** - Value or block of values (must be: any-type)

## Refinements:

**/any** - Allows setting words to any value.

## Description:

If the first argument is a block of words and the value is not a block, all of the words in the block will be set to the specified value. If the value is a block, then each of the words in the first block will be set to the respective values in the second block. If there are not enough values in the second block, the remaining words will be set to NONE

The /ANY refinementallows words to be set any datatype including those such as UNSET! that are not normally allowed. This is useful in situations where all values must be handled.

```
set 'test 1234
print test
1234
```

```
set [a b] 123
print a
123
```

```
print b
123
```

```
set [d e] [1 2]
print d
1
```

```
print e
2
```

## Related:

[**get**](http://www.rebol.com/docs/words/wget.html) - Gets the value of a word.
[**in**](http://www.rebol.com/docs/words/win.html) - Returns the word in the object's context.
[**unset**](http://www.rebol.com/docs/words/wunset.html) - Unsets the value of a word.
[**value?**](http://www.rebol.com/docs/words/wvalueq.html) - Returns TRUE if the word has been set.