# As-pair - Function Summary

## Summary:

Combine X and Y values into a pair.

## Usage:

**as-pair x y**

## Arguments:

**x** - The x argument. (must be: number)

**y** - The y argument. (must be: number)

## Description:

Provides a shortcut for creating PAIR values from separate X and Y integers.

```
    print as-pair 100 50
    100x50
```

If you are performing a lot of xy pair math, you can also take a performance advantage of standard math operations on pairs:

```
print 100x34 * 0x1
0x34
```

```
print 100X100 + 0x200
100x300
```

```
print 100x200 - 50
50x150
```

```
print 100x34 * 2
200x68
```

```
offset: 100x100 ; upper left corner
size: 300x500   ; object xy size
print offset + size ; the lower right corner
400x600
```

## Related:

[**to-pair**](http://www.rebol.com/docs/words/wto-pair.html)