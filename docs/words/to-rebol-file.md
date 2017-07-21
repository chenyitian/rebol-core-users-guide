# To-rebol-file - Function Summary

## Summary:

Converts a local system file path to a REBOL file path.

## Usage:

**to-rebol-file path**

## Arguments:

**path** - The path argument. (must be: file string)

## Description:

This function provides a standard way to convert local operating system files into REBOL's standard machine independent format.

```
probe to-rebol-file "c:\temp"
%/c/temp
```

```
probe to-rebol-file "e:\program files\rebol"
%/e/program%20files/rebol
```

Note that the format of the file path depends on your local system. Be careful how you use this function across systems.

## Related:

[**to-local-file**](http://www.rebol.com/docs/words/wto-local-file.html) - Converts a REBOL file path to the local system file path.