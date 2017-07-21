# Dir? - Function Summary

## Summary:

Returns TRUE if a file or URL is a directory.

## Usage:

**dir? target**

## Arguments:

**target** - The target argument. (must be: file url)

## Description:

Returns FALSE if it is not a directory.

```
print dir? %file.txt
false
```

```
print dir? %.
true
```

## Related:

[**exists?**](http://www.rebol.com/docs/words/wexistsq.html) - Determines if a file or URL exists.
[**make-dir**](http://www.rebol.com/docs/words/wmake-dir.html) - Creates the specified directory. No error if already exists.
[**modified?**](http://www.rebol.com/docs/words/wmodifiedq.html) - Returns the last modified date of a file or URL.