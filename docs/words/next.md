# Next - Function Summary

## Summary:

Returns the series at its next position.

## Usage:

**next series**

## Arguments:

**series** - The series argument. (must be: series port)

## Description:

If the series is at its tail, it will remain at its tail. NEXT will not go past the tail, nor will it wrap to the head.

```
print next "ABCDE"
BCDE
```

```
print next next "ABCDE"
CDE
```

```
print next [1 2 3 4]
2 3 4
```

```
str: "REBOL"
loop length? str [
	print str
	str: next str
]
REBOL
EBOL
BOL
OL
L
```

```
blk: [red green blue]
loop length? blk [
	probe blk
	blk: next blk
]
[red green blue]
[green blue]
[blue]
```

## Related:

[**back**](http://www.rebol.com/docs/words/wback.html) - Returns the series at its previous position.
[**first**](http://www.rebol.com/docs/words/wfirst.html) - Returns the first value of a series.
[**head**](http://www.rebol.com/docs/words/whead.html) - Returns the series at its head.
[**head?**](http://www.rebol.com/docs/words/wheadq.html) - Returns TRUE if a series is at its head.
[**tail**](http://www.rebol.com/docs/words/wtail.html) - Returns the series at the position after the last value.
[**tail?**](http://www.rebol.com/docs/words/wtailq.html) - Returns TRUE if a series is at its tail.