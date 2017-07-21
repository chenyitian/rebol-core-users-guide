# Load - Function Summary

## Summary:

Loads a file, URL, or string. Binds words to global context.

## Usage:

**load source**

## Arguments:

**source** - The source argument. (must be: file url string any-block binary)

## Refinements:

**/header** - Includes REBOL header object if present.

**/next** - Load the next value only. Return block with value and new position.

**/library** - Force file to be a dynamic library. (Command version)

**/markup** - Convert HTML and XML to a block of tags and strings.

**/all** - Load all values. Does not evaluate REBOL header.

## Description:

Reads and converts external data, including programs, data structures, images, and sounds into memory storage objects that can be directly accessed and manipulated by programs.

The argument to LOAD can be a file, URL, string, or binary value. When a file name or URL is provided, the data is read from disk or network first, then it is loaded. In the case of a string or binary value, it is loaded directly from memory.

Here are a few examples of using LOAD:

```
script: load %comments.r
image: load %test-image.png
sound: load %whoosh.wav
```

```
;data: load http://www.rebol.com/example.r
;data: load ftp://ftp.rebol.com/example.r
```

```
data: load "1 2 luke fred@example.com"
code: load {loop 10 [print "hello"]}
```

LOAD is often called for a text file that contains REBOL code or data that needs to be brought into memory. The text is first searched for a REBOL header, and if a header is found, it os evaluated first. (However, unlike the DO function, LOAD does not require that there be a header.)

If the load results in a single value, it will be returned. If it results in a block, the block will be returned. No evaluation of the block will be done; however, words in the block will be bound to the global context.

If the header object is desired, use the /HEADER option to return it as the first element in the block.

The /ALL refinement is used to load an entire script as a block. The header is not evaluated.

The /NEXT refinement returns a block consisting of two elements. The first element is the first value loaded in the series. The second element is the original series with the current index just past the LOADed value.

```
data: load "11 22 33 44"
print third data
33
```

```
set [value data] load/next data
print value
11
```

```
print data
22
```

## Related:

[**do**](http://www.rebol.com/docs/words/wdo.html) - Evaluates a block, file, URL, function, word, or any other value.
[**read**](http://www.rebol.com/docs/words/wread.html) - Reads from a file, url, or port-spec (block or object).
[**save**](http://www.rebol.com/docs/words/wsave.html) - Saves a value or a block to a file or url.