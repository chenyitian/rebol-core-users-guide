# Try - Function Summary

## Summary:

Tries to DO a block and returns its value or an error.

## Usage:

**try block**

## Arguments:

**block** - The block argument. (must be: block)

## Description:

TRY provides a useful means of capturing errors and handling them within a script. For instance, use TRY to test an expression that could fail and stop the script. TRY returns an error value if an error happened, otherwise it returns the normal result of the block.

```
if error? try [1 + "x"] [print "Did not work."]
Did not work.
```

```
if error? try [load "$10,20,30"] [print "No good"]
No good
```

## Related:

[**disarm**](http://www.rebol.com/docs/words/wdisarm.html) - Returns the error value as an object.
[**do**](http://www.rebol.com/docs/words/wdo.html) - Evaluates a block, file, URL, function, word, or any other value.
[**error?**](http://www.rebol.com/docs/words/werrorq.html) - Returns TRUE for error values.