# Exists? - Function Summary

## Summary:

Determines if a file or URL exists.

## Usage:

**exists? target**

## Arguments:

**target** - The target argument. (must be: file url)

## Description:

Returns FALSE if the file does not exist.

```
print exists? %file.txt
true
```

```
print exists? %doc.r
false
```

## Related:

[**delete**](http://www.rebol.com/docs/words/wdelete.html) - Deletes the specified file(s).
[**modified?**](http://www.rebol.com/docs/words/wmodifiedq.html) - Returns the last modified date of a file or URL.
[**read**](http://www.rebol.com/docs/words/wread.html) - Reads from a file, url, or port-spec (block or object).
[**size?**](http://www.rebol.com/docs/words/wsizeq.html) - Returns the size of a file or URL's contents.
[**write**](http://www.rebol.com/docs/words/wwrite.html) - Writes to a file, url, or port-spec (block or object).