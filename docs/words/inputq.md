# Input? - Function Summary

## Summary:

Returns TRUE if input characters are available.

## Usage:

**input?**

## Description:

INPUT? can be used to determine if input is waiting to be read from the standard input device. When it returns TRUE, input is waiting to be read (with INPUT).

```
print input?
false
```

```
if input? [name: input]
```

## Related:

[**input**](http://www.rebol.com/docs/words/winput.html) - Inputs a string from the console. New-line character is removed.