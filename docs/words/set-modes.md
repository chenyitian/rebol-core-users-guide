# Set-modes - Function Summary

## Summary:

Changes mode settings for a port.

## Usage:

**set-modes target modes**

## Arguments:

**target** - The target argument. (must be: file url block port)

**modes** - The modes argument. (must be: block)

## Description:

This function sets a wide range of special modes for file and network ports. SET-MODES takes a port and a block of modes that contains words and values to specify the modes should be set.

```
port: open %test-file.txt
set-modes port [
	binary: true
	world-read: true
	world-write: true
	world-execute: true
]
```

The mode block accepted by set-modes is actually an object-style initialization block and allows multiple names to reference the same value.

```
set-modes port [binary: world-read: world-write: false]
```

Be sure to close the port when you are done:

```
close port
```

Note that a block returned by GET-MODES can be passed as an argument to SET-MODES.

SET-MODE returns the port that was passed as an argument.

See GET-MODES for a list of all port mode words.

## Related:

[**get-modes**](http://www.rebol.com/docs/words/wget-modes.html) - Returns mode settings for a port.
[**open**](http://www.rebol.com/docs/words/wopen.html) - Opens a new port connection.
[**read**](http://www.rebol.com/docs/words/wread.html) - Reads from a file, url, or port-spec (block or object).
[**write**](http://www.rebol.com/docs/words/wwrite.html) - Writes to a file, url, or port-spec (block or object).