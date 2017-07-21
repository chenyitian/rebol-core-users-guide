# Files

## Contents:

- [1. Overview](#section-1)
- [2. Names and Paths](#section-2)
  - [2.1 File Names](#section-2.1)
  - [2.2 Path Strings](#section-2.2)
  - [2.3 Case Sensitivity](#section-2.3)
  - [2.4 File Name Functions](#section-2.4)
- [3. Reading Files](#section-3)
  - [3.1 Reading Text Files](#section-3.1)
  - [3.2 Reading Binary Files](#section-3.2)
  - [3.3 Reading Over the Network](#section-3.3)
- [4. Writing Files](#section-4)
  - [4.1 Writing Text Files](#section-4.1)
  - [4.2 Writing Binary Files](#section-4.2)
  - [4.3 Writing Files to a Network](#section-4.3)
- [5. Line Conversion](#section-5)
- [6. Blocks of Lines](#section-6)
- [7. File and Directory Information](#section-7)
  - [7.1 Directory Check](#section-7.1)
  - [7.2 File Existence](#section-7.2)
  - [7.3 File Size](#section-7.3)
  - [7.4 File Modification Date](#section-7.4)
  - [7.5 Directory Information](#section-7.5)
- [8. Directories](#section-8)
  - [8.1 Reading a Directory](#section-8.1)
  - [8.2 Making a Directory](#section-8.2)
  - [8.3 Renaming Directories and Files](#section-8.3)
  - [8.4 Deleting Directories and Files](#section-8.4)
  - [8.5 Current Directory](#section-8.5)
  - [8.6 Changing the Current Directory](#section-8.6)
  - [8.7 Listing the Current Directory](#section-8.7)

## 1. Overview

An important aspect of REBOL's power is its ability to manipulate files and directories. REBOL provides a wide range of functions designed to allow operations ranging from simple file reads to direct access to files and directories. For more information on direct access to files and directories, see the [Ports Chapter](rebolcore-14.html#_Toc487519750).

## 2. Names and Paths

REBOL provides a standard, machine independent file and path naming convention.

### 2.1 File Names

In scripts, file names and paths are written with a percent sign (%) followed by a sequence of characters:

```
%examples.r
%big-image.jpg
%graphics/amiga.jpg
%/c/plug-in/video.r
%//sound/goldfinger.mp3

```

The percent sign is necessary to prevent file names from being interpreted as words within the language.

Although it is not a good practice, spaces can be included in file names by enclosing the file name in double quotes (" "). The double quotes prevent the file name from being interpreted as multiple words:

```
%"this file.txt"
%"cool movie clip.mpg"

```

The standard Internet convention of using a percent sign (%) and a hex code is also allowed for character encoding. When this is done, quotes are not required. The above file names could also be written as:

```
%this%20file.txt
%cool%20movie%20clip.mpg

```

Note that the standard file suffix for REBOL scripts is ".r". On systems where this convention collides with another file type, a ".reb" suffix can be used instead.

### 2.2 Path Strings

File paths are written with a percent sign (%) followed by a sequence of directory names that are each separated by a forward slash (/).

```
%dir/file.txt
%/file.txt
%dir/
%/dir/
%/dir/subdir/
%../dir/file.txt

```

The standard character for separating directories is the forward slash (/), not the backslash (\). If backslashes are found they are converted to forward slashes:

```
probe %\some\cool\movie.mpg
%/some/cool/movie.mpg

```

REBOL provides a standard, operating system independent method for specifying directory paths. Paths can be relative to the current directory or absolute from the top-level file structure of the operating system.

File paths that do not begin with a forward slash (/) are relative paths.

```
%docs/intro.txt
%docs/new/notes.txt
%"new mail/inbox.mbx"

```

The standard convention of using double dots (..) to indicate a parent directory or a single dot (.) to refer to the current directory is also supported. For example:

```
%.
%./
%./file.txt
%..
%../
%../script.r
%../../plans/schedule.r

```

File paths use the standard Internet convention of beginning absolute paths with a forward slash (/). The forward slash indicates to start at the top level of the file system. (Generally, absolute paths should be avoided to ensure machine-independent scripts.) The example:

```
%/home/file.txt

```

would refer to a disk volume or partition named `home`. Other examples are:

```
%/ram/temp/test.r
%/cd0/scripts/test/files.r

```

To refer to the `C` volume that is often used by Windows, the notation is:

```
%/C/docs/file.txt
%"/c/program files/qualcomm/eudora mail/out.mbx"

```

Notice in the above lines that the disk volume, `C`, is not written as:

```
%c:/docs/file.txt

```

The above example is not a machine independent format and causes an error.

If the first directory name is absent, and the path begins with double forward slashes (//), then the file path is relative to the current volume:

```
%//docs/notes

```

### 2.3 Case Sensitivity

In REBOL, file names are **not** case-sensitive by default. However, when new files are created by the language, they keep the case they were typed in:

```
write %Script-File.r file-data

```

The above example creates the file name with the `S` and `F` in uppercase.

In addition, when file names are read from directories, the case is preserved:

```
print read %/home

```

For case-sensitive systems, such as UNIX, REBOL finds the closest case match to the specified file. For example, if a script asks to read `%test`.r, but only finds `%TEST`.r, the `%TEST`.r file is read. This behavior is necessary to allow machine-independent scripts.

### 2.4 File Name Functions

Various functions are provided to help you create file names and paths. These are listed below in [File Name Functions](rebolcore-12.html#10794).

| **to-file**    | Converts strings and blocks into a file name or file path. |
| -------------- | ---------------------------------------- |
| **split-path** | Splits a path into its directory part and its file name. |
| **clean-path** | Returns the absolute path that is equivalent to any given path containing double dot (..) or dot (.). |
| **what-dir**   | Returns the absolute path to the current directory. |

## 3. Reading Files

Files are read as a series of text characters or as binary bytes. The source of the file is either a local file on your system or a file from the network.

### 3.1 Reading Text Files

To read a local text file, use the **read** function:

```
text: read %file.txt

```

The **read** function returns a string that holds the entire text of the file. In the above example, the variable `text`refers to that string.

Within the string returned by **read**, line terminators are converted to `newline` characters, regardless of what style of line termination is used on your operating system. This allows you to write scripts that search for `newline`without concern for what particular character or characters constitute a line termination.

```
next-line: next find text newline

```

A file can also be read as separate lines that are stored in a block:

```
lines: read/lines %file.txt

```

See the [Line Conversion section](rebolcore-12.html#_Toc487519846) for more information about `newline` and reading lines.

To read a file a piece at a time, use the **open** function as described in the [Ports Chapter](rebolcore-14.html#_Toc487519750).

To view the contents of a text file, you can read it using **read** and print it using **print:**

```
print read %service.txt
I wanted the gold, and I sought it,I scrabbled and mucked like
a slave.

```

### 3.2 Reading Binary Files

To read a binary file such as an image, a program, or a sound, use **read/binary:**

```
data: read/binary %file.bin

```

The **read/binary** function returns a binary series that holds the entire contents of the file. In the above example, the variable `data` refers to the binary series. No conversion of any type is done to the file.

To read a binary file a piece at a time, use the **open** function as described in the [Ports Chapter](rebolcore-14.html#_Toc487519750).

### 3.3 Reading Over the Network

Files can be read from a network. For example, to view a text file from a network using the HTTP protocol:

```
print read http://www.rebol.com/test.txt
Hellotherenewuser!

```

The file could be written locally with the line:

```
write %test.txt read http:/www.rebol.com/test.txt

```

In the write process the file will have its line termination converted to that which is used by your operating system.

To read and save a binary file, such as an image, use the following line:

```
write %image.jpg
read/binary http:/www.rebol.com/image.jpg

```

Refer to the chapter on [Network Protocols](rebolcore-13.html#_Toc487519750) for more information and examples of accessing files across networks.

## 4. Writing Files

You can write a file as a series of text characters or as binary bytes. The location of the file can be either a local file on your system or a file on a network.

### 4.1 Writing Text Files

To write a local text file, use the following line of code:

```
write %file.txt "sample text here"

```

This writes the entire text to the file.

If a file contains `newline` characters, they will be converted to those used by your local file system. This allows you to deal with files in a consistent **manner**, but write them out using the convention that is standard to your file system.

For instance, the following line converts any text file from one line termination format (UNIX, Macintosh, PC, Amiga) to that which is used by your local system:

```
write %newfile.txt read %file.txt

```

The above line reads the entire file while converting its line termination to the REBOL standard, then writes the file converting it to the local operating system format.

To append to the end of a file, use the **/append** refinement:

```
write/append %file.txt "more text"

```

A file can also be written from separate lines that are stored in a block.

```
write/lines %file.txt lines

```

To write a file a piece at a time, use the **open** function as described in the [Ports Chapter](rebolcore-14.html#_Toc487519750).

### 4.2 Writing Binary Files

To write a binary file such as an image, a program, a sound, use **write/binary:**

```
write/binary %file.bin data

```

The **write/binary** function creates the file if it does not exist or overwrites the file if it already exists. No conversion of any type is done to the file.

To write a binary file a piece at a time, use the **open** function as described in the [Ports Chapter](rebolcore-14.html#_Toc487519750).

### 4.3 Writing Files to a Network

Files can also be written to a network. For example, to write a text file to a network using FTP, use:

```
write ftp://ftp.domain.com/file.txt "save this text"

```

The file can be read locally and written to the net with a line such as:

```
write ftp://ftp.domain.com/file.txt read %file.txt

```

In the process, the file has its line termination converted to the standard CRLF format.

To write a binary file, such as an image, to the network, use the following lines of code:

```
write/binary ftp://ftp.domain.com/file.txt/image.jpg
    read/binary %image.jpg

```

Refer to the chapter on [Network Protocols](rebolcore-13.html#_Toc487519750) for more information and examples of accessing files from networks.

## 5. Line Conversion

When a file is read as text, all line terminators are converted to `newline` (line feed) characters. Line feeds (used as line terminators on Amiga, Linux, and UNIX systems), carriage returns (used as line terminators on Macintosh), and the CR/LF combination (PC and Internet) are all converted to the equivalent `newline` characters.

Using a standard line terminator within scripts allows them to operate in a machine-independent fashion. For example, to search for and count all `newline` characters within a text file:

```
text: read %file.txt
count: 0
while [spot: find text newline][
    count: count + 1
    text: next spot
]

```

The line conversion is also useful for reading network files:

```
text: read ftp://ftp.rebol.com/test.txt

```

When a file is written, the `newline` character is converted to the line termination style standard for the operating system being used. For instance, the `newline` character is converted to a CRLF on the PC, LF on UNIX or Amiga, or CR for a Macintosh. Network files are written with CRLF.

The following function converts any text file with any terminator style to that used by the local operating system:

```
convert-lines: func [file] [write file read file]

```

The file is read and all line terminators are converted, then the file is written and `newline` characters are converted to the local operating system style.

Line conversion can be disabled by reading the file as binary. For instance, the following line:

```
write/binary %newfile.txt read/binary %oldfile.txt

```

preserves the line terminators of the text file.

## 6. Blocks of Lines

Text files can be easily accessed and managed as individual lines of text, rather than as a single series of characters. For example, to read a file as a block of lines:

```
lines: read/lines %service.txt

```

The above example returns a block containing a series of strings (one for each line) without line terminators. Empty lines are represented by empty strings.

To print a specific line you use the following code:

```
print first lines
print last lines
print pick lines 100
print lines/500

```

To print all of the lines of a file, use the following line of code:

```
foreach line lines [print line]
I wanted the gold, and I sought it,
I scrabbled and mucked like a slave.
Was it famine or scurvy -- I fought it;
I hurled my youth into a grave.
I wanted the gold, and I got it --
Came out with a fortune last fall, --
Yet somehow life's not what I thought it,
And somehow the gold isn't all.

```

To print all of the lines that contain the string `gold`, use the following line of code:

```
foreach line lines [
   if find line "gold" [print line]
]
I wanted the gold, and I sought it,
I wanted the gold, and I got it --
And somehow the gold isn't all.

```

You can write the text file out as lines using the **write** function:

```
write/lines %output.txt lines

```

To write out specific lines from a block, use:

```
write/lines %output.txt [
    "line one"
    "line two"
    "line three"
]

```

In fact, the functions **read/lines** and **write/lines** can be combined to process files one line at a time. For example the following code removes all of the comments from a REBOL script:

```
script: read/lines %script.r
foreach line script [
    where: find line ";"
    if where [clear where]
]
write/lines %script1.r script

```

*The sample script in the above example is for demonstration purposes only. In addition to removing comments, the sample script would also remove valid semicolons in quoted strings.*

Files can be read as lines from a network as well:

```
data: read/lines http://www.rebol.com

print pick (read/lines ftp://ftp.rebol.com/test.txt) 3
new

```

The **/lines** refinement can be used with the **open** function to read a line at a time from console input. See the chapter on [Ports](rebolcore-14.html#_Toc487519750) for more information.

In addition **/lines** can be used with **/append** to append lines from a block to a file.

## 7. File and Directory Information

There are a number of functions that provide useful information about a file, such as whether it exists, its file size in bytes, when it was last modified, and whether it is a directory.

### 7.1 Directory Check

To determine if a file name is that of a directory, use the **dir?** function:

```
print dir? %file.txt
false
print dir? %.
true

```

The **dir?** function works with some network protocols as well:

```
print dir? ftp://www.rebol.com/pub/
true

```

### 7.2 File Existence

To determine if a file exists, use the **exists?** function:

```
print exists? %file.txt

```

To determine if a file exists before you read it, use:

```
if exists? file [text: read file]

```

To avoid overwriting a file you can check it with, use:

```
if not exists? file [write file data]

```

The **exists?** function also works with some network protocols:

```
print exists? ftp://www.rebol.com/file.txt

```

### 7.3 File Size

To obtain the byte size of a file, use the **size?** function:

```
print size? %file.txt

```

The **size?** function also works with some network protocols:

```
print size? ftp://www.rebol.com/file.txt

```

### 7.4 File Modification Date

To obtain the last modification date of a file, use the **modified?** function:

```
print modified? %file.txt
30-Jun-2000/14:41:55-7:00

```

Not all operating systems keep track of the creation date of a file, so to keep REBOL scripts operating system independent only the last modification date is accessible.

The **modified?** function also works with some network protocols:

```
print modified? ftp://www.rebol.com/file.txt

```

### 7.5 Directory Information

The **info?** function obtains all file directory information at the same time. The information is returned as an object:

```
probe info? %file.txt
make object! [
    size: 306
    date: 30-Jun-2000/14:41:55-7:00
    type: 'file
]

```

To print information about all files in the current directory, use:

```
foreach file read %. [
    info: info? file
    print [file info/size info/date info/type]
]
build-guide.r 22334 30-Jun-2000/14:24:43-7:00 file
code/ 11 11-Oct-1999/18:37:04-7:00 directory
data.r 41 30-Jun-2000/14:41:36-7:00 file
file.txt 306 30-Jun-2000/14:41:55-7:00 file

```

The **info?** function also works with some network protocols:

```
probe info? ftp://www.rebol.com/file.txt

```

## 8. Directories

There are several easy-to-use functions for reading directories, managing subdirectories, making new directories, renaming files, and deleting files. In addition, there are standard functions for getting, changing, and listing the current directory. For more information on direct access to directories, see the [Ports Chapter](rebolcore-14.html#_Toc487519750).

### 8.1 Reading a Directory

Directories are read in the same manner as files. The **read** function returns a block of file names rather than text or binary data.

To read all the file names from the current directory, use the following line of code:

```
read %.

```

The above example reads the entire directory and returns a block of file names.

To print the names of all files in a directory, use the following line of code:

```
print read %intro/
CVS/ history.t intro.t overview.t quick.t

```

Within the returned block, names of directories are indicated with a trailing forward slash. To print each file name on a separate line, use:

```
foreach file read %intro/ [print file]
CVS/
history.t
intro.t
overview.t
quick.t

```

Here is an easy way to print just the directories that were found:

```
foreach file read %intro/ [
    if #"/" = last file [print file]
]
CVS/

```

If you want to read a directory from the network, be sure to include a forward slash at the end of the URL to indicate to the protocol that you are referring to a directory:

```
print read ftp://ftp.rebol.com/

```

### 8.2 Making a Directory

The **make-dir** function makes a new directory. The new name for the directory can be relative to either the current directory or an absolute path.

```
make-dir %new-dir
make-dir %local-dir/
make-dir %/work/docs/old-docs/

```

The trailing slash is optional for this function.

Internally, the **make-dir** function calls **open** with the **/new** refinement. The line:

```
close open/new %local-dir/

```

also creates a new directory. The trailing slash is important in this example, indicating that a directory is to be created rather than a file.

If you use the **make-dir** function to create a directory that already exists, an error will occur. The error can be caught with the **try** function. The directory can be checked in advance with the **exists?** function.

### 8.3 Renaming Directories and Files

To rename a file, use the **rename** function:

```
rename %old-file %new-file

```

The old file name may include a complete path to the file, but the new file name must not include a path. This is because the **rename** function is not intended to move files between directories (various operating systems do not provide this function).

```
rename %../docs/intro.txt %conclusion.txt

```

If the old file name is a directory (indicated by a trailing slash), the **rename** function renames the directory:

```
rename %../docs/ %manual/

```

If the file cannot be renamed, an error will occur. The error can be caught with the **try** function.

### 8.4 Deleting Directories and Files

Files can be deleted using the **delete** function:

```
delete %file

```

The file to delete can include a path:

```
delete %source/docs/file.txt

```

A block of files within the same directory can also be deleted:

```
delete [%file1 %file2 %file3]

```

A group of files can be deleted using a wildcard character and the **/any** refinement:

```
delete/any %file*
delete/any %secret.?

```

The asterisk (*) wildcard character matches all characters, and the question mark (?) wildcard character matches a single character.

To delete a directory, provide a trailing forward slash:

```
delete %dir/
delete %../docs/old/

```

If the file cannot be deleted, an error will occur. The error can be caught with the **try** function.

### 8.5 Current Directory

Use the **what-dir** function to determine the current directory:

```
print what-dir
/work/REBOL/

```

The **what-dir** function refers to the current script's directory path, as found in `system/script/path`.

### 8.6 Changing the Current Directory

To change the current directory, use:

```
change-dir %new-path/to-dir/

```

If the trailing slash is not included, the function adds it.

### 8.7 Listing the Current Directory

To list the contents of the current directory, use:

```
list-dir

```

The number of columns used to show the directory is dependent on the console window size and the maximum file name length.