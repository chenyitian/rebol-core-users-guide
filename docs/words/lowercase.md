# Lowercase - Function Summary

## Summary:

Converts string of characters to lowercase.

## Usage:

**lowercase string**

## Arguments:

**string** - The string argument. (must be: any-string)

## Refinements:

**/part** - Limits to a given length or position.

**range** - The range argument. (must be: integer any-string)

## Description:

The series passed to this function is modified as a result.

```
print lowercase "ABCDEF"
abcdef
```

```
print lowercase/part "ABCDEF" 3
abcDEF
```

## Related:

[**trim**](http://www.rebol.com/docs/words/wtrim.html) - Removes whitespace from a string. Default removes from head and tail.
[**uppercase**](http://www.rebol.com/docs/words/wuppercase.html) - Converts string of characters to uppercase.