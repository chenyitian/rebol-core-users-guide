# To-local-file - Function Summary

## Summary:

Converts a REBOL file path to the local system file path.

## Usage:

**to-local-file path**

## Arguments:

**path** - The path argument. (must be: file string)

## Description:

This function provides a way to convert standard, system independent REBOL file formats into the file format used by the local operating system.

```
probe to-local-file %/c/temp
%c:\temp
```

```
probe to-local-file what-dir
%C:\rebol\link\ranch\projects\manuals\dictionary
```

Note that the format of the file path depends on your local system. Be careful how you use this function across systems.

## Related:

[**to-rebol-file**](http://www.rebol.com/docs/words/wto-rebol-file.html) - Converts a local system file path to a REBOL file path.