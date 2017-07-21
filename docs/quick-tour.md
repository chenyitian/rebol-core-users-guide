# Chapter 3 - Quick Tour

## Contents:

[1. Overview](#section-1)
[2. Values](#section-2)
  [2.1 Numbers](#section-2.1)
  [2.2 Times](#section-2.2)
  [2.3 Dates](#section-2.3)
  [2.4 Money](#section-2.4)
  [2.5 Tuples](#section-2.5)
  [2.6 Strings](#section-2.6)
  [2.7 Tags](#section-2.7)
  [2.8 Email Addresses](#section-2.8)
  [2.9 URLs](#section-2.9)
  [2.10 Filenames](#section-2.10)
  [2.11 Pairs](#section-2.11)
  [2.12 Issues](#section-2.12)
  [2.13 Binary](#section-2.13)
[3. Words](#section-3)
[4. Blocks](#section-4)
[5. Variables](#section-5)
[6. Evaluation](#section-6)
[7. Functions](#section-7)
[8. Paths](#section-8)
[9. Objects](#section-9)
[10. Scripts](#section-10)
[11. Files](#section-11)
[12. Networking](#section-12)
  [12.1 HTTP](#section-12.1)
  [12.2 FTP](#section-12.2)
  [12.3 SMTP](#section-12.3)
  [12.4 POP](#section-12.4)
  [12.5 NNTP](#section-12.5)
  [12.6 Daytime](#section-12.6)
  [12.7 Whois](#section-12.7)
  [12.8 Finger](#section-12.8)
  [12.9 DNS](#section-12.9)
  [12.10 TCP](#section-12.10)

## 1. Overview

This chapter provides a quick way to familiarize yourself with the REBOL language. Using examples, this chapter presents the basic concepts and structure of the language, illustrating everything from data values to performing network operations.

## 2. Values

A script is written with a sequence of **values**. A wide variety of values exist and you are familiar with many of them from daily experience.

When possible, REBOL also allows the use of international formats for values such as decimal numbers, money, time, and date.

### 2.1 Numbers

Numbers are written as integers, decimals, or scientific notation. For example:

```
1234 -432 3.1415 1.23E12

```

And can also be written in European format:

```
123,4 0,01 1,2E12

```

### 2.2 Times

Time is written in hours and minutes with optional seconds, each separated by colons. For example:

```
12:34 20:05:32 0:25.345 0:25,345

```

Seconds can include a decimal sub-second. Times can also include AM and PM appended without intervening spaces:

```
12:35PM 9:15AM

```

### 2.3 Dates

Dates are written in either international format: day-month-year or year-month-day. A date can also include a time and a time zone. The name or abbreviation of a month can be used to make its format more identifiable in the United States. For example:

```
20-Apr-1998 20/Apr/1998 (USA friendly)

20-4-1998 1998-4-20     (international)

1980-4-20/12:32         (date with time)

1998-3-20/8:32-8:00     (with time zone)

```

### 2.4 Money

Money is written as an optional international three-letter currency symbol followed by a numeric amount. For example:

```
$12.34  USD$12.34  CAD$123.45  DEM$1234,56

```

### 2.5 Tuples

Tuples are used for version numbers, RGB color values, and network addresses. They are written as integers that range from 0 to 255 and are separated by dots. For example:

```
2.3.0.3.1  255.255.0  199.4.80.7

```

At least two dots are required (otherwise the number will be interpreted as a decimal value, not a tuple). Example:

```
2.3.0  ; tuple
2.3.   ; tuple
2.3    ; decimal

```

### 2.6 Strings

Strings are written in a single-line format or a multiline format. Single-line format strings are enclosed in quotes. Multiline format strings are enclosed in braces. Strings that include quotes, tabs, or line breaks must be enclosed in braces using the multiline format. For example:

```
"Here is a single-line string"

{Here is a multiline string that
contains a "quoted" string.}

```

Special characters (escapes) within strings are indicated with the caret character (^). [See the string section in the Values Chapter for the table of escape sequences.](rebolcore-16.html)

### 2.7 Tags

Tags are useful for markup languages such as XML and HTML. Tags are enclosed in angle brackets For example:

```
<title> </body>

<font size="2" color="blue">

```

### 2.8 Email Addresses

Email addresses are written directly in REBOL. They must include an at sign (@). For example:

```
info@rebol.com

pres-bill@oval.whitehouse.gov

```

### 2.9 URLs

Most types of Internet URLs are accepted directly by REBOL. They begin with a scheme name (HTTP for example) followed by a path. For example:

```
http://www.rebol.com

ftp://ftp.rebol.com/sendmail.r

ftp://freda:grid@da.site.dom/dir/files/

mailto:info@rebol.com

```

### 2.10 Filenames

Filenames are preceded by a percent sign to distinguish them from other words. For example:

```
%data.txt

%images/photo.jpg

%../scripts/*.r

```

### 2.11 Pairs

Pairs are used to indicate spatial coordinates, such as positions on a display. They are used to indicate both positions and sizes. Coordinates are separated by an `x`. For example:

```
100x50

1024x800

-50x200

```

### 2.12 Issues

Issues are identification numbers, such as telephone numbers, model numbers, credit card numbers. For example:

```
#707-467-8000

#0000-1234-5678-9999

#MFG-932-741-A

```

### 2.13 Binary

Binary values are byte strings of any length. They can be encoded directly as hexadecimal or base-64. For example:

```
#{42652061205245424F4C}

64#{UkVCT0wgUm9ja3Mh}

```

## 3. Words

Words are the symbols used by REBOL. A word may or may not be a variable, depending on how it is used. Words are also used directly as symbols.

```
show next image

Install all files here

Country State City Street Zipcode

on off true false one none

```

REBOL has no keywords; there are no restrictions on what words are used or how they are used. For instance, you can define your own function called `print` and use it instead of the predefined function for printing values.

Words are not case sensitive and can include hyphens and a few other special characters such as:

```
+ - `  * ! ~ & ? |

```

The following examples illustrate valid words:

```
number?  time?  date!
image-files  l'image
++ -- == +-
***** *new-line*
left&right left|right

```

The end of a word is indicated by a space, a line break, or one of the following characters:

```
[ ] ( ) { } " : ; /

```

The following characters are not allowed in words:

```
@ # $ % ^ ,

```

## 4. Blocks

REBOL is composed by grouping values and words into **blocks**. Blocks are used for code, lists, arrays, tables, directories, associations, and other sequences.

A block is a type of *series* which is a *collection of values* organized in a *specific order*.

A block is enclosed in square brackets [ ]. Within a block, values and words can be organized in any order and can span any number of lines. The following examples illustrate the valid forms of blocks:

```
[white red green blue yellow orange black]

["Spielberg" "Back to the Future" 1:56:20 MCA]

[
    Ted    ted@gw2.dom   #213-555-1010
    Bill   billg@ms.dom  #315-555-1234
    Steve  jobs@apl.dom  #408-555-4321
]

[
    "Elton John"  6894  0:55:68
    "Celine Dion" 68861 0:61:35
    "Pink Floyd"  46001 0:50:12
]

```

Blocks are used for code as well as for data, as shown in the following examples:

```
loop 10 [print "hello"]

if time > 10:30 [send jim news]

sites: [
    http://www.rebol.com [save %reb.html data]
    http://www.cnn.com   [print data]
    ftp://www.amiga.com  [send cs@org.foo data]
]

foreach [site action] sites [
    data: read site
    do action
]

```

A script file itself also is a block. Although it does not include the brackets, the block is implied. For example, if the lines below were put in a script file:

```
red
green
blue
yellow

```

When the file is loaded, it will be a block that contains the words red, green, blue, and yellow. It is equivalent to writing:

```
[red green blue yellow]

```

## 5. Variables

Words can be used as variables that refer to values. To define a word as a variable, follow the word with a colon (:), then the value to which the variable refers as shown in the following examples:.

```
age: 22
snack-time: 12:32
birthday: 20-Mar-1997
friends: ["John" "Paula" "Georgia"]

```

A variable can refer to any type of value, including functions (see [Functions](#_Toc487519697)) and objects (see [Objects](#_Toc487519699)).

A variable refers to a specific value only within a defined context, such as a block, a function, or an entire program. Outside that context the variable can refer to some other value or to no value at all. The context of a variable can span an entire program or it can be restricted to a particular block, function, or object. In other languages, the context of a variable is often referred to as the scope of a variable.

## 6. Evaluation

Blocks are evaluated to compute their results. When a block is evaluated the values of its variables are obtained. The following examples evaluate the variables `age`, `snack-time`, `birthday`, and `friends` that were defined in the previous section:

```
print age
22
if current-time > snack-time [print snack-time]
12:32
print third friends
Georgia

```

A block can be evaluated multiple times by using a loop, as shown in the following examples:

```
loop 10 [prin "*"]  ;("prin" is not a typo, see manual)
**********
loop 20 [
    wait 8:00
    send friend@rebol.com read http://www.cnn.com
]

repeat count 3 [print ["count:" count]]
count: 1
count: 2
count: 3

```

The evaluation of a block returns a result. In the following examples, `5` and `PM` are the results of evaluating each block:

```
print do [2 + 3]
5
print either now/time < 12:00 ["AM"]["PM"]
PM

```

In REBOL there are no special operator precedence rules for evaluating blocks. The values and words of a block are always evaluated from first to last, as shown in the following example:

```
print 2 + 3 * 10
50

```

Parentheses can be used to control the order of evaluation, as shown in the following examples:

```
2 + (3 * 10)
32
(length? "boat") + 2
6

```

You can also evaluate a block and return each result that was computed within it. This is the purpose of the **reduce** function:

```
reduce [1 + 2  3 + 4  5 + 6]
3 7 11

```

## 7. Functions

A function is a block with variables that are given new values each time the block is evaluated. These variables are called the arguments of the function.

In the following example, the word `sum` is set to refer to a function that accepts two arguments, `a` and `b` :

```
sum: func [a b] [a + b]

```

In the above example, **func** is used to define a new function. The first block in the function describes the arguments of the function. The second block is the block of code that gets evaluated when the function is used. In this example, the second block adds two values and returns the result.

The next example illustrates one use of the function `sum` that was defined in the previous example:

```
print sum 2 3
5

```

Some functions need local variables as well as arguments. To define this type of function, use **function**, instead of **func**, as shown in the following example:

```
average: function [series] [total] [
    total: 0
    foreach value series [total: total + value]
    total / (length? series)
]

print average [37 1 42 108]
47

```

In the above example, the word `series` is an argument and the word `total` is a local variable used by the function for calculation purposes.

The function argument block can contain strings to describe the purpose of a function and its argument, as shown in the following example:

```
average: function [
    "Return the numerical average of numbers"
    series "Numbers to average"
] [total] [
    total: 0
    foreach value series [total: total + value]
    total / (length? series)
]

```

These descriptive strings are kept with the function and can be viewed by asking for help about the function, as shown below:

```
help average
USAGE:
    AVERAGE series
DESCRIPTION:
    Return the numerical average of numbers
    AVERAGE is a function value.
ARGUMENTS:
    series -- Numbers to average (Type: any)

```

## 8. Paths

If you are using files and URLs, then you are already familiar with the concept of paths. A path provides a set of values that are used to navigate from one point to another. In the case of a file, a path specifies the route through a set of directories to the location of the file. In REBOL, the values in a path are called **refinements**.

A slash (/) is used to separate words and values in a path, as shown in the following examples of a file path and a URL path:

```
%source/images/globe.jpg

http://www.rebol.com/examples/simple.r

```

Paths can also be used to select values from blocks, pick characters from strings, access variables in objects, and refine the operation of a function, as shown in the following examples:

```
USA/CA/Ukiah/size (block selection)
names/12          (string position)
account/balance   (object function)
match/any         (function option)

```

The **print** function in next example shows the simplicity of using a path to access a mini-database created from a few blocks:

```
towns: [
    Hopland [
        phone #555-1234
        web   http://www.hopland.ca.gov
    ]

        Ukiah [
        phone #555-4321
        web   http://www.ukiah.com
        email info@ukiah.com
    ]
]

print towns/ukiah/web
http://www.ukiah.com

```

## 9. Objects

An object is a set of variables that have specific values in a context. Objects are used for managing data structures and more complex behavior. The following example shows how a bank account is set up as an object to specify its attributes and functions:

```
account: make object! [
  name: "James"
  balance: $100
  ss-number: #1234-XX-4321
  deposit:  func [amount] [balance: balance + amount]
  withdraw: func [amount] [balance: balance - amount]
]

```

In the above example, the words `name`, `balance`, `ss-number`, `deposit`, and `withdraw` are local variables of the `account` object. The `deposit` and `withdraw` variables are functions that are defined within the object. The variables of the account can be accessed with a path, as shown in the next example:

```
print account/balance
$100.00
account/deposit $300

print ["Balance for" account/name "is" account/balance]
Balance for James is $400.00

```

The next example shows how to make another account with a new balance but with all other values remaining the same:

```
checking-account: make account [
    balance: $2000
]

```

Notice that the new object is called checking-account, and it shares the values of the original account, but provides a new balance amount.

Just as easily you can create a new account object that extends the old account object, adding new variables for the bank name and last activity date:

```
account: make account [
    bank: "Savings Bank"
    last-active: 20-Jun-2000
]

print account/balance
$400.00
print account/bank
Savings Bank
print account/last-active
20-Jun-2000

```

## 10. Scripts

A script is a file that holds a block that can be loaded and evaluated. The block can contain code or data, and typically contains a number of sub-blocks.

Scripts require a header to identify the presence of code. The header can include the script title, date, and other information. In the following example of a script, the first block contains the header information:

```
REBOL [
    Title: "Web Page Change Detector"
    File:  %webcheck.r
    Author: "Reburu"
    Date:  20-May-1999
    Purpose: {
        Determine if a web page has changed since it was
        last checked, and if it has, send the new page
        via email.
    }
    Category: [web email file net 2]
]

page: read http://www.rebol.com

page-sum: checksum page

if any [
    not exists? %page-sum.r
    page-sum <> (load %page-sum.r)
][
    print ["Page Changed" now]
    save %page-sum.r page-sum
    send luke@rebol.com page
]

```

## 11. Files

In REBOL, files are easily accessed. The following table describes some of the ways to access files.

You can read a text file with:

```
data: read %plan.txt

```

You can display a text file with:

```
print read %plan.txt

```

To write a text file:

```
write %plan.txt data

```

For instance, you could write out the current time with:

```
write %plan.txt now

```

You can also easily append to the end of a file:

```
write/append %plan data

```

Binary files can be read and written with:

```
data: read/binary %image.jpg

write/binary %new.jpg data

```

To load a file as a REBOL block or value:

```
data: load %data.r

```

Saving a block or a value to a file is just as easy:

```
save %data.r data

```

To evaluate a file as a script (it needs a header to do this.):

```
do %script.r

```

You can read a file directory with:

```
dir: read %images/

```

and, you can then display the file names with:

```
foreach file dir [print file]

```

To make a new directory:

```
make-dir %newdir/

```

To find out the current directory path:

```
print what-dir

```

If you need to delete a file:

```
delete %oldfile.txt

```

You can also rename a file with:

```
rename %old.txt %new.txt

```

To get information about a file:

```
print size? %file.txt

print modified? %file.txt

print dir? %image

```

## 12. Networking

There are a number of Internet protocols built into REBOL. These protocols are easy to use and require very little knowledge of networking.

### 12.1 HTTP

The following example shows how to use the HTTP protocol to read a web page:

```
page: read http://www.rebol.com

```

The next example fetches an image from a web page and writes it to a local file:

```
image: read/binary http://www.page.dom/image.jpg

write/binary %image.jpg image

```

### 12.2 FTP

The following reads and writes files to a server using the file transfer protocol (FTP):

```
file: read ftp://ftp.rebol.com/test.txt

write ftp://user:pass@site.dom/test.txt file

```

The next example gets a directory listing from FTP:

```
print read ftp://ftp.rebol.com/pub

```

### 12.3 SMTP

The following example sends email with the simple mail transfer protocol (SMTP):

```
send luke@rebol.com "Use the force."

```

The next example sends the text of a file as an email:

```
send luke@rebol.com read %plan.txt

```

### 12.4 POP

The following example fetches email with the post office protocol (POP) and prints all of the current messages but leaves them on the server:

```
foreach message read pop://user:pass@mail.dom [
    print message
]

```

### 12.5 NNTP

The following example fetches news with the network news transfer protocol (NNTP), reading all of the news in a particular news group:

```
messages: read nntp://news.server.dom/comp.lang.rebol

```

The next example reads a list of all news group and prints them:

```
news-groups: read nntp://news.some-isp.net

foreach group news-groups [print group]

```

### 12.6 Daytime

The following example gets the current time from a server:

```
print read daytime://everest.cclabs.missouri.edu

```

### 12.7 Whois

The following example finds out who is in charge of a domain using the whois protocol:

```
print read whois://rebol@rs.internic.net

```

### 12.8 Finger

The following example gets user information with the finger protocol:

```
print read finger://username@host.dom

```

### 12.9 DNS

The following example determines an Internet address from a domain name and a domain name from an address:

```
print read dns://www.rebol.com

print read dns://207.69.132.8

```

### 12.10 TCP

Direct connections with TCP/IP are also possible in REBOL. The following example is a simple, but useful, server that waits for connections on a port, then executes whatever has been sent:

```
server-port: open/lines tcp://:9999

forever [
    connection-port: first server-port
    until [
        wait connection-port
        error? try [do first connection-port]
    ]
    close connection-port
]
```