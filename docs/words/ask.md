# Ask - Function Summary

## Summary:

Ask the user for input.

## Usage:

**ask question**

## Arguments:

**question** - Prompt to user (must be: series)

## Refinements:

**/hide** - mask input with *

## Description:

Provides a common prompting function that is the same as a PRIN followed by an INPUT. The resulting input will have spaces trimmed from its head and tail. The /HIDE refinement hides input with "*" characters.

```
print ask "Your name, please? "
Your name, please? test
```

## Related:

[**confirm**](http://www.rebol.com/docs/words/wconfirm.html) - Confirms a user choice.
[**input**](http://www.rebol.com/docs/words/winput.html) - Inputs a string from the console. New-line character is removed.
[**prin**](http://www.rebol.com/docs/words/wprin.html) - Outputs a value with no line break.