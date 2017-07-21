# Clean-path - Function Summary

## Summary:

Cleans-up '.' and '..' in path; returns the cleaned path.

## Usage:

**clean-path target**

## Arguments:

**target** - The target argument. (must be: file url)

## Description:

Rebuilds a directory path after decoding parent (..) and current (.) path indicators.

```
probe clean-path %com/www/../../../graphics/image.jpg
%/C/rebol/link/ranch/projects/manuals/graphics/image.jpg
```

```
messy-path: %/rebol/scripts/neat-stuff/../../experiments/./tests
neat-path: clean-path messy-path
probe neat-path
%/rebol/experiments/tests
```

URLs are returned unmodified (because the true paths may not be known).

## Related:

[**change-dir**](http://www.rebol.com/docs/words/wchange-dir.html) - Changes the active directory path.
[**dir?**](http://www.rebol.com/docs/words/wdirq.html) - Returns TRUE if a file or URL is a directory.
[**list-dir**](http://www.rebol.com/docs/words/wlist-dir.html) - Prints a multi-column sorted listing of a directory.
[**split-path**](http://www.rebol.com/docs/words/wsplit-path.html) - Splits a file or URL path. Returns a block containing path and target.