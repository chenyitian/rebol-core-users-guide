# Change-dir - Function Summary

## Summary:

Changes the active directory path.

## Usage:

**change-dir dir**

## Arguments:

**dir** - new directory path (must be: file)

## Description:

Changes the value of system/script/path. This value is used for file-related operations. Any file path that does not begin with a slash (/) will be relative to the path in system/script/path. When a script file is executed using the DO native, the path will automatically be set to the directory containing the path. When REBOL starts, it is set to the current directory where REBOL is started.

```
current: what-dir
make-dir %./rebol-temp/
probe current
%/C/rebol/link/ranch/projects/manuals/dictionary/
```

```
change-dir %./rebol-temp/
probe what-dir
%/C/rebol/link/ranch/projects/manuals/dictionary/rebol-temp/
```

```
change-dir current
delete %./rebol-temp/
probe what-dir
%/C/rebol/link/ranch/projects/manuals/dictionary/
```

## Related:

[**list-dir**](http://www.rebol.com/docs/words/wlist-dir.html) - Prints a multi-column sorted listing of a directory.
[**make-dir**](http://www.rebol.com/docs/words/wmake-dir.html) - Creates the specified directory. No error if already exists.
[**what-dir**](http://www.rebol.com/docs/words/wwhat-dir.html) - Prints the active directory path