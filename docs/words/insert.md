# Insert - Function Summary

## Summary:

Inserts a value into a series and returns the series after the insert.

## Usage:

**insert series value**

## Arguments:

**series** - Series at point to insert (must be: series port bitset)

**value** - The value to insert (must be: any-type)

## Refinements:

**/part** - Limits to a given length or position.

**range** - The range argument. (must be: number series port pair)

**/only** - Inserts a series as a series.

**/dup** - Duplicates the insert a specified number of times.

**count** - The count argument. (must be: number pair)

## Description:

If the value is a series compatible with the first (block or string-based datatype), then all of its values will be inserted. The series position just past the insert is returned, allowing multiple inserts to be cascaded together.

This function includes many refinements.

/PART allows you to specify how many elements you want to insert.

/ONLY will force a block to be insert, rather than its individual elements. (Is only done if first argument is a block datatype.)

/DUP will cause the inserted series to be repeated a given number of times.

The series will be modified.

```
str: copy "here this"
insert str "now "
print str
now here this
```

```
insert tail str " message"
print str
now here this message
```

```
insert tail str reduce [tab now]
print str
now here this message	9-Mar-2004/0:59:54-8:00
```

```
insert insert str "Tom, " "Tina, "
print str
Tom, Tina, now here this message	9-Mar-2004/0:59:54-8:00
```

```
insert/dup str "." 7
print str
.......Tom, Tina, now here this message	9-Mar-2004/0:59:54-8:00
```

```
insert/part tail str next "!?$" 1
print str
.......Tom, Tina, now here this message	9-Mar-2004/0:59:54-8:00?
```

```
blk: copy ["hello"]
insert blk 'print
probe blk
[print "hello"]
```

```
insert tail blk http://www.rebol.com
probe blk
[print "hello" http://www.rebol.com]
```

```
insert/only blk [separate block]
probe blk
[[separate block] print "hello" http://www.rebol.com]
```

## Related:

[**append**](http://www.rebol.com/docs/words/wappend.html) - Appends a value to the tail of a series and returns the series head.
[**change**](http://www.rebol.com/docs/words/wchange.html) - Changes a value in a series and returns the series after the change.
[**clear**](http://www.rebol.com/docs/words/wclear.html) - Removes all values from the current index to the tail. Returns at tail.
[**join**](http://www.rebol.com/docs/words/wjoin.html) - Concatenates values.
[**remove**](http://www.rebol.com/docs/words/wremove.html) - Removes value(s) from a series and returns after the remove.