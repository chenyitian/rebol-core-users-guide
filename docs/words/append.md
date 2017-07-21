# Append - Function Summary

## Summary:

Appends a value to the tail of a series and returns the series head.

## Usage:

**append series value**

## Arguments:

**series** - The series argument. (must be: series port)

**value** - The value argument.

## Refinements:

**/only** - Appends a block value as a block

## Description:

Works on any type of series, including strings and blocks. Returns the series at its head.

/ONLY forces a block to be inserted as a block element (works only if the first argument is a block).

```
string: copy "hello"
probe append string " there"
"hello there"
```

```
file: copy %file
probe append file ".txt"
%file.txt
```

```
url: copy http://
probe append url "www.rebol.com"
http://www.rebol.com
```

```
block: copy [1 2 3 4]
probe append block [5 6]
[1 2 3 4 5 6]
```

```
probe append/only block [a block]
[1 2 3 4 5 6 [a block]]
```

## Related:

[**change**](http://www.rebol.com/docs/words/wchange.html) - Changes a value in a series and returns the series after the change.
[**insert**](http://www.rebol.com/docs/words/winsert.html) - Inserts a value into a series and returns the series after the insert.
[**remove**](http://www.rebol.com/docs/words/wremove.html) - Removes value(s) from a series and returns after the remove.