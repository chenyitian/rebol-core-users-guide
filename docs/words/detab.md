# Detab - Function Summary

## Summary:

Converts tabs in a string to spaces. (tab size 4)

## Usage:

**detab string**

## Arguments:

**string** - The string argument. (must be: any-string)

## Refinements:

**/size** - Specifies the number of spaces per tab.

**number** - The number argument. (must be: integer)

## Description:

The REBOL language default tab size is four spaces. Use the /SIZE refinement for other sizes such as eight. DETAB will remove tabs from the entire string even beyond the first non-space character.

The series passed to this function is modified as a result.

```
text: " lots    of  tabs    here"
print detab copy text
 lots    of  tabs    here
```

```
print detab/size text 8
 lots    of  tabs    here
```

## Related:

[**entab**](http://www.rebol.com/docs/words/wentab.html) - Converts spaces in a string to tabs. (tab size 4)