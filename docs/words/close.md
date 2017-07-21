# Close - Function Summary

## Summary:

Closes an open port connection.

## Usage:

**close port**

## Arguments:

**port** - The port argument. (must be: port)

## Description:

Closes a port opened earlier with the OPEN function. Any changes to the port data that have been buffered will be written.

```
port: open %test-file.txt
insert port "Date: "
insert port form now
insert port newline
close port
```

```
print read %test-file.txt

9-Mar-2004/0:59:47-8:00Date: 
9-Mar-2004/0:57:58-8:00Date: 
9-Mar-2004/0:55:18-8:00Date: 
9-Mar-2004/0:54:58-8:00Date: 
9-Mar-2004/0:06:50-8:00Date: 
8-Mar-2004/23:53:31-8:00Date: 
8-Mar-2004/23:49:07-8:00Date: 
8-Mar-2004/23:46:40-8:00Date: 
8-Mar-2004/23:45:23-8:00Date: 
8-Mar-2004/23:40:04-8:00Date: 
8-Mar-2004/23:35:04-8:00Date: 
8-Mar-2004/23:33:09-8:00Date:
```

## Related:

[**do**](http://www.rebol.com/docs/words/wdo.html) - Evaluates a block, file, URL, function, word, or any other value.
[**load**](http://www.rebol.com/docs/words/wload.html) - Loads a file, URL, or string. Binds words to global context.
[**open**](http://www.rebol.com/docs/words/wopen.html) - Opens a new port connection.
[**send**](http://www.rebol.com/docs/words/wsend.html) - Send a message to an address (or block of addresses)