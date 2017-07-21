# Scripts

## Contents:

- [1. Overview](#section-1)
- [1.1 File Suffix](#section-1.1)
- [1.2 Structure](#section-1.2)
- [2. Headers](#section-2)
- [3. Script Arguments](#section-3)
  - [3.1 Program Options](#section-3.1)
- [4. Running Scripts](#section-4)
  - [4.1 Loading Scripts](#section-4.1)
  - [4.2 Saving Scripts](#section-4.2)
  - [4.3 Commenting Scripts](#section-4.3)
- [5. Style Guide](#section-5)
  - [5.1 Formatting](#section-5.1)
  - [5.2 Word Names](#section-5.2)
  - [5.3 Script Headers](#section-5.3)
  - [5.4 Function Headers](#section-5.4)
  - [5.5 Script File Names](#section-5.5)
  - [5.6 Embedded Examples](#section-5.6)
  - [5.7 Embedded Debugging](#section-5.7)
  - [5.8 Minimize Globals](#section-5.8)
- [6. Script Cleanup](#section-6)

## 1. Overview

The term **script** refers not only to single files that are evaluated but also to **source** text embedded within other types of files (such as, web pages), or **fragments** of source text that are saved as data files or passed as messages.

### 1.1 File Suffix

REBOL scripts typically append a .r suffix to file names; however, this convention is not required. The interpreter reads files with any suffix and scans the contents for a valid REBOL script header.

### 1.2 Structure

The structure of a script is free-form. Indentation and spacing can be used to clarify the structure and content of the script. In addition, you are encouraged to use the standard scripting style to make scripts more universally readable. See the [Style Guide](#_Toc487519762) for more information.

## 2. Headers

Directly preceding the script body, every script must have a header that identifies its purpose and other script attributes. A header can contain the script name, author, date, version, file name, and additional information. REBOL data files that are not intended for direct evaluation do not require a header.

Headers are useful for several reasons.

- They identify a script as being valid source text for the REBOL interpreter.
- The interpreter uses the header to print out the script's title and determine what resources and versions it needs before evaluating the script.
- Headers provide a standard way to communicate the title, purpose, author, and other details of scripts. You can often determine from a script's header if a script interests you.
- Script archives and web sites use headers for generating script directories, categories, and cross references.
- Some text editors access and update a script's header to keep track of information such as the author, date, version, and history.

The general form of a script header is:

```
REBOL [block]

```

For the interpreter to recognize the header, the block must immediately follow the word **REBOL**. Only white space (spaces, tabs, and lines) is permitted between the word **REBOL** and the block.

The block that follows the **REBOL** word is an object definition that describes the script. The preferred minimal header is:

```
REBOL [
    Title:  "Scan Web Sites"
    Date:   2-Feb-2000
    File:   %webscan.r
    Author: "Jane Doer"
    Version: 1.2.3
]

```

When a script is loaded, the header block is evaluated and its words are set to their defined values. These values are used by the interpreter and can also be used by the script itself.

Note that words defined as a single value can also be defined as multiple values by providing them in a block:

```
REBOL [
    Title: "Scan Web Sites"
    Date:   12-Nov-1997
    Author: ["Ema User" "Wasa Writer"]
]

```

Headers can be more complex, providing information about the author, copyright, formatting, version requirements, revision history, and more. Because the block is used to construct the header object, it can also be extended with new information. This means that a script can extend the header as needed, but it should be done with care to avoid ambiguous or redundant information.

A full header might look something like this:

```
REBOL [
    Title:   "Full REBOL Header Example"
    Date:    8-Sep-1999
    Name:    'Full-Header  ; For window title bar

    Version: 1.1.1
    File:    %headfull.r
    Home:    http://www.rebol.com/rebex/

    Author:  "Carl Sassenrath"
    Owner:   "REBOL Headquarters"
    Rights:  "Copyright (C) Carl Sassenrath 1999"

    Needs:   [2.0 ODBC]
    Tabs:    4

    Purpose: {
        The purpose or general reason for the program
        should go here.
    }

    Note: {
        An important comment or notes about the program
        can go here.
    }

    History: [
        0.1.0 [5-Sep-1999 "Created this example" "Carl"]
        0.1.1 [8-Sep-1999 {Moved the header up, changed
            comment on extending the header, added
            advanced user comment.} "Carl"]
    ]

    Language: 'English
]

```

#### 2 Prefaced Scripts

Script text does not need to begin with a header. Scripts can begin with any text, allowing them to be inserted into email messages, web pages, and other files.

The header marks the beginning of the script, and the text that follows is the body of the script. Text that appears before the header is called the **preface** and is ignored during evaluation.

```
The text that appears before the header is ignored
by REBOL and can be used for comments, email headers,
HTML tags, etc.

REBOL [
  Title:   "Preface Example"
  Date:    8-Jul-1999
]

print "This file has a preface before the header"

```

#### 2 Embedded Scripts

If a script is to be followed by other text unrelated to the script itself, the script must be enclosed with square brackets [ ]:

```
Here is some text before the script.
[
    REBOL [
        Title:   "Embedded Example"
        Date:    8-Nov-1997
    ]
    print "done"
]
Here is some text after the script.

```

Only white space is permitted between the initial bracket and the word REBOL.

## 3. Script Arguments

When a script is evaluated, it has access to information about itself. This is found in the `system/script` object. The object contains the fields listed in [Object Fields](#83666) for system/script.

|      | **Header** | The header object of the script. This can be used to access the script's title, author, version, date, and other fields. |
| ---- | ---------- | ---------------------------------------- |
|      | **Parent** | If the script was evaluated from another script, this is the system/script object for the parent script. |
|      | **Path**   | The file directory path or URL to the script being evaluated. |
|      | **Args**   | The arguments to the script. These are passed from the operating system command line or from the do function that was used to evaluate the script. |

Examples of using the script object are:

```
print system/script/title

print system/script/header/date

do system/script/args

do system/script/path/script.r

```

The last example evaluates a script called `script`.r in the same directory as the script that is currently running.

### 3.1 Program Options

Scripts also have access to the options provided to the REBOL interpreter when it was started. These are found in the system/options object. The object contains the fields listed in [Object Fields](#16558) for system/options.

|      | **Home**   | The file path as determined by your operating system's environment. This is the path set in the HOME environment variable or system registry for systems that support it. This is the path used to find the rebol.r and user.r files. |
| ---- | ---------- | ---------------------------------------- |
|      | **Script** | The file name of the initial script provided when the interpreter was launched. |
|      | **Path**   | The path to the current directory.       |
|      | **Args**   | The initial arguments provided to the interpreter on the command line. |
|      | **Do-arg** | The string provided as an argument to the --do option on the command line. |

The system/options object also contains additional options that were provided on the command line. Type

```
probe system/options

```

to examine the contents of the options object.

Examples:

```
print system/options/script

probe system/options/args

print read system/options/home/user.r

```

## 4. Running Scripts

There are two ways to run a script: as the initial script when the REBOL interpreter is started, or from the **do**function.

To run a script when starting the interpreter, provide the script name on the command line following the REBOL program name:

```
rebol script.r

```

As soon as the interpreter initializes, the script is evaluated.

From the **do** function, provide the script file name or URL as an argument. The file is loaded into the interpreter and evaluated:

```
do %script.r

do http://www.rebol.com/script.r

```

The **do** function returns the result of the script when it finishes evaluation.

Note that the script file must include a valid REBOL header.

### 4.1 Loading Scripts

Script files can be loaded as data with the **load** function. This function reads the script and translates the script into values, words, and blocks, but does not evaluate the script. The result of the **load** function is a block, unless only a single value was loaded, then that value is returned.

The script argument to the **load** function is a file name, URL, or a string.

```
load %script.r
load %datafile.txt
load http://www.rebol.org/script.r
load "print now"

```

The **load** function performs the following steps:

- Reads the text from the file, URL, or string.
- Searches for a script header, if present.
- Translates data beginning after the header, if found.
- Returns a block containing the translated values.

For example, if a script file buy.r contained the text:

```
Buy 100 shares at $20.00 per share

```

it could be loaded with the line:

```
data: load %buy.r

```

which would result in a block:

```
probe data
[Buy 100 shares at $20.00 per share]

```

****

It should be noted that the "Buy" example above is a dialect of REBOL, not directly executable code. See Chapter 4 on Expressions or Chapter 15 on Parsing for more information.

Note that a file does not require a header to be loaded. The header is necessary only if the file is to be run as a script.

The **load** function supports a few refinements. The load Function Refinements lists the refinements and a description of their functionality:

|      | **/header** | Includes the header if present.          |
| ---- | ----------- | ---------------------------------------- |
|      | **/next**   | Loads only the next value, one value at a time. This is useful for parsing REBOL scripts. |
|      | **/markup** | Treats the file as an HTML or XML file and returns a block that holds its tags and text. |

Normally, **load** does not return the header from the script. But, if the **/header** refinement is used the returned block contains the header object as its first argument.

The **/next** refinement loads the next value and returns a block containing two values. The first returned value is the next value from the series. The second returned value is the string position immediately following the last item loaded.

The **/markup** refinement loads HTML and XML data as a block of tags and strings. All tags are tag data types. All other data are treated as strings.

If the following file contents where loaded with **load/markup:**

```
<title>This is an example</title>

```

a block would be produced:

```
probe data
[<title> "This is an example" </title>]

```

### 4.2 Saving Scripts

Data can be saved to a script file in a format that can be loaded into REBOL with the **load** function. This is a useful way to save data values and blocks of data. In this fashion, it is possible to create entire mini-databases.

The **save** function expects two arguments: a file name and either a block or a value to be saved:

```
data: [Buy 100 shares at $20.00 per share]

save %data.r data

```

The data is written out in REBOL source text format, which can be loaded later with:

```
data: load %data.r

```

Simple values can also be saved and loaded. For instance, a date stamp can be saved with:

```
save %date.r now

```

and later reloaded with:

```
stamp: load %date.r

```

In the previous example, because stamp is a single value, it is not enclosed in a block when loaded.

To save a script file with a header, the header can be provided in a refinement as either an object or a block:

```
header: [Title: "This is an example"]

save/header %data.r data header

```

### 4.3 Commenting Scripts

Commenting is useful for clarifying the purpose of sections of a script. Script headers provide a high level description of the script and comments provide short descriptions of functions. It is also a good idea to provide comments for other parts of your code as well.

A single-line comment is made with a semicolon. Everything following the semicolon to the end of the line is part of the comment:

```
zertplex: 10   ; set to the highest quality

```

You can also use strings for comments. For instance, you can create multi-line comments with a string enclosed in braces:

```
{
    This is a long multilined comment.
}

```

This technique of commenting works only when the string is not interpreted as an argument to a function. If you want to make sure that a multi-line comment is recognized as a comment and is not interpreted as code, precede the string with the word **comment** :

```
comment {
    This is a long multilined comment.
}

```

The **comment** function tells REBOL to ignore the following block or string. *Note that string and block comments are actually part of the script block. Care should be taken to avoid placing them in data blocks, because they would appear as part of the data.*

## 5. Style Guide

REBOL scripts are free-form. You can write a script using the indenting, spacing, line length, and line terminators you prefer. You can put each word on a separate line or join them together on one long line.

While the formatting of your script does not affect the interpreter, it does affect its human readability. Because of this, REBOL Technologies encourages you to follow the standard scripting style described in this section.

Of course, you don't have to follow any of these suggestions. However, scripting style is more important than it first seems. It can make a big difference in the readability and reuse of scripts. Users may judge the quality of your scripts by the clarity of their style. Sloppy scripts often mean sloppy code. Experienced script writers usually find that a clean, consistent style makes their code easier to produce, maintain, and revise.

### 5.1 Formatting

Use the following guidelines for formatting REBOL scripts for clarity.

#### 5.1.1 Indent Content for Clarity

The contents of a block are indented, but the block's enclosing square brackets [ ] are not. That's because the square brackets belong to the prior level of syntax, as they define the block but are not contents of the block. Also, it's easier to spot breaks between adjacent blocks when the brackets stand out.

Where possible, an opening square bracket remains on the line with its associated expression. The closing bracket can be followed by more expressions of that same level. These same rules apply equally to parenthesis ( ) and braces { }.

```
if check [do this and that]

if check [
    do this and do that
    do another thing
    do a few more things
]

either check [do something short][
    do something else]

either check [
    when an expression extends
    past the end of a block...
][
    this helps keep things
    straight
]

while [
    do a longer expression
    to see if it's true
][
    the end of the last block
    and start of the new one
    are at the WHILE level
]

adder: func [
    "This is an example function"
    arg1 "this is the first arg"
    arg2 "this is the second arg"
][
    arg1 + arg2
]

```

An exception is made for expressions that normally belong on a single line, but extend to multiple lines:

```
if (this is a long conditional expression that
    breaks over a line and is indented
)[
    so this looks a bit odd
]

```

This also applies to grouped values that belong together, but must be wrapped to fit on the line:

```
[
    "Hitachi Precision Focus" $1000 10-Jul-1999
        "Computers Are Us"

    "Nuform Natural Keyboard" $70 20-Jul-1999
        "The Keyboard Store"
]

```

#### 5.1.2 Standard Tab Size

REBOL standard tab size is four spaces. Because people use different editors and readers for scripts, you can elect to use spaces rather than tabs.

#### 5.1.3 Detab Before Posting

The tab character (ASCII 9) does not indent four spaces in many viewers, browsers, or shells, so use an editor or REBOL to detab a script before publishing it to the net. The following function detabs a file with standard four-space tabs:

```
detab-file: func [file-name [file!]] [
    write file-name detab read file-name
]
detab-file %script.r

```

The following function converts an eight-space tabs to four-space tabs:

```
detab-file: func [file-name [file!]] [
    write file-name detab entab/size read file-name 8
]

```

#### 5.1.4 Limit Line Lengths to 80 Characters

For ease of reading and portability among editors and email readers, limit lines to 80 characters. Long lines that get wrapped in the wrong places by email clients are difficult to read and have problems loading.

### 5.2 Word Names

Words are a user's first exposure to your code, so it is critical to choose words carefully. A script should be clear and concise. When possible, the words should relate to their English or other human language equivalent, in a simple, direct way.

The following are standard naming conventions for REBOL.

#### 5.2.1 Use the Shortest Word that Communicates the Meaning

Short, crisp words work best where possible:

```
size  time  send  wait  make  quit

```

Local words can often be shortened to a single word. Longer, more descriptive words are better for global words.

#### 5.2.2 Use Whole Words Where Possible

What you save when abbreviating a word is rarely worth it. Type date not dt, or image-file not imgfl.

#### 5.2.3 Hyphenate Multiple Word Names

The standard style is to use hyphens, not character case, to distinguish words.

```
group-name image-file  clear-screen  bake-cake

```

#### 5.2.4 Begin Function Names with a Verb

Function names begin with a verb and are followed by a noun, adverb, or adjective. Some nouns can also be used as verbs.

```
make  print  scan  find  show  hide  take
rake-coals  find-age  clear-screen

```

Avoid unnecessary words. For instance, quit is just as clear as quit-system.

When using a noun as a verb, use special characters such as ? where applicable. For instance, the function for getting the length of a series is **length?**. Other REBOL functions using this naming convention are:

```
size?  dir?  time?  modified?

```

#### 5.2.5 Begin Data Words with Nouns

Words for objects or variables that hold data should begin with a noun. They can include modifiers (adjectives) as needed:

```
image  sound  big-file  image-files  start-time

```

#### 5.2.6 Use Standard Names

There are standard names in REBOL that should be used for similar types of operations. For instance:

```
make-blub           ;creating something new
free-blub           ;releasing resources of something
copy-blub           ;copying the contents of something
to-blub             ;converting to it
insert-blub         ;inserting something
remove-blub         ;removing something
clear-blub          ;clearing something

```

### 5.3 Script Headers

The advantage of using headers is clear. Headers give users a summary of a script and allow other scripts to process the information (like a cataloging script). A minimum header provides a title, date, file name and purpose. Other fields can also be provided such as author, notes, usage, and needs.

```
REBOL [
    Title: "Local Area Defringer"
    Date:  1-Jun-1957
    File:  %defringe.r
    Purpose: {
        Stabilize the wide area ignition transcriber
        using a double ganged defringing algorithm.
    }
]

```

### 5.4 Function Headers

It is useful to provide a description in function specification blocks. Limit such text to one line of 70 characters or less. Within the description, mention what type of value the function normally returns.

```
defringe: func [
    "Return the defringed localization radius."
    area "Topo area to defringe"
    time "Time allotted for operation"
    /cost num "Maximum cost permitted"
    /compound "Compound the calculation"
][
    ...code...
]

```

### 5.5 Script File Names

The best way to name a file is to think about how you can best find that file in a few months. Short and clear names are often enough. Plurals should be avoided, unless meaningful.

In addition, when naming a script, consider how the name will sort in a directory. For instance, keep related files together by starting them with a common word.

```
%net-start.r
%net-stop.r
%net-run.r

```

### 5.6 Embedded Examples

Where appropriate, provide examples within a script to show how the script operates and to give users a quick way of verifying that the script works correctly on their system.

### 5.7 Embedded Debugging

It is often useful to build in debugging functions as part of the script. This is especially true of networking and file handling scripts where it is not desirable to send and write files while running in test mode. Such tests can be enabled with a control variable at the head of the script.

```
verbose: on
check-data: off

```

### 5.8 Minimize Globals

In large scripts and where possible, avoid using global variables that carry their internal state from one module or function to another. For short scripts, this isn't always practical. But recognize that short scripts may become longer scripts over time.

If you have a collection of global variables that are closely related, consider using an object to keep track of them:

```
user: make object! [
    name:  "Fred Dref"
    age:   94
    phone: 707-555-1234
    email: dref@fred.dom
]

```

## 6. Script Cleanup

Here is a short script that can be used to clean up the indentation of a script. It works by parsing the REBOL syntax and reconstructing each line of the script. This example can be found in the REBOL Script Library at www.REBOL.com.

```
out: none ; output text
spaced: off ; add extra bracket spacing
indent: "" ; holds indentation tabs

emit-line: func [] [append out newline]

emit-space: func [pos] [
    append out either newline = last out [indent] [
        pick [#" " ""] found? any [
            spaced
            not any [find "[(" last out
                     find ")]" first pos]
        ]
    ]
]

emit: func [from to] [
    emit-space from append out copy/part from to
]

clean-script: func [
    "Returns new script text with standard spacing."
    script "Original Script text"
    /spacey "Optional spaces near brackets/parens"
    /local str new
] [
    spaced: found? spacey
    out: append clear copy script newline
    parse script blk-rule: [
        some [
            str:
            newline (emit-line) |
            #";" [thru newline | to end] new:
                (emit str new) |
            [#"[" | #"("]
                (emit str 1 append indent tab)
                blk-rule |
            [#"]" | #")"]
                (remove indent emit str 1) |
            skip (set [value new]
                load/next str emit str new) :new
        ]
    ]
    remove out ; remove first char
]

script: clean-script read %script.r

write %new-script.r script
```