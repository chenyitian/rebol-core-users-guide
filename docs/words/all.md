# All - Function Summary

## Summary:

Shortcut AND. Evaluates and returns at the first FALSE or NONE.

## Usage:

**all block**

## Arguments:

**block** - Block of expressions (must be: block)

## Description:

Evaluates each expression in a block until one of the expressions returns NONE or FALSE, in which case a NONE is returned. Otherwise, the value of the last expression will be returned.

```
print all [1 none]
none
```

```
print all [none 1]
none
```

```
print all [1 2]
2
```

```
print all [10 > 1 "yes"]
yes
```

```
print all [1 > 10 "yes"]
none
```

```
time: 10:30
if all [time > 10:00 time < 11:00] [print "time is now"]
time is now
```

No other expressions are evaluated beyond the point where a value fails:

```
a: 0
all [none a: 2]
print a
0
```

```
a: 0
all [1 a: 2]
print a
2
```

```
day: 10
time: 9:45
ready: all [day > 5  time < 10:00  time: 12:00]
print time
12:00
```

## Related:

[**and**](http://www.rebol.com/docs/words/wand.html) - Returns the first value ANDed with the second.
[**any**](http://www.rebol.com/docs/words/wany.html) - Shortcut OR. Evaluates and returns the first value that is not FALSE or NONE.
[**or**](http://www.rebol.com/docs/words/wor.html) - Returns the first value ORed with the second.