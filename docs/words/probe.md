# Probe - Function Summary

## Summary:

Prints a molded, unevaluated value and returns the same value.

## Usage:

**probe value**

## Arguments:

**value** - The value argument.

## Description:

Probe is very useful for debugging. Insert it anywhere a value is being passed and it will display the value without interfering with the code.

```
probe ["red" "green" "blue"]
["red" "green" "blue"]
```

```
if probe now/time > 12:00 [print "now"]
false
```

## Related:

[**mold**](http://www.rebol.com/docs/words/wmold.html) - Converts a value to a REBOL-readable string.
[**print**](http://www.rebol.com/docs/words/wprint.html) - Outputs a value followed by a line break.