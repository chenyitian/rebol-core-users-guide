# Confirm - Function Summary

## Summary:

Confirms a user choice.

## Usage:

**confirm question**

## Arguments:

**question** - Prompt to user (must be: series)

## Refinements:

**/with** - The with refinement.

**choices** - The choices argument. (must be: string block)

## Description:

This function provides a method of prompting the user for a TRUE ("y" or "yes") or FALSE ("n" or "no") response. Alternate responses can be identified with the /WITH refinement.

```
confirm "Answer: 14. Y or N? "
```

```
confirm/with "Use A or B? " ["A" "B"]
```

## Related:

[**ask**](http://www.rebol.com/docs/words/wask.html) - Ask the user for input.
[**input**](http://www.rebol.com/docs/words/winput.html) - Inputs a string from the console. New-line character is removed.
[**prin**](http://www.rebol.com/docs/words/wprin.html) - Outputs a value with no line break.