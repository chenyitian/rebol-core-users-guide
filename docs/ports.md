# Chapter 14 - Ports

## Contents:

[1. Overview](#section-1)
[2. Opening a Port](#section-2)
  [2.1 The Open Function](#section-2.1)
  [2.2 Open Refinements](#section-2.2)
[3. Closing a Port](#section-3)
[4. Reading from a Port](#section-4)
[5. Writing to a Port](#section-5)
[6. Updating a Port](#section-6)
[7. Waiting for a Port](#section-7)
[8. Other Port Modes](#section-8)
  [8.1 Line Mode](#section-8.1)
  [8.2 Read and Write Only](#section-8.2)
  [8.3 Direct Port Access](#section-8.3)
  [8.4 Skipping Data](#section-8.4)
[9. File Permissions](#section-9)
[10. Directory Ports](#section-10)

## 1. Overview

Ports access **external** series such as files, networks, consoles, events, databases, data encoders, and data decoders. Port data is processed using the standard REBOL series functions as described in the [Series Chapter](rebolcore-6.html#_Toc487519750).

Ports are used for both input and output. The type of data a port handles depends on how the port is opened. Three types of data are possible:

| **String** | a series of bytes, converts line breaks (default) |
| ---------- | ---------------------------------------- |
| **Binary** | a series of bytes, no conversion of the data |
| **Block**  | a series of REBOL values                 |

A port can be opened in one of two buffering modes:

| **Buffered** | all of the data is held in memory (default) |
| ------------ | ---------------------------------------- |
| **Direct**   | data is not held in memory               |

In addition, a port can be opened with:

| **Wait**    | port will wait for data (default) |
| ----------- | --------------------------------- |
| **No-wait** | port will not wait for data       |

## 2. Opening a Port

### 2.1 The Open Function

The **open** function initializes access to a port according to specified parameters. The function can be supplied with a filename, a URL, or an object. In addition, there are several refinements that will affect the open operation or the access to the port's data.

The simplest method of using **open** is to provide it with a filename or URL as its argument. In the example below, a file port is opened:

```
fp: open %file.txt

```

The `fp` variable refers to the port. If the port did not open, an error will occur. If necessary, the error can be caught with the **try** function.

By default the file is opened as buffered. This means that the file is accessed and modified in memory and changes to the file are not written out until the port is closed or updated.

For files, the **open** function will automatically create the file if it does not already exist.

```
close open %somefile.txt
if exists? %somefile.txt [print "somefile exists"]
somefile exists

```

The **/new** refinement can be used to overwrite an existing file.

```
write %somefile.txt "text in some file"
print read %somefile.txt
text in some file
close insert open/new %somefile.txt "new data"
print read %somefile.txt
new data

```

Once a port is open, the series operations such as **copy**, **insert**, **remove**, **clear**, **first**, **next**, and **length?**can be used to access and change the contents the port.

### 2.2 Open Refinements

The open function accepts a number of refinements that can be used to modify its operation:

| **/binary**  | port data is binary                      |
| ------------ | ---------------------------------------- |
| **/string**  | port data is text, translate all line terminators |
| **/with**    | specify an alternate line termination    |
| **/lines**   | handle data a line at a time or as a block of lines |
| **/direct**  | do not buffer the port                   |
| **/new**     | create or recreate the target of the port |
| **/read**    | open for read only operation             |
| **/write**   | open for write only operation            |
| **/no-wait** | do not wait for data                     |
| **/skip**    | skip part of the data                    |
| **/allow**   | specify protection attributes of files   |
| **/custom**  | allow special refinements                |

## 3. Closing a Port

Access to a port is terminated with the **close** function. All buffered data that has not been saved will be written to the target file. The example below will close a port opened earlier:

```
close fp

```

If you attempt to close a port that is not open, an error will occur.

A port that is closed can be reopened again with the **open** function:

```
open fp

```

## 4. Reading from a Port

The series **copy** function is used to read data from an open port:

```
print copy fp
I wanted the gold, and I sought it,I scrabbled and mucked like
a slave....

```

This function will wait for the port data. If you don't want to wait for the data, open the port with the /no-wait refinement.

To read only a portion of the port data, use **copy/part:**

```
print copy/part fp 35
I wanted the gold, and I sought it,

```

Note that the second argument to copy can be a length or a position within the port.

You can use the series **find** and **copy** functions to read just part of the port's data:

```
a: find fp "famine"
print copy/part a find a newline
famine or scurvy -- I fought it;

```

The first, next, and other positional series functions can also be used on the port:

```
print first fp
I
print first next next fp
w

```

The **copy** function will return **none** when all data have been read from a port. When running in **/no-wait** mode, the **copy** function will return an empty string if no data is available for the port.

```
tp: open/direct/binary/no-wait tcp://system:8000
content: make binary! 1000
while [wait tp  data: copy tp] [append content data]
close tp

```

## 5. Writing to a Port

The **insert** function is used to write to a port.

```
insert fp "I was a fool to seek it."

```

If the port is buffered, the change will occur externally when the port is closed or updated (with the **update**function). If the port is opened with **/direct**, then the change will occur immediately.

All of the **insert** refinements can be used on the port. For example, to write 20 spaces into a port:

```
insert/dup fp " " 20

```

You can also use the **remove**, **clear**, **change**, **append**, **replace**, and other series modifying functions on the port.

For example, to remove a single character or a number of characters:

```
remove fp

remove/part fp 20

```

and to remove all remaining characters, write:

```
clear fp

```

## 6. Updating a Port

The **update** function forces a port to update its status with respect to the external device. For example, when writing a buffered file, the **update** function can be used to force the data buffer out to the file. When reading, the **update** function can be used to be certain that any pending data has been read into memory.

```
update fp

```

## 7. Waiting for a Port

The **wait** function is essential to programs that need to handle asynchronous data transfers. With **wait**, you can wait for data on one or more ports, or for a timeout to occur.

The **wait** function will accept a single port:

```
wait port

```

or, an entire block of ports can be provided:

```
wait [port1 port2 port3]

```

In addition, a timeout value can be provided as a number of seconds or as a time value:

```
wait [port1 port2 10]

wait [port1 port2 0:00:05]

```

The first example will time out in ten seconds. The second example will timeout in five seconds.

The **wait** function will return the port that is ready or `none` if the timeout occurred.

```
ready: wait [port1 port2 10]
if ready [data: copy ready]

```

The above example will read data from the first ready port if a timeout did not occur.

To obtain a block of all ports that are ready, use the /all refinement.

```
ready: wait/all [port1 port2 10]
if ready [
    foreach port ready [
        append data copy port
    ]
]

```

This example would append data from all ready ports into a single series.

You can also use the **dispatch** function to evaluate a block or function based on the results of a **wait** on multiple ports.

```
dispatch [
    port1 [print "port1 awake"]
    port2 [print "port2 awake"]
    10 [print "timeout!"]
]

```

**Use /No-wait and /Direct**

To use **wait** with most ports, you will need to specify the **/no-wait** and **/direct** refinements as part of the open. This indicates that the normal data access functions should not block and that data is not buffered.

```
port1: open/no-wait/direct tcp://system:8000

```

## 8. Other Port Modes

### 8.1 Line Mode

The **open** function allows ports to be opened for line access. In line mode, the first function will return a line of text, rather than a character. The example below reads a file one line at a time:

```
fp: open/lines %file.txt
print first fp
I wanted the gold, and I got it --
print third fp
Yet somehow life's not what I thought it,

```

The /lines refinement is also useful for Internet protocols that are line oriented.

```
tp: open/lines tcp://server:8000
print first tp

```

### 8.2 Read and Write Only

You can use the **/read** refinement to open a port as read only:

```
fp: open/read %file.txt

```

Changes made to the port's buffer, are not written back to the file.

To open for write only, use the **/write** refinement:

```
fp: open/write %file.txt

```

File ports opened with the **/write** refinement will not read the current data upon opening the port.

Closing, or updating a write only file port will cause existing data in the file to be overwritten:

```
insert fp "This is the law of the Yukon..."
close fp
print read %file.txt
This is the law of the Yukon...

```

### 8.3 Direct Port Access

The **/direct** refinement opens an unbuffered port. This is useful to access files a portion at a time, such as when a file is too large to be held in memory.

```
fp: open/direct %file.txt

```

Reading the data with a **copy** function will move the port's head forward:

```
print copy/part fp 40
I wanted the gold, and I sought it,^/ I
print copy/part fp 40
scrabbled and mucked like a slave.^/Was i

```

In direct mode, the port will always be at its head position:

```
print head? fp
true

```

The **copy** function will return `none` when the port has reached its end.

Here is an example that uses direct ports to copy a file of any size:

```
from-port: open/direct %a-file.jpg
to-port: open/direct %a-file.jpg
while [data: copy/part from-port 100000 ][
    append to-port data
]
close from-port
close to-port

```

### 8.4 Skipping Data

There are two ways to skip data that exists in a port. First, you can open the port with the **/skip** refinement. This **open** function will automatically skip to a point in the port. For example:

```
fp: open/direct/skip %file.big 1000000

fp: open/skip http://www.example.com/bigfile.dat 100000

```

You can also use the **skip** function on the port. For files that are opened with **/direct** and **/binary** the skip operation is identical to a file system seek operation. Data is not read into memory. This is not possible in **/string**mode because the line breaks interfere with the skip size.

```
fp: open/direct/binary %file.dat
fp: skip fp 100000

```

## 9. File Permissions

When files are created by REBOL, default access permissions are set. On Windows and Macintosh systems files are created with full access privileges. On UNIX systems files are created with the permissions set to the current umask setting.

When using **open** or **write** to access a file the **/allow** refinement is used to set file access permissions.

The **/allow** refinement takes a block as an argument. This block can consist of any or all of the three words **read**,**write** and **execute**.

**Operating System Restrictions**

The **/allow** refinement will only set permissions on operating systems supporting the specified permission setting. If the operating system does not support a permission setting used, the setting will be ignored. For instance, files on UNIX systems may be set as executable (**** execute ), but the Windows and Macintosh operating systems don't support this. When dealing with UNIX systems, permissions set using **/allow** will only set the user permissions. Using **/** allow will cause all access permissions to be removed for users and others.

To make a file read only, use **open/allow**, or **write/allow** with a read block.

```
write/allow %file.txt [read]

```

To make a file readable and executable:

```
open/allow %file.txt [read execute]

```

You can set similar permissions for write access:

```
write/allow %file.txt [read write]

```

To prevent any access to a file (for operating systems where this would make a difference) provide an empty permissions block:

```
write/allow %file.txt []

```

To permit full access:

```
write/allow %file [read write execute]

```

## 10. Directory Ports

Directory ports allow you to open direct access to file directories. Within the system, this is how most other directory functions are created.

When you open a directory, you gain direct access to the directory as a block of filenames:

```
mydir: open %intro/
forall mydir [print first mydir]
CVS/
history.t
intro.t
overview.t
quick.t
close mydir

```

You can advance to a specific position within a directory series and remove a file with code such as:

```
dir: open %.
remove next dir
close dir

```

This deletes the second file in the current directory. Similarly,

```
remove at dir 5

```

would delete the fifth file in the directory, and:

```
clear dir

```

would delete all of the files in the directory.

To delete all files that contain with the word "junk", you can write:

```
dir: open %intro/
while [not tail? dir] [
    either find first dir "junk" [remove dir][
        dir: next dir
    ]
]
close dir

```

The changes made to a directory are made when the directory is closed or when it is updated. To force the action to occur immediately use a line such as:

```
update dir

```

The method of directory access can also be used for changing the names of files. After the **open**, the line:

```
change at dir 3 %newname.txt

```

will rename the third file in the directory. Similarly, the names of any of the files in the directory can be changed.

Here is an example that renames all of the files in a directory by adding the word REBOL to their names:

```
dir: open %intro/
forall dir [insert first dir "REBOL"]
close dir
```