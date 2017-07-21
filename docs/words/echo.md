# Echo - Function Summary

## Summary:

Copies console output to a file.

## Usage:

**echo target**

## Arguments:

**target** - The target argument. (must be: file none logic)

## Description:

Write output to a file in addition to the user console. The previous contents of a file will be overwritten. The echo can be stopped with ECHO NONE or by starting another ECHO.

```
echo %helloworld.txt
print "Hello World!"
echo none
Hello World!
```

## Related:

[**print**](http://www.rebol.com/docs/words/wprint.html) - Outputs a value followed by a line break.
[**trace**](http://www.rebol.com/docs/words/wtrace.html) - Enables and disables evaluation tracing.