# Uppercase - Function Summary

## Summary:

Converts string of characters to uppercase.

## Usage:

**uppercase string**

## Arguments:

**string** - The string argument. (must be: any-string)

## Refinements:

**/part** - Limits to a given length or position.

**range** - The range argument. (must be: integer any-string)

## Description:

The series passed to this function is modified as a result.

```
print uppercase "abcdef"
ABCDEF
```

```
print uppercase/part "abcdef" 1
Abcdef
```

## Related:

[**lowercase**](http://www.rebol.com/docs/words/wlowercase.html) - Converts string of characters to lowercase.
[**trim**](http://www.rebol.com/docs/words/wtrim.html) - Removes whitespace from a string. Default removes from head and tail.