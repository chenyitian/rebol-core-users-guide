# Appendix 2 - Errors

## Contents:

[1. Overview](#section-1)
[2. Error Categories](#section-2)
  [2.1 Syntax Errors](#section-2.1)
  [2.2 Script Errors](#section-2.2)
  [2.3 Math Errors](#section-2.3)
  [2.4 Access Errors](#section-2.4)
  [2.5 User Errors](#section-2.5)
  [2.6 Internal Errors](#section-2.6)
[3. Catching Errors](#section-3)
[4. Error Object](#section-4)
[5. Generating Errors](#section-5)
[6. Error Messages](#section-6)
  [6.1 Syntax Errors](#section-6.1)
  [6.2 Script Errors](#section-6.2)
  [6.3 Access Errors](#section-6.3)
  [6.4 Internal Errors](#section-6.4)

## 1. Overview

Errors are exceptions that occur when certain irregular conditions occur. These conditions range from syntax errors to file or network access errors. Here are a few examples:

```
12-30
** Syntax Error: Invalid date -- 12-30.
** Where: (line 1) 12-30
1 / 0
** Math Error: Attempt to divide by zero.
** Where: 1 / 0
read %nofile.r
** Access Error: Cannot open /example/nofile.r.
** Where: read %nofile.r

```

Errors are processed within the system as values of the **error!** datatype. An error is an object that, if evaluated, will print an error message and halt. You can also catch errors and handle them in your script. Errors can be passed to functions, returned from functions, and assigned to variables.

## 2. Error Categories

There are several categories of errors.

### 2.1 Syntax Errors

Syntax errors occur when a script uses REBOL syntax incorrectly. For instance, if a closing bracket is missing or a string is missing its closing quote, a syntax error will occur. These errors only occur during the load or evaluation of a file or string.

### 2.2 Script Errors

Script errors are general run-time errors. For instance, an invalid argument to a function will cause a script error.

### 2.3 Math Errors

Math errors occur when a math operation cannot be processed. For instance, when attempting to divide by zero an error will occur.

### 2.4 Access Errors

Access errors occur when a problem occurs with a file, port or network access. For example, an access error will occur when attempting to read a file that does not exist.

### 2.5 User Errors

User errors are generated explicitly by a script by creating an error value and returning it.

### 2.6 Internal Errors

Internal errors occur within the REBOL interpreter.

## 3. Catching Errors

You can catch errors with the **try** function. The **try** function is similar to the **do** function. It evaluates a block, but always returns a value, even when an error occurs.

When no error occurs, **try** returns the value of a block. For example:

```
print try [100 / 10]
10

```

When an error occurs, try returns the error. If you write:

```
print try [100 / 0]
** Math Error: Attempt to divide by zero.
** Where: 100 / 0

```

the error is returned from the **try** and the **print** function cannot handle it.

To handle errors in a script, you must prevent REBOL from evaluating the error. You can prevent an error from being evaluated by passing it to a function. For instance, the **error?** function will return true when it is passed an error:

```
print error? try [100 / 0]
true

```

You can also print the data type of the value returned from a try:

```
print type? try [100 / 0]
error!

```

The **disarm** function converts an error to an error object that can be examined. In the example below, the error variable holds an error object:

```
error: disarm try [100 / 0]

```

When an error is disarmed, it will be an object! data type, not an error! datatype. Evaluating the disarmed object will not cause an error:

```
probe disarm try [100 / 0]
make object! [
    code: 400
    type: 'math
    id: 'zero-divide
    arg1: none
    arg2: none
    arg3: none
    near: [100 / 0]
    where: none
]

```

Error values can be set to a word before they are disarmed. To set a word to an error, it must be preceded by a function that prevents the error from propagating further. For example:

```
disarm err: try [100 / 0]

```

Setting a variable enables you to access the value of the block later. The example below will print an error or non-error value:

```
either error? result: try [100 / 0] [
    probe disarm result
][
    print result
]

```

## 4. Error Object

The error object shown above has the structure:

```
make object! [
    code: 400
    type: 'math
    id: 'zero-divide
    arg1: none
    arg2: none
    arg3: none
    near: [100 / 0]
    where: none
]

```

Where the fields are:

| **code**  | The error code number. These are obsolete and should not be used. |
| --------- | ---------------------------------------- |
| **type**  | The type field identifies the error category. It is always a word data type of syntax, script, math, access, user, and internal. |
| **id**    | The id field is the name for the error as a word. It identifies the specific error that occurred within the error category. |
| **arg1**  | This field holds the first argument to the error message. For instance, it may include the data type of the value that caused the error. |
| **arg2**  | This field holds the second argument to the error message. |
| **arg3**  | This field holds the third argument to the error message. |
| **near**  | The near field is a code fragment that shows where the error occurred. |
| **where** | The where field is reserved.             |

You can write code that checks any of the error object fields. In this example, the error is printed only when the error id indicates a divide by zero error:

```
error: disarm try [1 / 0]
if error/id = 'zero-divide [
    print {It is a Divide by Zero error}
]
It is a Divide by Zero error

```

The error id word also provides the error block that will be printed by the interpreter. For example:

```
error: disarm try [print zap]
probe get error/id
[:arg1 "has no value"]

```

This block is defined by the system/errors object.

## 5. Generating Errors

User errors can be generated. The simplest way to generate an error is **make** it. Here is an example:

```
make error! "this is an error"
** User Error: this is an error.
** Where: make error! "this is an error"

```

Any of the existing errors can be generated by making the error with a block argument. This block contains the error category name and the error message id name. If the error requires arguments, the arguments follow the message id name. The arguments are what define the `arg1`, `arg2` and `arg3` values in the error object. Here is an example:

```
make error! [script expect-set series! number!]
** Script Error: Expected one of: series! - not: number!.
** Where: make error! [script expect-set series! number!]

```

Custom errors can be entered into the `system/error` object's `user` category. This is done by making a new user category with new entries. These entries are used when generating errors. For instance, the following example enters an error into the user category:

```
system/error/user: make system/error/user [
    my-error: "a simple error"
]

```

Now an error can be generated using the `my-error` message id:

```
if error? err: try [
    make error! [user my-error]
] [probe disarm err]
make object! [
    code: 803
    type: 'user
    id: 'my-error
    arg1: none
    arg2: none
    arg3: none
    near: [make error! [user my-error]]
    where: none
]

```

To create more informative errors, define an error that uses data available when it is generated. This data is included in the disarmed error object and printed as part of the error message. For instance, to use all three argument spaces in an error object:

```
system/error/user: make system/error/user [
    my-error: [:arg1 "doesn't go into" :arg2 "using" :arg3]
]

if error? err: try [
    make error! [user my-error [this] "that" my-function]
] [probe disarm err]
make object! [
    code: 803
    type: 'user
    id: 'my-error
    arg1: [this]
    arg2: "that"
    arg3: 'my-function
    near: [make error! [user my-error [this] "that" my-function]]
    where: none
]

```

The error message generated for `my-error` can be printed without stopping the script:

```
disarmed: disarm err
print bind (get disarmed/id) (in disarmed 'id)
this doesn't go into that using my-function

```

A new library category may be created if there is a need to group a series of errors together by making a new category in `system/error:`

```
system/error: make system/error [
    my-errors: make object! [
        code: 1000
        type: "My Error Category"
        error1: "a simple error"
        error2: [:arg1 "doesn't go into" :arg2 "using" :arg3]
    ]
]

```

The **type** defined in the error object will be the error type printed when the error is generated. The following example illustrates generating an error from both `error1` and `error2` in the `my-error` category.

Generating an error from `error1`. This error requires no arguments:

```
disarmed: disarm try [make error! [my-errors error1]]
print get disarmed/id
a simple error

```

Generating an error from `error2` requires three arguments:

```
disarmed: disarm try [
make error! [my-errors error2 [this] "that" my-function]]
print bind (get disarmed/id) (in disarmed 'id)
this doesn't go into that using my-function

```

Finally, the description that returns the errors defined in `my-errors` may be obtained with:

```
probe get in get disarmed/type 'type
My Error Category

```

## 6. Error Messages

Listed below is a list of all errors defined in the system/error object error catalog.

### 6.1 Syntax Errors

#### 6.1.1 invalid

Data could not be translated into a valid REBOL datatype. In other words, a malformed value was evaluated.

Message:

```
["Invalid" :arg1 "--" :arg2]

```

Example:

```
filter-error try [load "1024AD"]
** Syntax Error: Invalid integer -- 1024AD
** Where: (line 1) 1024AD

```

#### 6.1.2 missing

A block, string or paren expression was left unclosed.

Message:

```
["Missing" :arg2 "at" :arg1]

```

Example:

```
filter-error try [load "("]
** Syntax Error: Missing ) at end-of-script
** Where: (line 1) (

```

#### 6.1.3 header

An attempt was made to evaluate a file as a REBOL script and the file did not have a REBOL header.

Message:

```
Script is missing a REBOL header

```

Example:

```
write %no-header.r {print "data"}
filter-error try [do %no-header.r]
** Syntax Error: Script is missing a REBOL header
** Where: do %no-header.r

```

### 6.2 Script Errors

#### 6.2.1 no-value

An attempt was made to evaluate an undefined word.

Message:

```
[:arg1 "has no value"]

```

Example:

```
filter-error try [undefined-word]
** Script Error: undefined-word has no value
** Where: undefined-word

```

#### 6.2.2 need-value

An attempt was made to define a word to nothing. A set-word was used without an argument.

Message:

```
[:arg1 "needs a value"]

```

Example:

```
filter-error try [set-to-nothing:]
** Script Error: set-to-nothing needs a value
** Where: set-to-nothing:

```

#### 6.2.3 no-arg

A function was evaluated without providing it with all the arguments it was expecting.

Message:

```
[:arg1 "is missing its" :arg2 "argument"]

```

Example:

```
f: func [b][probe b]
filter-error try [f]
** Script Error: f is missing its b argument
** Where: f

```

#### 6.2.4 expect-arg

A function was provided an argument of a datatype it wasn't expecting.

Message:

```
[:arg1 "expected" :arg2 "argument of type:" :arg3]

```

Example:

```
f: func [b [block!]][probe b]
filter-error try [f "string"]
** Script Error: f expected b argument of type: block
** Where: f "string"

```

#### 6.2.5 expect-set

Two series values were used together in a way that was not compatible. For instance, when trying to do a **union**between a string and a block.

Message:

```
["Expected one of:" :arg1 "- not:" :arg2]

```

Example:

```
filter-error try [union [a b c] "a b c"]
** Script Error: Expected one of: block! - not: string!
** Where: union [a b c] "a b c"

```

#### 6.2.6 invalid-arg

This is a generic error for handling values that were used improperly. For instance, when a set-word is used inside of a function's specification block.

Message:

```
["Invalid argument:" :arg1]

```

Example:

```
filter-error try [f: func [word:][probe word]]
** Script Error: Invalid argument: word
** Where: func [word:] [probe word]

```

#### 6.2.7 invalid-op

An attempt was made to use an operator that had been redefined. The operator used is no longer a valid operator.

Message:

```
["Invalid operator:" :arg1]

```

Example:

```
*: "operator redefined to a string"
filter-error try [5 * 10]
** Script Error: Invalid operator: *
** Where: 5 * 10

```

#### 6.2.8 no-op-arg

A math or comparison operator was used without providing the second argument.

Message:

```
Operator is missing an argument

```

Example:

```
filter-error try [1 +]
** Script Error: Operator is missing an argument
** Where: 1 +

```

#### 6.2.9 no-return

A function expecting a block to return a value did not return anything. For instance, when using the **while** or **until** function.

Message:

```
Block did not return a value

```

Examples:

```
filter-error try [ ; first block returns nothing
    while [print 10][probe "ten"]
]
10
** Script Error: Block did not return a value
** Where: while [print 10] [probe "ten"]
filter-error try [
    until [print 10] ; block returns nothing
]
10
** Script Error: Block did not return a value
** Where: until [print 10]

```

#### 6.2.10 not-defined

A word used was not defined within any context.

Message:

```
[:arg1 "is not defined in this context"]

```

#### 6.2.11 no-refine

An attempt was made to use a function refinement that didn't exist for that function.

Message:

```
[:arg1 "has no refinement called" :arg2]

```

Example:

```
f: func [/a] [if a [print "a"]]
filter-error try [f/b]
** Script Error: f has no refinement called b
** Where: f/b

```

#### 6.2.12 invalid-path

An attempt was made to access a block or object value using a path that did not exist within that block or object.

Message:

```
["Invalid path value:" :arg1]

```

Example:

```
blk: [a "a" b "b"]
filter-error try [print blk/c]
** Script Error: Invalid path value: c
** Where: print blk/c
obj: make object! [a: "a" b: "b"]
filter-error try [print obj/d]
** Script Error: Invalid path value: d
** Where: print obj/d

```

#### 6.2.13 cannot-use

An attempt was made to perform an operation on a value of an incompatible datatype. For instance, when attempting to add a string to a number.

Message:

```
["Cannot use" :arg1 "on" :arg2 "value"]

```

Example:

```
filter-error try [1 + "1"]
** Script Error: Cannot use add on string! value
** Where: 1 + "1"

```

#### 6.2.14 already-used

An attempt was made to **alias** a word that had already been aliased.

Message:

```
["Alias word is already in use:" :arg1]

```

Example:

```
alias 'print "prink"
filter-error try [alias 'probe "prink"]
** Script Error: Alias word is already in use: prink
** Where: alias 'probe "prink"

```

#### 6.2.15 out-of-range

An attempt was made to modify an invalid series index.

Message:

```
["Value out of range:" :arg1]

```

Example:

```
blk: [1 2 3]
filter-error try [poke blk 5 "five"]
** Script Error: Value out of range: 5
** Where: poke blk 5 "five"

```

#### 6.2.16 past-end

An attempt was made to access series data beyond the length of the series.

Message:

```
Out of range or past end

```

Example:

```
blk: [1 2 3]
filter-error try [print fourth blk]
** Script Error: Out of range or past end
** Where: print fourth blk

```

#### 6.2.17 no-memory

The system ran out of memory while trying to complete an operation.

Message:

```
Not enough memory

```

#### 6.2.18 wrong-denom

A math operation was performed on money values of two different denominations. For instance, when trying to add USD$1.00 to DEN$1.50.

Message:

```
[:arg1 "not same denomination as" :arg2]

```

Example:

```
filter-error try [US$1.50 + DM$1.50]
** Script Error: US$1.50 not same denomination as DM$1.50
** Where: US$1.50 + DM$1.50

```

#### 6.2.19 bad-press

An attempt was made to decompress a binary value that was corrupt or not a compressed format.

Message:

```
["Invalid compressed data - problem:" :arg1]

```

Example:

```
compressed: compress {some data}
change compressed "1"
filter-error try [decompress compressed]
** Script Error: Invalid compressed data - problem: -3
** Where: decompress compressed

```

#### 6.2.20 bad-port-action

An attempt was made to perform an unsupported action on a port. For instance, when trying to use **find** on a TCP port.

Message:

```
["Cannot use" :arg1 "on this type port"]

```

#### 6.2.21 needs

An attempt was made to run a script that needed either a new version of REBOL or a file that couldn't be found. This information will be found in the script's REBOL header.

Message:

```
["Script needs:" :arg1]

```

#### 6.2.22 locked-word

An attempt was made to modify a protected word. The word will have been protected with the **protect** function.

Message:

```
["Word" :arg1 "is protected, cannot modify"]

```

Example:

```
my-word: "data"
protect 'my-word
filter-error try [my-word: "new data"]
** Script Error: Word my-word is protected, cannot modify
** Where: my-word: "new data"

```

#### 6.2.23 dup-vars

A function was evaluated that had multiple occurrences of a word defined in its specification block. For instance, if the word `arg` was defined as both argument one and two.

Message:

```
["Duplicate function value:" :arg1]

```

Example:

```
filter-error try [f: func [a /local a][print a]]
** Script Error: Duplicate function value: a
** Where: func [a /local a] [print a]

```

### 6.3 Access Errors

#### 6.3.1 cannot-open

A file could not be accessed. This could be a local or network file. Most common reason for this error is a nonexistent directory.

Message:

```
["Cannot open" :arg1]

```

Example:

```
filter-error try [read %/c/path-not-here]
** Access Error: Cannot open /c/path-not-here
** Where: read %/c/path-not-here

```

#### 6.3.2 not-open

An attempt was made to use a port that was closed.

Message:

```
["Port" :arg1 "not open"]

```

Example:

```
p: open %file.txt
close p
filter-error try [copy p]
** Access Error: Port file.txt not open
** Where: copy p

```

#### 6.3.3 already-open

An attempt was made to **open** a port that was already open.

Message:

```
["Port" :arg1 "already open"]

```

Example:

```
p: open %file.txt
filter-error try [open p]
** Access Error: Port file.txt already open
** Where: open p

```

#### 6.3.4 already-closed

An attempt was made to **close** a port that had already been closed.

Message:

```
["Port" :arg1 "already closed"]

```

Example:

```
p: open %file.txt
close p
filter-error try [close p]
** Access Error: Port file.txt not open
** Where: close p

```

#### 6.3.5 invalid-spec

An attempt was made to create a port with **make** using a specification that a port could not be built from.

Message:

```
["Invalid port spec:" :arg1]

```

Example:

```
filter-error try [p: make port! [scheme: 'naughta]]
** Access Error: Invalid port spec: scheme naughta
** Where: p: make port! [scheme: 'naughta]

```

#### 6.3.6 socket-open

The operating system ran out of sockets to allocate.

Message:

```
["Error opening socket" :arg1]

```

#### 6.3.7 no-connect

A connection to another host failed. This is generic error covering a range of reasons for the connection failure. When more information is known about the reason for the connection failure, a more specific error will be thrown.

Message:

```
["Cannot connect to" :arg1]

```

Example:

```
filter-error try [read http://www.host.dom/]
** Access Error: Cannot connect to www.host.dom
** Where: read http://www.host.dom/

```

#### 6.3.8 no-delete

An attempt was made to **delete** a file that was either locked or protected.

Message:

```
["Cannot delete" :arg1]

```

Example:

```
p: open %file.txt
filter-error try [delete %file.txt]
** Access Error: Cannot delete file.txt
** Where: delete %file.txt

```

#### 6.3.9 no-rename

An attempt was made to **rename** a file that was either locked or protected.

Message:

```
["Cannot rename" :arg1]

```

Example:

```
p: open %file.txt
filter-error try [rename %file.txt %new-name.txt]
** Access Error: Cannot rename file.txt
** Where: rename %file.txt %new-name.txt

```

#### 6.3.10 no-make-dir

An attempt was made to create a directory in a file path that did not exist or was write protected.

Message:

```
["Cannot make directory" :arg1]

```

Example:

```
filter-error try [make-dir %/c/no-path/dir]
** Access Error: Cannot make directory /c/no-path/dir/
** Where: m-dir path return path

```

#### 6.3.11 timeout

The timeout period elapsed while waiting to for a response from another host. This timeout is set in the port's `timeout` attribute.

Message:

```
Network timeout

```

#### 6.3.12 new-level

An attempt was made within a script to change the security to a lower level of security that was denied. This is to say, whenever a script requests a lower security setting and the user denies the request, this error is thrown.

Message:

```
["Attempt to change security level to" :arg1]

```

Example:

```
secure quit
filter-error try [secure none] ; denied request

secure none

```

#### 6.3.13 security

A security violation occurred. This will happen when an attempt is made to access a file or the network when the **secure** setting is set to `throw`.

Message:

```
REBOL - Security Violation

```

Example:

```
secure throw
filter-error try [open %file.txt]
** Access Error: REBOL - Security Violation
** Where: open %file.txt
secure none

```

#### 6.3.14 invalid-path

A malformed file path was used.

Message:

```
["Bad file path:" :arg1]

```

Example:

```
filter-error try [read %/]

```

### 6.4 Internal Errors

#### 6.4.1 bad-path

A path was evaluated that began with an invalid word.

Message:

```
["Bad path:" arg1]

```

Example:

```
path: make path! [1 2 3]
filter-error try [path]
** Internal Error: Bad path: 1
** Where: path

```

#### 6.4.2 not-here

An attempt was made to use a REBOL/Command or REBOL/View feature from REBOL/Core.

Message:

```
[arg1 "not supported on your system"]

```

#### 6.4.3 stack-overflow

The system's memory stack overflowed while trying to perform an operation.

Message:

```
["Stack overflow"]

```

Example:

```
call-self: func [][call-self]
filter-error try [call-self]
** Internal Error: Stack overflow
** Where: call-self

```

#### 6.4.4 globals-full

The maximum allowable number of defined global words has been exceeded.

Message:

```
["No more global variable space"]
```