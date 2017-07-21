# Info? - Function Summary

## Summary:

Returns information about a file or url.

## Usage:

**info? target**

## Arguments:

**target** - The target argument. (must be: file url)

## Description:

The information is returned within an object that has SIZE, DATE, and TYPE words. These can be accessed in the same manner as other objects.

```
info: info? %file.txt
print info/size
5221
```

```
print info/date
9-Mar-2004/0:59:50-8:00
```

## Related:

[**dir?**](http://www.rebol.com/docs/words/wdirq.html) - Returns TRUE if a file or URL is a directory.
[**exists?**](http://www.rebol.com/docs/words/wexistsq.html) - Determines if a file or URL exists.
[**modified?**](http://www.rebol.com/docs/words/wmodifiedq.html) - Returns the last modified date of a file or URL.
[**size?**](http://www.rebol.com/docs/words/wsizeq.html) - Returns the size of a file or URL's contents.