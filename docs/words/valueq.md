# Value? - Function Summary

## Summary:

Returns TRUE if the word has been set.

## Usage:

**value? value**

## Arguments:

**value** - The value argument.

## Description:

Returns FALSE for all other values. The word can be passed as a literal or as the result of other operations.

```
test: 1234
print value? 'test
true
```

```
print value? second [test this]
false
```

## Related:

[**equal?**](http://www.rebol.com/docs/words/wequalq.html) - Returns TRUE if the values are equal.
[**same?**](http://www.rebol.com/docs/words/wsameq.html) - Returns TRUE if the values are identical.
[**strict-equal?**](http://www.rebol.com/docs/words/wstrict-equalq.html) - Returns TRUE if the values are equal and of the same datatype.
[**unset?**](http://www.rebol.com/docs/words/wunsetq.html) - Returns TRUE for unset values.