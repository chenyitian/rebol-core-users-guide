# String Series

## Contents:

- [1. String Functions](#section-1)
- [2. Converting Values to Strings](#section-2)
  - [2.1 Join](#section-2.1)
  - [2.2 Rejoin](#section-2.2)
  - [2.3 Form](#section-2.3)
  - [2.4 Reform](#section-2.4)
  - [2.5 Mold](#section-2.5)
  - [2.6 Remold](#section-2.6)
  - [2.7 String Spacing Functions](#section-2.7)
  - [2.8 Uppercase and Lowercase](#section-2.8)
  - [2.9 Checksum](#section-2.9)
  - [2.10 Compression and Decompression](#section-2.10)
  - [2.11 Number Base Conversion](#section-2.11)
  - [2.12 Internet Hexadecimal Decoding](#section-2.12)

## 1. String Functions

There are a wide variety of functions that operate on or produce strings. Functions are available for modifying strings, searching strings, compressing and decompressing strings, changing the spacing of strings, parsing strings, and converting strings. These functions operate on all string related datatypes, such as **string!**, **binary!**, **tag!**, **file!**, **URL!**, **email!**, and **issue!**.

The string creation, modification and search functions are covered in the [Series chapter](rebolcore-6.html#_Toc487519750). They include the items listed in [String Functions](#42807).

|      | **copy**    | copy all or part of a string             |
| ---- | ----------- | ---------------------------------------- |
|      | **make**    | allocate storage for a string            |
|      | **insert**  | insert a character or substring into another string |
|      | **remove**  | remove one or more characters from a string |
|      | **change**  | change one or more characters in a string |
|      | **append**  | insert a character or substring at the tail of a string |
|      | **find**    | find or match a character or string in another string |
|      | **replace** | find a string and replace it with another string |

In addition, the series traversing functions like **next**, **back**, **head**, and **tail** were covered. They are used to reposition in strings. In addition, the series test functions allow you to determine your position within a string.

This chapter will introduce functions that convert REBOL values into strings. These functions are used often, and they are also used by the **print** and **probe** functions. They include:

|      | **form**   | convert values with spaces and in human readable format |
| ---- | ---------- | ---------------------------------------- |
|      | **mold**   | convert values in REBOL readable format  |
|      | **join**   | convert values with no spaces            |
|      | **reform** | reduces values before forming them       |
|      | **remold** | reduces values before molding them       |
|      | **rejoin** | reduces values before joining them       |

This chapter will also describes these string functions:

|      | **detab**      | replace tabs with spaces                 |
| ---- | -------------- | ---------------------------------------- |
|      | **entab**      | replace spaces with tabs                 |
|      | **trim**       | remove white space or lines around strings |
|      | **uppercase**  | convert string to uppercase              |
|      | **lowercase**  | convert string to lowercase              |
|      | **checksum**   | compute a checksum for string            |
|      | **compress**   | compress string                          |
|      | **decompress** | decompress string                        |
|      | **enbase**     | convert a string to base value           |
|      | **debase**     | convert an enbased string to a string    |
|      | **dehex**      | convert hexadecimal ASCII values to characters |

## 2. Converting Values to Strings

### 2.1 Join

The **join** function takes two arguments and concatenates them into a single series.

The data type of series returned is based on the value of the first argument. When the first argument is a series value, that series type is returned.

```
str: "abc"
file: %file
url: http://www.rebol.com/

probe join str [1 2 3]
abc123
probe join file ".txt"
%file.txt
probe join url %index.html
http://www.rebol.com/index.html

```

When the first argument is not a series, the **join** converts it to a string first, then performs the append:

```
print join $11 " dollars"
$11.00 dollars
print join 9:11:01 " elapsed"
9:11:01 elapsed
print join now/date " -- today"
30-Jun-2000 -- today
print join 255.255.255.0 " netmask"
255.255.255.0 netmask
print join 412.452 " light-years away"
412.452 light-years away

```

When the second argument to **join** is a block, the values of that block are evaluated and appended to the series returned.

```
print join "a" ["b" "c" 1 2]
abc12
print join %/ [%dir1/ %sub-dir/ %filename ".txt"]
%/dir1/sub-dir/filename.txt
print join 11:09:11 ["AM" " on " now/date]
11:09:11AM on 30-Jun-2000
print join 312.423 [123 987 234]
312.423123987234

```

### 2.2 Rejoin

The **rejoin** function is identical to join, except that it takes one argument, a block.

```
print rejoin ["try" 1 2 3]
try123
print rejoin ["h" 'e #"l" (to-char 108) "o"]
hello

```

### 2.3 Form

The **form** function converts a value to a string:

```
print form $1.50
$1.50
print type? $1.50
money
print type? form $1.50
string

```

The following example uses **form** to find a number by its decimal value:

```
blk: [11.22 44.11 11.33 11.11]
foreach num blk [if find form num ".11" [print num]]
44.11
11.11

```

When **form** is used on a block, all values in the block are converted to string values with spaces between each value:

```
print form [11.22 44.11 11.33]
11.22 44.11 11.33

```

The **form** function does not evaluate the values of a block. This results in words being converted to string values:

```
print form [a block of undefined words]
a block of undefined words
print form [33.44 num "-- unevaluated string:" str]
33.44 num -- unevaluated string: str

```

### 2.4 Reform

The **reform** function is like **form**, except that blocks are reduced before being converted.

```
str1: "Today's date is:"
str2: "The time is now:"
print reform [str1 now/date newline str2 now/time]
Today's date is: 30-Jun-2000 The time is now: 14:41:44

```

The **print** function is based on the **reform** function.

### 2.5 Mold

The **mold** function converts a value to a string that is usable by REBOL. Strings created with **mold** can be converted back to values with the **load** function.

```
blk: [[11 * 4] ($15 - $3.89) "eleven dollars"]
probe blk
[[11 * 4] ($15.00 - $3.89) "eleven dollars"]
molded-blk: mold blk
probe molded-blk
{[[11 * 4] ($15.00 - $3.89) "eleven dollars"]}
print type? blk
block
print type? molded-blk
string
probe first blk
[11 * 4]
probe first molded-blk
#"["

```

The strings returned from **mold** can be loaded by REBOL:

```
new-blk: load molded-blk
probe new-blk
[[11 * 4] ($15.00 - $3.89) "eleven dollars"]
print type? new-blk
block
probe first new-blk
[11 * 4]

```

The **mold** function does not evaluate the values of a block.

```
money: $11.11
sub-blk: [inside another block mold this is unevaluated]
probe mold [$22.22 money "-- unevaluated block:" sub-blk]
{[$22.22 money "-- unevaluated block:" sub-blk]}
probe mold [a block of undefined words]
[a block of undefined words]

```

### 2.6 Remold

The **remold** function works just like **mold**, except that blocks are reduced before being converted.

```
str1: "Today's date is:"
probe remold [str1 now/date]
{["Today's date is:" 30-Jun-2000]}

```

### 2.7 String Spacing Functions

#### 2.7.1 Trim

The **trim** function removes extra spaces from a string.

The default operation of **trim** is to remove extra spaces from the head and tail of a string:

```
str: "  line of text with spaces around it "
print trim str
line of text with spaces around it

```

Note that the string is modified in the process:

```
print str
line of text with spaces around it

```

To trim a copy of the string, write:

```
print trim copy str
line of text with spaces around it

```

Trim includes a number of refinements to specify where space is to be removed from a string:

|      | **/head**  | removes space from the head of the string |
| ---- | ---------- | ---------------------------------------- |
|      | **/tail**  | removes space from the tail of the string |
|      | **/auto**  | removes space from each line, relative to the first line |
|      | **/lines** | removes newlines, replacing them with spaces |
|      | **/all**   | - removes all whitespace                 |
|      | **/with**  | removes all specified characters         |

Use the **/head** and **/tail** refinements to trim from either end of a string:

```
probe trim/head copy str
line of text with spaces around it
probe trim/tail copy str
line of text with spaces around it

```

Use the **/auto** refinement to trim leading spaces from multiple lines leaving indented spaces intact:

```
str: {
    indent text
        indent text
            indent text
        indent text
    indent text
}
print str
indent text
    indent text
        indent text
    indent text
indent text
probe trim/auto copy str
{indent text
    indent text
        indent text
    indent text
indent text
}

```

Use **/lines** to trim the head and tail and also convert newlines into spaces:

```
probe trim/lines copy str
{indent text indent text indent text indent text indent text}

```

Use **/all** to remove all whitespace:

```
probe trim/all copy str
indenttextindenttextindenttextindenttextindenttext

```

The **/with** refinement will remove all characters that you specify. In the following example, spaces, line breaks and the characters `e` and `t` are removed:

```
probe trim/with copy str " ^/et"
indnxindnxindnxindnxindnx

```

#### 2.7.2 Detab and Entab

The **detab** and **entab** will convert tabs to spaces and spaces to tabs.

```
str:
{^(tab)line one
^(tab)^(tab)line two
^(tab)^(tab)^(tab)line three
^(tab)line^(tab)full^(tab)of^(tab)tabs}
print str
line one
        line two
            line three
    line    full    of  tabs

```

By default, the **detab** function converts tabs to four spaces (the REBOL standard spacing). All tabs in the string will be converted to spaces, regardless of where they are located.

```
probe detab str
{    line one
        line two
            line three
    line    full    of  tabs}

```

Note that the **detab** and **entab** functions affect the string that is provided as an argument. To change a copy of the source string, use the **copy** function.

The **entab** function converts spaces to tabs. Every four spaces will be converted to a single tab. Only spaces at the beginning of a line will be converted to tabs.

```
probe entab str
{^-line one
^-^-line two
^-^-^-line three
^-line^-full^-of^-tabs}

```

You can use the **/size** refinement to specify the size of tabs. For instance, if you want to convert each tab to eight spaces, or convert every eight spaces to a tab, you can use this example:

```
probe detab/size str 8
{        line one
                line two
                        line three
        line    full    of      tabs}
probe entab/size str 8
{^-line one
^-^-line two
^-^-^-line three
^-line^-full^-of^-tabs}

```

### 2.8 Uppercase and Lowercase

There are two functions for changing character casing: **uppercase** and **lowercase**. The **uppercase** function takes a string argument and converts its characters to uppercase:

```
print uppercase "SamPle TExT, tO test CASES"
SAMPLE TEXT, TO TEST CASES

```

The **lowercase** function converts characters to lowercase:

```
print lowercase "Sample TEXT, tO teST Cases"
sample text, to test cases

```

To convert only a portion of a string, use the **/part** refinement:

```
print upppercase/part "ukiah" 1
Ukiah

```

### 2.9 Checksum

The **checksum** returns the checksum of the string value. There are three types of checksum that can be computed:

|      | **CRC**    | 24 bit circular redundancy checksum |
| ---- | ---------- | ----------------------------------- |
|      | **TCP**    | standard Internet 16 bit checksum   |
|      | **Secure** | a cryptographically secure checksum |

By default, the CRC checksum is computed:

```
print checksum "hello"
52719
print checksum (read http://www.rebol.com/)
356358

```

To compute a TCP 16-bit checksum, use the **/tcp** refinement:

```
print checksum/tcp "hello"
10943

```

A secure checksum will return a binary value, not an integer. Use the **/secure** refinement to compute a secure checksum:

```
print checksum/secure "hello"
#{AAF4C61DDCC5E8A2DABEDE0F3B482CD9AEA9434D}

```

### 2.10 Compression and Decompression

The **compress** function will compress a string and return a binary datatype. In the following example, a small file is compressed by reading its contents, compressing them, then writing it back to disk:

```
Str:
{I wanted the gold, and I sought it,
  I scrabbled and mucked like a slave.
Was it famine or scurvy -- I fought it;
  I hurled my youth into a grave.
I wanted the gold, and I got it --
  Came out with a fortune last fall, --
Yet somehow life's not what I thought it,
  And somehow the gold isn't all.}

print [size? str "bytes"]
306 bytes
bin: compress str

print [size? bin "bytes"]
156 bytes

```

Note that the result of the compression is a binary data type.

The **decompress** function decompresses a previously compressed string.

```
print decompress bin
I wanted the gold, and I sought it,
  I scrabbled and mucked like a slave.
Was it famine or scurvy -- I fought it;
  I hurled my youth into a grave.
I wanted the gold, and I got it --
  Came out with a fortune last fall, --
Yet somehow life's not what I thought it,
  And somehow the gold isn't all.

```

**Save Your Data**

Always keep an uncompressed backup of compressed data. If you lose only one byte from a compressed binary, it can be difficult to recover the data. Do not store file archives in a compressed format unless you have copies that are not compressed.

### 2.11 Number Base Conversion

To be sent as text, binary strings must be converted to hexadecimal or base64 encoding. This is often done for email and newsgroup content.

The **enbase** function will encode a binary string:

```
line: "No! There's a land!"
print enbase line
Tm8hIFRoZXJlJ3MgYSBsYW5kIQ==

```

Encoded strings can be decoded with the **debase** function. Note that the result is a binary value. To convert it back to a string, use the **to-string** function.

```
b-line: debase e-line
print type? b-line
binary
probe b-line
#{4E6F2120546865726527732061206C616E6421}
print to-string b-line
No! There's a land!

```

The **/base** refinement may be used with **enbase** and **debase** to specify a base2 (binary), base16 (hexadecimal), or base64 encoding.

Here are some examples using base2:

```
e2-str: enbase/base str 2
print e2-str
01100001
b2-str: debase/base e2-str 2
print type? b2-str
binary
probe b2-str
#{61}
print to-string b2-str
a
```

Here are some examples using base16:

```
e16-line: enbase/base line 16
print e16-line
4E6F2120546865726527732061206C616E6421
b16-line: debase/base e16-line 16
print type? b16-line
binary
probe b16-line
#{4E6F2120546865726527732061206C616E6421}
print to-string b16-line
No! There's a land!
```

### 2.12 Internet Hexadecimal Decoding

The **dehex** function converts Internet URL and CGI style hexadecimal encoded characters to strings. Hexadecimal ASCII representations appear in a URL or CGI string as `%xx`, where `xx` is the hexadecimal value.

```
str: "there%20seem%20to%20be%20no%20spaces"
print dehex str
there seem to be no spaces
print dehex "%68%65%6C%6C%6F"
hello
```