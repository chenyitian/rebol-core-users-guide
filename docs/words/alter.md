# Alter - Function Summary

## Summary:

If a value is not found in a series, append it; otherwise, remove it.

## Usage:

**alter series value**

## Arguments:

**series** - The series argument. (must be: series port)

**value** - The value argument.

## Description:

The ALTER function is a type of data set operation. It either adds or removes a value depending on whether the value is already included. The word ALTER is short for the word "alternate".

For example, let's say you want to keep track of a few options used by your code. The options may be: FLOUR, SUGAR, SALT, and PEPPER. The following code will create a new block (to hold the data set) and add to it:

```
options: copy []
alter options 'SALT
probe options
[SALT]
```

```
alter options 'SUGAR
probe options
[SALT SUGAR]
```

You can use functions like FIND to test the presence of an option in the set:

```
if find options 'SALT [print "Salt was found"]
Salt was found
```

If you use ALTER a second time for the same option word, it will be removed:

```
alter options 'SALT
probe options
[SUGAR]
```

Normally ALTER values are symbolic words (such as those shown above) but any datatype can be used such as integers, strings, etc.

```
alter options 120
alter options "test"
probe options
[SUGAR 120 "test"]
```

## Related:

[**difference**](http://www.rebol.com/docs/words/wdifference.html) - Return the difference of two data sets.
[**exclude**](http://www.rebol.com/docs/words/wexclude.html) - Return the first set less the second set.
[**find**](http://www.rebol.com/docs/words/wfind.html) - Finds a value in a series and returns the series at the start of it.
[**intersect**](http://www.rebol.com/docs/words/wintersect.html) - Create a new value that is the intersection of the two arguments.
[**remove**](http://www.rebol.com/docs/words/wremove.html) - Removes value(s) from a series and returns after the remove.
[**unique**](http://www.rebol.com/docs/words/wunique.html) - Returns a set with duplicate values removed.