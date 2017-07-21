# Foreach - Function Summary

## Summary:

Evaluates a block for each value(s) in a series.

## Usage:

**foreach word data body**

## Arguments:

**word** - Word or block of words to set each time (will be local) (must be: get-word word block)

**data** - The series to traverse (must be: series)

**body** - Block to evaluate each time (must be: block)

## Description:

For every value in a series, such as a block or string, this function will evaluate a block using a variable that holds that value.

For example, the series below is a block of city names. For each name in that block, the PRINT function will be evaluated. The CITY variable holds the name of the city each time.

```
cities: ["Eureka" "Ukiah" "Santa Rosa" "Mendocino"]
foreach city cities [print city]
Eureka
Ukiah
Santa Rosa
Mendocino
```

This also works for strings. Each character of the string will be printed below:

```
chars: "abcdef"
foreach char chars [print char]
a
b
c
d
e
f
```

The second argument can also be a block of words to get multiple values at the same time from the block:

```
months: ["March" 31 "April" 30 "May" 31 "June" 30]
foreach [name days] months [print [name "has" days "days"]]
March has 31 days
April has 30 days
May has 31 days
June has 30 days
```

## Related:

[**for**](http://www.rebol.com/docs/words/wfor.html) - Repeats a block over a range of values.
[**forall**](http://www.rebol.com/docs/words/wforall.html) - Evaluates a block for every value in a series.
[**forskip**](http://www.rebol.com/docs/words/wforskip.html) - Evaluates a block for periodic values in a series.