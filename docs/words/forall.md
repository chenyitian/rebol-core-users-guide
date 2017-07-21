# Forall - Function Summary

## Summary:

Evaluates a block for every value in a series.

## Usage:

**forall word body**

## Arguments:

**word** - Word set to each position in series and changed as a result (must be: word)

**body** - Block to evaluate each time (must be: block)

## Description:

The FORALL function moves through a series one value at a time.

The WORD argument is a variable that moves through the series. Prior to evaluation, the WORD argument must be set to the desired starting position within the series (normally the head, but any position is valid). After each evaluation of the block, the word will be advanced to the next position within the series.

```
cities: ["Eureka" "Ukiah" "Santa Rosa" "Mendocino"]
forall cities [print first cities]
Eureka
Ukiah
Santa Rosa
Mendocino
```

```
chars: "abcdef"
forall chars [print first chars]
a
b
c
d
e
f
```

Important: The WORD argument is modified as a result of running this function. The WORD is set to the tail of the series in most cases. You can reset it to the head of the series with a HEAD function.

For example:

```
chars: "abcdef"
forall chars [print first chars]
probe chars
a
b
c
d
e
f
""
```

Now, reset the chars word to the head of the string:

```
chars: head chars
probe chars
"abcdef"
```

The FORALL function can be thought of as a shortcut for:

```
[
	while [not tail? series] [
		(your code)
		series: next series
	]
]
```

## Related:

[**for**](http://www.rebol.com/docs/words/wfor.html) - Repeats a block over a range of values.
[**foreach**](http://www.rebol.com/docs/words/wforeach.html) - Evaluates a block for each value(s) in a series.
[**forskip**](http://www.rebol.com/docs/words/wforskip.html) - Evaluates a block for periodic values in a series.