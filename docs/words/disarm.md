# Disarm - Function Summary

## Summary:

Returns the error value as an object.

## Usage:

**disarm error**

## Arguments:

**error** - The error argument. (must be: error)

## Description:

DISARM allows access to the values of an error object. If the error is not disarmed, it will occur again immediately.

```
probe disarm try [1 + "x"]

make object! [
	code: 312
	type: 'script
	id: 'cannot-use
	arg1: 'add
	arg2: 'string!
	arg3: none
	near: [1 + "x"]
	where: 'do-out
]
```

The error object returned from DISARM can be used to determine the type of error and its arguments. For example in the case of a divide by zero error:

```
probe disarm try [1 / 0]

make object! [
	code: 400
	type: 'math
	id: 'zero-divide
	arg1: none
	arg2: none
	arg3: none
	near: [1 / 0]
	where: 'do-out
]
```

You might write a TRY block that handles the error after it has happened:

```
if error? err: try [
    value: 1 / 0
][
    err: disarm err
    either err/id = 'zero-divide [value: 0] [probe err quit]
]
print value
0
```

## Related:

[**attempt**](http://www.rebol.com/docs/words/wattempt.html) - Tries to evaluate and returns result or NONE on error.
[**error?**](http://www.rebol.com/docs/words/werrorq.html) - Returns TRUE for error values.
[**trace**](http://www.rebol.com/docs/words/wtrace.html) - Enables and disables evaluation tracing.
[**try**](http://www.rebol.com/docs/words/wtry.html) - Tries to DO a block and returns its value or an error.