# Attempt - Function Summary

## Summary:

Tries to evaluate and returns result or NONE on error.

## Usage:

**attempt value**

## Arguments:

**value** - The value argument.

## Description:

The ATTEMPT function is a shortcut for the frequent case of:

```
error? try [block]
```

The format for ATTEMPT is:

```
attempt [block]
```

ATTEMPT is useful where you either do not care about the error result or you want to make simple types of decisions based on the error.

```
attempt [make-dir %fred]
```

ATTEMPT returns the result of the block if an error did not occur. If an error did occur, a NONE is returned.

In the line:

```
value: attempt [load %data]
probe value
none
```

the value is set to NONE if the %data file cannot be loaded (e.g. it is missing or contains an error). This allows you to write conditional code such as:

```
if not value: attempt [load %data] [print "Problem"]
Problem
```

Or code such as:

```
value: any [attempt [load %data] [12 34]]
probe value
[12 34]
```

## Related:

[**error?**](http://www.rebol.com/docs/words/werrorq.html) - Returns TRUE for error values.
[**try**](http://www.rebol.com/docs/words/wtry.html) - Tries to DO a block and returns its value or an error.