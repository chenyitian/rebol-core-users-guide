# List-dir - Function Summary

## Summary:

Prints a multi-column sorted listing of a directory.

## Usage:

**list-dir dir**

## Arguments:

**dir** - Directory to list or nothing (must be: any-type)

## Description:

Lists the files and directories of the specified path in a sorted multi-column output. If no path is specified, the directory specified in system/script/path is listed. Directory names are followed by a slash (/) in the output listing.

```
list-dir
autos.txt          comments.r         data               data.r    

date.r             datecode.r         datetime.txt       dict-html.
r        
dictionary.html    dictionary.r       file.comp          file.decom
p        
file.txt           fred/              helloworld.txt     junkme.txt

newfile.txt        public/            rebol-test-file.r  rebuild.ba
t        
test-file          test-file.txt      test-image.png     test-page.
html     
testfile           trash.me           undoced.r          upload.r  

whoosh.wav         words.r            words/
```

To obtain a block of files for use by your program, use the LOAD function. The example below returns a block that contains the names of all files and directories in the local directory.

```
files: load %./
print length? files
probe files
31
[%dictionary.html %dictionary.r %comments.r %whoosh.wav %undoced.r %rebuild.bat %words/ %fred/ %file.txt %test-file.txt %file.comp %file.decomp %helloworld.txt %public/ %test-file %autos.txt %newfile.txt %rebol-test-file.r %date.r %data.r %test-image.png %test-page.html %trash.me %junkme.txt %datetime.txt %data %upload.r %datecode.r %words.r %testfile %dict-html.r]
```

## Related:

[**change-dir**](http://www.rebol.com/docs/words/wchange-dir.html) - Changes the active directory path.
[**make-dir**](http://www.rebol.com/docs/words/wmake-dir.html) - Creates the specified directory. No error if already exists.
[**read**](http://www.rebol.com/docs/words/wread.html) - Reads from a file, url, or port-spec (block or object).
[**what-dir**](http://www.rebol.com/docs/words/wwhat-dir.html) - Prints the active directory path