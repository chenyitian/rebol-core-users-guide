# Forskip - Function Summary

## Summary:

Evaluates a block for periodic values in a series.

## Usage:

**forskip word skip-num body**

## Arguments:

**word** - Word set to each position in series and changed as a result (must be: word)

**skip-num** - Number of values to skip each time (must be: integer)

**body** - Block to evaluate each time (must be: block)

## Description:

Prior to evaluation, the word must be set to the desired starting position within the series (normally the head, but any position is valid). After each evaluation of the block, the word's position in the series is changed by skipping the number of values specified by the second argument (see the SKIP function).

```
areacodes: [
	"Ukiah"         707
	"San Francisco" 415
	"Sacramento"    916
]
forskip areacodes 2 [
	print [ first areacodes "area code is" second areacodes]
]
Ukiah area code is 707
San Francisco area code is 415
Sacramento area code is 916
```

## Related:

[**for**](http://www.rebol.com/docs/words/wfor.html) - Repeats a block over a range of values.
[**forall**](http://www.rebol.com/docs/words/wforall.html) - Evaluates a block for every value in a series.
[**foreach**](http://www.rebol.com/docs/words/wforeach.html) - Evaluates a block for each value(s) in a series.
[**skip**](http://www.rebol.com/docs/words/wskip.html) - Returns the series forward or backward from the current position.