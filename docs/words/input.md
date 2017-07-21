# Input - Function Summary

## Summary:

Inputs a string from the console. New-line character is removed.

## Usage:

**input**

## Refinements:

**/hide** - Mask input with a * character

## Description:

Returns a string from the standard input device (normally the keyboard, but can also be a file or an interactive shell). The string does not include the new-line character used to terminate it.

The /HIDE refinement hides input with "*" characters.

```
prin "Enter a name: "
name: input
print [name "is" length? name "characters long"]
Enter a name: test is 4 characters long
```

## Related:

[**ask**](http://www.rebol.com/docs/words/wask.html) - Ask the user for input.
[**confirm**](http://www.rebol.com/docs/words/wconfirm.html) - Confirms a user choice.
[**input?**](http://www.rebol.com/docs/words/winputq.html) - Returns TRUE if input characters are available.