# Trace - Function Summary

## Summary:

Enables and disables evaluation tracing.

## Usage:

**trace mode**

## Arguments:

**mode** - The mode argument. (must be: logic)

## Refinements:

**/net** - Enable/disable network tracing.

**/function** - Enable/disable function call tracing.

## Description:

Used for debugging a script. TRACE ON turns it on. TRACE OFF turns it off. To limit the amount of output selective place trace around the parts of the script that need it. TRACE/NET allows watching what the network protocols are doing.

## Related:

[**echo**](http://www.rebol.com/docs/words/wecho.html) - Copies console output to a file.
[**probe**](http://www.rebol.com/docs/words/wprobe.html) - Prints a molded, unevaluated value and returns the same value.