# Delete - Function Summary

## Summary:

Deletes the specified file(s).

## Usage:

**delete target**

## Arguments:

**target** - the file to delete (must be: file url)

## Refinements:

**/any** - allow wild cards

## Description:

Deletes the file or URL object that is specified. If the file or URL refers to an empty directory, then the directory will be deleted.

```
write %delete-test.r "This file is no longer needed."
delete %delete-test.r
```

## Related:

[**exists?**](http://www.rebol.com/docs/words/wexistsq.html) - Determines if a file or URL exists.