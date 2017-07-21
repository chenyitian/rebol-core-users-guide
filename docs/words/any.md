# Any - Function Summary

## Summary:

Shortcut OR. Evaluates and returns the first value that is not FALSE or NONE.

## Usage:

**any block**

## Arguments:

**block** - Block of expressions (must be: block)

## Description:

Evaluates each expression in a block until one of the expressions returns a value other than NONE or FALSE, in which case the value is returned. Otherwise, NONE will be returned.

```
print any [1 none]
1
```

```
print any [none 1]
1
```

```
print any [none none]
none
```

```
print any [false none]
none
```

```
print any [true none]
true
```

```
time: 10:30
if any [time > 10:00  time < 11:00] [print "time is now"]
time is now
```

No other expressions are evaluated beyond the point where a successful value is found:

```
a: 0
any [none a: 2]
print a
2
```

```
a: 0
any [1 a: 2]
print a
0
```

```
day: 10
time: 9:45
ready: any [day > 5  time < 10:00  time: 12:00]
print time
9:45
```

## Related:

[**all**](http://www.rebol.com/docs/words/wall.html) - Shortcut AND. Evaluates and returns at the first FALSE or NONE.
[**and**](http://www.rebol.com/docs/words/wand.html) - Returns the first value ANDed with the second.
[**or**](http://www.rebol.com/docs/words/wor.html) - Returns the first value ORed with the second.