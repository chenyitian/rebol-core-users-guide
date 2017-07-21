# Values

## Contents:

- [1. Number Values](#section-1)
  - [1.1 Decimal](#section-1.1)
  - [1.2 Integer](#section-1.2)
- [2. Series Values](#section-2)
  - [2.1 Binary](#section-2.1)
  - [2.2 Block](#section-2.2)
  - [2.3 Email](#section-2.3)
  - [2.4 File](#section-2.4)
  - [2.5 Hash](#section-2.5)
  - [2.6 Image](#section-2.6)
  - [2.7 Issue](#section-2.7)
  - [2.8 List](#section-2.8)
  - [2.9 Paren](#section-2.9)
  - [2.10 Path](#section-2.10)
  - [2.11 String](#section-2.11)
  - [2.12 Tag](#section-2.12)
  - [2.13 URL](#section-2.13)
- [3. Other Values](#section-3)
  - [3.1 Character](#section-3.1)
  - [3.2 Date](#section-3.2)
  - [3.3 Logic](#section-3.3)
  - [3.4 Money](#section-3.4)
  - [3.5 None](#section-3.5)
  - [3.6 Pair](#section-3.6)
  - [3.7 Refinement](#section-3.7)
  - [3.8 Time](#section-3.8)
  - [3.9 Tuple](#section-3.9)
  - [3.10 Words](#section-3.10)

## 1. Number Values

### 1.1 Decimal

#### 1.1.1 Concept

The **decimal!** datatype is based on 64-bit standard IEEE floating point numbers. They are distinguished from integer numbers by a decimal point (a period or a comma is allowed for international usage, see the notes below).

#### 1.1.2 Format

Decimal values are a sequence of numeric digits, followed by a decimal point, which can be a period (.) or a comma (,), followed by more digits. A plus (+) or minus (-) immediately before the first digit indicates sign. Leading zeros before the decimal point are ignored. Extra spaces, commas, and periods are not allowed.

```
1.23
123.
123.0
0.321
0.123
1234.5678

```

A comma can be used in place of a period to represent the decimal point (which is the standard in many countries):

```
1,23
0,321
1234,5678

```

Use a single quote (`) to separate the digits in long decimals. Single quotes can appear anywhere after the first digit in the number, but not before the first digit.

```
100'234'562.3782
100'234'562,3782

```

Do not use commas or periods separate the digits in a decimal value.

Scientific notation can be used to specify the exponent of a number by appending the number with the letter **E** or **e**followed by a sequence of digits. The exponent can be a positive or negative number.

```
1.23E10
1.2e007
123.45e-42
56,72E300
-0,34e-12
0.0001e-001

```

Decimal numbers span from 2.2250738585072e-308 up to 1.7976931348623e+308 and can contain up to 15 digits of precision.

#### 1.1.3 Creation

Use the **to-decimal** function to convert **string!**, **integer!**, **block!**, or **decimal!** datatypes to a decimal number:

```
probe to-decimal "123.45"
123.45
probe to-decimal 123
123
probe to-decimal [-123 45]
-1.23E+47
probe to-decimal [123 -45]
1.23E-43
probe to-decimal -123.8
-123.8
probe to-decimal 12.3
12.3

```

If a decimal and integer are combined in an expression, the integer is converted to a decimal number:

```
probe 1.2 + 2
3.2
probe 2 + 1.2
3.2
probe 1.01 > 1
true
probe 1 > 1.01
false

```

#### 1.1.4 Related

Use **decimal?** to determine whether a value is an **decimal!** datatype.

```
print decimal? 0.123
true

```

Use the **form**, **print**, and **mold** functions with an integer argument to print a decimal value in its simplest form:

- integer. If it can be represented as one.
- decimal without exponent. If it's not too big or too small.
- scientific notation. If it's too big or small.

For example,

```
probe mold 123.4
123.4
probe form 2222222222222222
2.22222222222222E+15
print 1.00001E+5
100001

```

Single quotes (`) and a leading plus sign (+) do not appear in decimal output:

```
print +1'100'200.222'112
1100200.222112

```

### 1.2 Integer

#### 1.2.1 Concept

The **integer!** datatype includes 32-bit positive and negative numbers and zero. Unlike decimal numbers, integers do not contain a decimal point.

#### 1.2.2 Format

Integer values consist of a sequence of numeric digits. A plus (+) or minus (-) immediately before the first digit indicates sign. (There cannot be a space between the sign and the first digit.) Leading zeros are ignored.

```
0 1234 +1234 -1234 00012 -0123

```

Do not use commas or periods in integers. If a comma or period is found within an integer it is interpreted as a decimal value. However, you can use a single quote (`) to separate the digits in long integers. Single quotes can appear anywhere after the first digit in the number, but not before the first digit.

```
2'147'483'647

```

Integers span a range from -2147483648 to 2147483647.

#### 1.2.3 Creation

Use the **to-integer** function to convert a **string!**, **logic!**, **decimal!**, or **integer!** datatype to an integer:

```
probe to-integer "123"
123
probe to-integer false
0
probe to-integer true
1
probe to-integer 123.4
123
probe to-integer 123.8
123
probe to-integer -123.8
-123

```

If a decimal and integer are combined in an expression, the integer is converted to a decimal:

```
probe 1.2 + 2
3.2
probe 2 + 1.2
3.2
probe 1.01 > 1
true
probe 0 < .001
true

```

#### 1.2.4 Related

Use **integer?** to determine whether a value is an **integer!** datatype.

```
probe integer? -1234
true

```

Use the **form**, **print**, and **mold** functions with an integer argument to print a integer value as a string:

```
probe mold 123
123
probe form 123
123
print 123
123

```

Integers that are out of range or cannot be represented in 32 bits are flagged as an error.

## 2. Series Values

### 2.1 Binary

#### 2.1.1 Concept

Binary values hold binary data of any arbitrary type. Any sequence of bytes can be stored, such as an image, audio, executable file, compressed data, and encrypted data. The source format for binary data can be base-2 (binary), base-16 (hex), and base-64. The default base for binary data in REBOL is base-16.

#### 2.1.2 Format

Binary strings are written as a number sign (#) followed by a string enclosed in braces. The characters within the string are encoded in one of several formats as specified by an optional number prior to the number sign. Base-16 is the default format.

```
#{3A18427F 899AEFD8} ; default base-16
2#{10010110110010101001011011001011} ; base-2
64#{LmNvbSA8yw9CB0aGvXmgUkVCu2Uz934b} ; base-64

```

Spaces, tabs and newlines are permitted within the string. Binary data can span multiple lines.

```
probe #{
    3A
    18
    92
    56
}
#{3A189256}

```

Strings that are missing the correct number of characters to create a correct binary result are padded on the right.

#### 2.1.3 Creation

The **to-binary** function converts data to the **binary!** datatype at the default base set in **system/options/binary-base:**

```
probe to-binary "123"
#{313233}
probe to-binary "today is the day..."
#{746F64617920697320746865206461792E2E2E}

```

To convert an integer into its binary value, pass it in a block:

```
probe to-binary [1]
#{01}
probe to-binary [11]
#{0B}

```

Converting a series of integers into a binary, returns the bit conversion for each integer concatenated into a single binary value:

```
probe to-binary [1 1 1 1]
#{01010101}

```

#### 2.1.4 Related

Use **binary?** determine whether a value is an **binary!** datatype.

```
probe binary? #{616263}
true

```

Binary values are a type of series:

```
probe series? #{616263}
true
probe length? #{616263} ; three hex values in this binary
3

```

Closely related to working with **binary!** datatypes are the functions **enbase** and **debase**. The **enbase** function converts strings to their base-2, base-16 or base-64 representations as strings. The **debase** function converts enbased strings to a binary value of the base specified in **system/options/binary-base**.

### 2.2 Block

#### 2.2.1 Concept

Blocks are groups of values and words. Blocks are used everywhere, from a script itself to blocks of data and code provided in a script.

Block values are indicated by opening and closing square brackets ([ ]) with any amount of data contained between them.

```
[123 data "hi"]  ; block with data
[]               ; empty block

```

Blocks can hold records of information:

```
woodsmen: [
    "Paul" "Bunyan" paul@bunyan.dom
    "Grizzly" "Adams" grizzly@adams.dom
    "Davy" "Crocket" davy@crocket.dom
]

```

Blocks can contain code:

```
[print "this is a segment of code"]

```

Blocks are also a type of series, and thus anything that can be done with a series can be done with a block value.

Blocks can be searched:

```
probe copy/part (find woodsmen "Grizzly") 3
[
    "Grizzly" "Adams" grizzly@adams.dom]

```

Blocks can be modified:

```
append woodsmen [
    "John" "Muir" john@muir.dom
]
probe woodsmen
[
    "Paul" "Bunyan" paul@bunyan.dom 
    "Grizzly" "Adams" grizzly@adams.dom 
    "Davy" "Crocket" davy@crocket.dom 
    "John" "Muir" john@muir.dom
]

```

Blocks can be evaluated:

```
blk: [print "data in a block"]
do blk
data in a block

```

Blocks can contain blocks:

```
blks: [
    [print "block one"]
    [print "block two"]
    [print "block three"]
]
foreach blk blks [do blk]
block one
block two
block three

```

#### 2.2.2 Format

Blocks can contain any number of values or no values at all. They can extend over multiple lines and can include any type of value, including other blocks.

An empty block:

```
[ ]

```

A block of integers:

```
[24 37 108]

```

A REBOL header:

```
REBOL [
    Title: "Test Script"
    Date: 31-Dec-1998
    Author: "Ima User"
]

```

The condition and evaluation block of a function:

```
while [time < 10:00] [
    print time
    time: time + 0:10
]

```

Words in a block need not be defined:

```
blk: [undefined words in a block]
probe value? pick blk 1
false

```

Blocks allow any number of lines, spaces, or tabs. Lines and spaces can be placed anywhere within the block, so long as they do not divide a single value.

#### 2.2.3 Creation

The **to-block** function converts data to the **block!** datatype:

```
probe to-block luke@rebol.com
[luke@rebol.com]
probe to-block {123 10:30 "string" luke@rebol.com}
[123 10:30 "string" luke@rebol.com]

```

#### 2.2.4 Related

Use **block?** to determine whether a value is an **block!** datatype.

```
probe block? [123 10:30]
true

```

As blocks are a subset of the **series!** pseudotype, use **series?** to check this:

```
probe series? [123 10:30]
true

```

Using **form** on a block value creates a string from the contents contained in the block:

```
probe form [123 10:30]
123 10:30

```

Using **mold** on a block value creates a string from the block value and it's contents, thus allowing it to be reloaded as a REBOL block value:

```
probe mold [123 10:30]
[123 10:30]

```

Closely related datatypes are **hash!** and **list!**. They are used in much the same way as block values, but have special capabilities. List values are designed to handle modification of lists more quickly than block values, and hash values are designed handle data lookup and hash indexing of data. These are useful when dealing with large data sets.

### 2.3 Email

#### 2.3.1 Concept

An email address is a datatype. The **email!** datatype allows for easy expression of email addresses:

```
send luke@rebol.com {some message}

emails: [
    john@keats.dom
    lord@byron.dom
    edger@guest.dom
    alfred@tennyson.dom
]
mesg: {poetry reading at 8:00pm!}
foreach email emails [send email mesg]

```

Email is also one of the **series!** datatypes, so the same rules that apply to series apply to emails:

```
probe head change/part jane@doe.dom "john" 4
john@doe.dom

```

#### 2.3.2 Format

The standard format of an email address is a name, followed by an at sign (@), followed by a domain. An email address can be of any length, but must not include any of restricted characters, such as square brackets, quotes, braces, spaces, newlines, etc..

The following **email!** datatype formats are valid:

```
info@rebol.com
123@number-mail.org
my-name.here@an.example-domain.com

```

Upper and lower cases are preserved in email addresses.

#### 2.3.3 Access

Refinements can be used with an email value to get the user name or domain. The refinements are:

- /user - Get the user name.
- /host - Get the domain.

Here's how these refinements work:

```
email: luke@rebol.com
probe email/user
luke
probe email/host
rebol.com

```

#### 2.3.4 Creation

The **to-email** function converts data to the **email!** datatype:

```
probe to-email "info@rebol.com"
info@rebol.com
probe to-email [info rebol.com]
info@rebol.com
probe to-email [info rebol com]
info@rebol.com
probe to-email [user some long domain name out there dom]
user@some.long.domain.name.out.there.dom

```

#### 2.3.5 Related

Use **email?** to determine whether a value is an **email!** datatype.

```
probe email? luke@rebol.com
true

```

As emails are a subset of the **series!** pseudotype, use **series?** to determine whether the value is a series:

```
probe series? luke@rebol.com
true
probe pick luke@rebol.com 5
#"@"

```

### 2.4 File

#### 2.4.1 Concept

The **file!** datatype can be a file name, directory name, or directory path.

```
%file.txt
%directory/
%directory/path/to/some/file.txt

```

File values are a subset of series, and thus can be manipulated as a series:

```
probe find %dir/path1/path2/file.txt "path2"
%path2/file.txt
f: %dir/path/file.txt
probe head remove/part (find f "path/") (length? "path/")
%dir/file.txt

```

#### 2.4.2 Format

Files are designated with a percent sign (%)followed by a sequence of characters:

```
load %image.jpg
prog: load %examples.r
save %this-file.txt "This file has few words."
files: load %../programs/

```

Unusual characters in file names must be encoded with a % hexadecimal number, which is an Internet convention. A file name with a space (hexadecimal 20) would look like:

```
probe %cool%20movie%20clip.mpg
%cool%20movie%20clip.mpg
print %cool%20movie%20clip.mpg
cool movie clip.mpg

```

Another format is to enclose the file name in quotes:

```
probe %"cool movie clip.mpg"
%cool%20movie%20clip.mpg
print %"cool movie clip.mpg"
cool movie clip.mpg

```

The standard character for separating directories in a path is the forward slash (/), not the backslash (\). However, the REBOL language automatically converts backslashes found in file names to forward slashes:

```
probe %\some\path\to\some\where\movieclip.mpg
%/some/path/to/some/where/movieclip.mpg

```

#### 2.4.3 Creation

The **to-file** function converts data to the **file!** datatype:

```
probe to-file "testfile"
%testfile

```

When passed a block, elements in the block are concatenated into a file path with the final element used as the file name:

```
probe to-file [some path to a file the-file.txt]
%some/path/to/a/file/the-file.txt

```

#### 2.4.4 Related

Use **file?** to determine whether a value is an **file!** datatype.

```
probe file? %rebol.r
true

```

As files are a subset of the **series!** pseudotype, use **series?** to check this:

```
probe series? %rebol.r
true

```

### 2.5 Hash

#### 2.5.1 Concept

Hash is a block that is specially organized to make finding data faster. When searching is performed on a hash block, the search is performed by using a hash table for lookup. For large blocks, this can speed searches by hundreds of times.

#### 2.5.2 Format

Hash blocks must be constructed by using **make** or **to-hash**. They have no lexical format.

#### 2.5.3 Creation

Use **make** to initialize a hash block:

```
hsh: make hash! 10 ; allocating space for 10 elements

```

The **to-hash** function converts data to the hash datatype.

Convert a block:

```
blk: [1 "one" 2 "two" 3 "three" 4 "four"]
probe hash: to-hash blk
make hash! [1 "one" 2 "two" 3 "three" 4 "four"]
print select hash 2
two

```

Convert various values:

```
probe to-hash luke@rebol.com

probe to-hash 123.5

probe to-hash {123 10:30 "string" luke@rebol.com}

```

#### 2.5.4 Related

Use **hash?** to test the datatype.

```
hsh: to-hash [1 "one" 2 "two" 3 "three" 4 "four"]
probe hash? Hsh
true

```

As hashes are a subset of the series! pseudotype, use **series?** to check this:

```
probe series? hsh
true

```

Forming a hash value creates a string from the contents contained in the hash:

```
probe form hsh
"1 one 2 two 3 three 4 four"

```

Molding a hash value creates a string of the hash value itself and its contents, thus allowing it to be reloaded as a REBOL hash value:

```
probe mold hsh
make hash! [1 "one" 2 "two" 3 "three" 4 "four"]

```

### 2.6 Image

#### 2.6.1 Concept

The **image!** datatype is a series that holds RGB images. This datatype is used with REBOL/View.

The image formats supported are GIF, JPEG, and BMP. The loaded image can be manipulated as a series.

#### 2.6.2 Format

Images are normally loaded from a file. However, they can be expressed in source code as well by making an image. The block provided includes the image size and its RGB data.

```
image: make image! [192x144 #{
    B34533B44634B44634B54735B7473
    84836B84836B84836BA4837BA4837
    BC4837BC4837BC4837BC4837BC483 ...
}

```

#### 2.6.3 Creation

Empty images can be created using **make** or **to-image:**

```
empty-img: make image! 300x300
empty-img: to-image 150x300

```

The size of the image is provided.

Images can also be made from snapshots of a face object. This is also done using **make** or **to-image:**

```
face-shot: make image! face
face-shot: to-image face

```

Use **load** to load an image file. If the image's format is not supported, it will fail to load.

Loading an image:

```
img: load %bay.jpg

```

#### 2.6.4 Related

Use **image?** to determine whether a value is the **image!** datatype:

```
probe image? img

```

Images are a subset of the **series!** pseudotype:

```
probe series? img

```

Use the **/size** refinement to return the pixel size of an image as a pair value:

```
probe img/size

```

The pixel values of an image are obtained using **pick** and changed using **poke**. The value returned by **pick** is an RGB tuple value. The value replaced with **poke** also should be a tuple value.

Picking specific pixels:

```
probe pick img 1 

probe pick img 1500

```

Poking specific pixels:

```
poke img 1 255.255.255 
probe pick img 1 

poke img 1500 0.0.0 
probe pick img 1500

```

### 2.7 Issue

#### 2.7.1 Concept

An **issue!** is a series of characters used to sequence symbols or identifiers for things like telephone numbers, model numbers, serial numbers, and credit card numbers.

Issue values are a subset of series, and thus can be manipulated as series:

```
probe copy/part find #888-555-1212 "555" 3
#555

```

#### 2.7.2 Format

Issues start with a number sign (#) and continue until the first delimiting character (such as a space) is reached.

```
#707-467-8000
#A-0987654321-CD-09876
#1234-5678-4321-8765
#MG82/32-7

```

Values that contain delimiting characters should be written as strings rather than issues.

#### 2.7.3 Creation

The **to-issue** function converts data to the **issue!** datatype:

```
probe to-issue "1234-56-7890"
#1234-56-7890

```

#### 2.7.4 Related

Use **issue?** to determine whether a value is an **issue!** datatype.

```
probe issue? #1234-56-7890
true

```

As issues are a subset of the series pseudotype, use **series?** to check this:

```
probe series? #1234-56-7890
true

```

The **form** function returns an issue as a string without the number sign (#):

```
probe form #1234-56-7890
1234-56-7890

```

The **mold** function returns an issue as a string that can be read by REBOL as an issue value:

```
probe mold #1234-56-7890
#1234-56-7890

```

The **print** function prints an issue to standard output after doing a **reform** on it:

```
print #1234-56-7890
1234-56-7890

```

### 2.8 List

#### 2.8.1 Concept

Lists are linked list blocks that allow for faster and more efficient insertion and removal of their values. They can be used in cases where a large number of insertions or removals are being performed on large blocks.

#### 2.8.2 Format

List blocks must be constructed by using **make** or **to-list**. They have no lexical format.

Lists values are not a direct substitute for blocks. There are a couple of differences between blocks and lists:

- Inserting into a list modifies its reference to just after the point of insertion.
- Removing the element currently referenced in a list causes the reference to reset to the tail of the list

The following examples show the difference in behavior between inserting into a list and a block.

Initializing a block and list:

```
blk: [1 2 3]

lst: to-list [1 2 3]

```

Inserting into a block and list:

```
insert blk 0

insert lst 0

```

Looking at the word after the block and list after insertion. Notice **blk** points to the head, as before the insertion of **0**, but **lst** points to just after the point of insertion:

```
print blk
0 1 2 3
print lst
1 2 3
print head lst
0 1 2 3

```

The following examples show the difference in behavior between removing an element from a list and a block.

Initializing a block and a list:

```
blk: [1 2 3]

lst: to-list [1 2 3]

```

Removing from the block and list:

```
remove blk

remove lst

```

Looking at the word after removal of the value. Notice **lst** now points to the tail of the series:

```
print blk
2 3
print tail? lst
true
print head lst
2 3

```

If you don't want the word to be at the tail after removing a value, step forward and remove the value behind the current index. The following examples depicts this.

Initializing a list:

```
lst: to-list [1 2 3]

```

Stepping forward and removing the value behind the current index:

```
remove back (lst: next lst)

```

Looking at the word after removing the value:

```
probe lst
make list! [2 3]

```

#### 2.8.3 Creation

Use **make** to initialize a list value:

```
lst: make list! 10 ; allocating space for 10 elements

```

The **to-list** function converts data to the **list!** datatype:

Convert a block:

```
blk: [1 "one" 2 "two" 3 "three" 4 "four"]
probe to-list blk

```

#### 2.8.4 Related

Use **list?** to determine whether a value is an **list!** datatype.

```
lst: to-list [1 "one" 2 "two" 3 "three" 4 "four"]
probe list? Lst
true

```

Since lists are a subset of the **series!** datatype, use **series?** to check whether a list is a series:

```
probe series? lst
true

```

Using **form** on a list value creates a string from the contents contained in the list:

```
probe form lst
"1 one 2 two 3 three 4 four"

```

Using **mold** on a list value creates a string of the list value itself and it's contents, thus allowing it to be reloaded as a REBOL list value:

```
probe mold lst
make list! [1 "one" 2 "two" 3 "three" 4 "four"]

```

### 2.9 Paren

#### 2.9.1 Concept

A **paren!** datatype is a block that is immediately evaluated. It is identical to a block in every way, except that it is evaluated when it is encountered and its result is returned.

When used within an evaluated expression, a **paren!** allows you to control the order of evaluation:

```
print 1 + (2 * 3)
7
print 1 + 2 * 3
9

```

The value of a **paren!** can be accessed and modified in the same way as any block. However, when referring to a **paren!**, care must be taken to prevent if from being evaluated. If you store a paren in a variable, you will need to use a get-word form (:word) to prevent it from being evaluated.

Parens are a type of series, thus anything that can be done with a series can be done with paren values.

```
paren: first [(1 + 2 * 3 / 4)]

print type? :paren
paren!
print length :paren
7
print first :paren
1
print last :paren
4
insert :paren [10 + 5 *]
probe :paren
(10 + 5 * 1 + 2 * 3 / 4)
print paren
12.75

```

#### 2.9.2 Format

Parens are identified by their open and closing parenthesis. They can span multiple lines and contain any data, including other paren values.

#### 2.9.3 Creation

The **make** function can be used to allocate a paren value:

```
paren: make paren! 10
insert :paren 10
insert :paren `+
insert :paren 20

print :paren
20 + 10
print paren
30

```

The **to-paren** function converts data to the **paren!** datatype:

```
probe to-paren "123 456"
(123 456)
probe to-paren [123 456]
(123 456)

```

#### 2.9.4 Related

Use **paren?** to test the datatype.

```
blk: [(3 + 3)]
probe pick blk 1
(3 + 3)
probe paren? pick blk 1
true

```

As parens are a subset of the **series!** pseudotype, use **series?** to check this:

```
probe series? pick blk 1
true

```

Using **form** on a paren value creates a string from the contents contained in the paren:

```
probe form pick blk 1
3 + 3

```

### 2.10 Path

#### 2.10.1 Concept

Paths are a collection of words and values delineated with forward slashes (/). Paths are used to navigate to or find something. The words and values of a path are called refinements, and they are combined to provide a means of navigating through a value or function.

Paths can be used on blocks, files, strings, lists, hashes, functions, and objects. How a path operates depends on the datatype being used.

Paths can be used to select values from blocks, pick characters from strings, access variables in objects, refine the operation of a function:

```
USA/CA/Ukiah/size (block selection)

names/12          (string position)

account/balance   (object function)

match/any         (function option)

```

The example below shows the simplicity of using a path to access a mini-database created from a few blocks:

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

Summary of path constructs:

| Action         | Type Word     | Type Test     | Conversion      |
| -------------- | ------------- | ------------- | --------------- |
| **path/word:** | **set-path!** | **set-path?** | **to-set-path** |
| **path/word**  | **path!**     | **path?**     | **to-path**     |
| **'path/word** | **lit-path!** | **lit-path?** | **to-lit-path** |

Examples of paths:

Evaluate an object's function:

```
obj: make object! [
    hello: func [] [print "hello! hello!"]
]
obj/hello
hello! hello!

```

Evaluate an object's word:

```
obj: make object! [
    text: "do you believe in magic?"
]
probe obj/text
do you believe in magic?

```

Function refinements:

```
hello: func [/again] [
    print either again ["hello again!"]["hello"]
]
hello/again
hello again!

```

Select from blocks, or multiple blocks:

```
USA: [
    CA [
        Ukiah [
            population 15050
            elevation [610 feet]
        ]
        Willits [
            population 5073
            elevation [1350 feet]
        ]
    ]
]
print USA/CA/Ukiah/population
15050
print form USA/CA/Willits/elevation
1350 feet

```

Pick elements from series and embedded series by their numeric position:

```
string-series: "abcdefg"
block-series: ["John" 21 "Jake" 32 "Jackson" 43 "Joe" 52]
block-with-sub-series: [ "abc" [4 5 6 [7 8 9]]]
probe string-series/4
#"d"
probe block-series/3
Jake
probe block-series/6
43
probe block-with-sub-series/1/2
#"b"
probe block-with-sub-series/2/2
5
probe block-with-sub-series/2/4/2
8

```

The words supplied as paths are symbolic and therefore unevaluated. This is necessary to allow the most intuitive form for object referencing. To use a word's reference, an explicit word value reference is required:

```
city: 'Ukiah
probe USA/CA/:city
[
    population 15050 
    elevation "610 feet"
]

```

Paths in blocks, hashes, or objects are evaluated by matching the word at the top level of the path, and verifying the word as a **block!**, **hash!** or **object!** value. Then the next word in the path is sought as a word expressed in the block, hash or object and an implicit **select** is performed. The value following the word matched is returned. When the returned value is a block, hash, or object, the path can be extended:

Getting the value associated with **CA** in **USA:**

```
probe USA/CA
[
    Ukiah [
        population 15050 
        elevation "610 feet"
    ] 
    Willits [
        population 9935 
        elevation "1350 feet"
    ]
]

```

Getting the value associated with **Willits** in **USA/CA:**

```
probe USA/CA/Willits
[
    population 9935 
    elevation "1350 feet"
]

```

Getting the value associated with **population** in **USA/CA/Willits:**

```
probe USA/CA/Willits/population
9935

```

When a word is used in a path that does not exist at the given point in the structure, an error is produced:

```
probe USA/CA/Mendocino
** Script Error: Invalid path value: Mendocino.
** Where: probe USA/CA/Mendocino

```

Paths can be used to change values in blocks and objects:

```
USA/CA/Willits/elevation: "1 foot, after the earthquake"
probe USA/CA/Willits
[
    population 9935 
    elevation "1 foot, after the earthquake"
]
obj/text: "yes, I do believe in magic."
probe obj
make object! [
    text: "yes, I do believe in magic."
]

```

Blocks, hashes, functions, and objects can be mixed in paths.

Selecting from elements in a block inside an object:

```
obj: make object! [
    USA: [
        CA [
            population "too many"
        ]
    ]
]
probe obj/USA/CA/population
too many

```

Using function refinements within an object:

```
obj: make object! [
    hello: func [/again] [
        print either again [
            "hello again"
        ] [
            "oh, hello"
        ]
    ]
]
obj/hello/again
hello again

```

Paths are a type of series, thus anything that can be done with a series can be done with path values:

```
root: [sub1 [sub2 [
    word "a word at the end of the path"
    num 55
]   ]   ]
path: 'root/sub1/sub2/word
probe :path
root/sub1/sub2/word

```

In the previous example, the **:path** notation was used to get the path itself, not the path's value:

```
probe path
a word at the end of the path

```

Looking at how long a path is:

```
probe length? :path
4

```

Finding a word within a path:

```
probe find :path 'sub2
sub2/word

```

Changing a word in a path:

```
change find :path 'word 'num
probe :path
root/sub1/sub2/num
probe path
55

```

#### 2.10.2 Format

Paths are expressed relative to a root word by providing a number of refinements, each separated by a forward slash (/). These refinements can be words or values. Their specific interpretation vary depending on the datatype of the root value.

The words supplied as refinements in paths are symbolic and are not evaluated. This is necessary to allow the most intuitive form for object referencing. To use a word's reference, an explicit word value reference is required:

```
root/:word

```

This example uses the value of the variable, rather than it name.

#### 2.10.3 Creation

You can **make** an empty path of a given size with:

```
path: make path! 10
insert :path `test
insert tail :path `this
print :path
test/this

```

The **to-path** function converts data to the **path!** datatype:

```
probe to-path [root sub]
root/sub
probe to-path "root sub"
root/sub

```

The **to-set-word** function converts other values to the **set-word** datatype.

```
probe to-set-path "root sub"
root/sub:

```

The **to-lit-word** function converts other values to the **lit-word** datatype.

```
probe to-lit-path "root sub"
'root/sub

```

#### 2.10.4 Related

Use **path?**, **set-path?**, and **lit-path?** to determine the datatype of a value.

```
probe path? second [1 two "3"]
false
blk: [sub1 [sub2 [word 1]]]
blk2: [blk/sub1/sub2/word: 2]
if set-path? (pick blk2 1) [print "it is set"]
it is set
probe lit-path? first ['root/sub]
true

```

As paths are a subset of the **series!** pseudotype, use **series?** to check this:

```
probe series? pick [root/sub] 1
true

```

Use **form** on a path value creates a string from the path:

```
probe form pick [root/sub] 1
root/sub

```

Use **mold** on a path value creates a string of the path value itself, thus allowing it to be reloaded as a REBOL path value:

```
probe mold pick [root/sub] 1
root/sub

```

### 2.11 String

#### 2.11.1 Concept

Strings are a series of characters. All operations performable on series values can be performed on strings.

#### 2.11.2 Format

String values are written as a sequence of characters surrounded by double quotes " " or braces {}. Strings enclosed in double quotes are restricted to a single line and must not contain unprintable characters.

```
"This is a short string of characters."

```

Strings enclosed in braces are used for larger sections of text that span multiple lines. All of the characters of the string, including spaces, tabs, quotes, and newlines are part of the string.

```
{This is a long string of text that will 
not easily fit on a single line of source.
These are often used for documentation
purposes.}

```

Braces are counted within the string, so a string can include other braces as long as the number of closing braces matches the number of opening braces.

```
{
This is another long string of text that would
never fit on a single line. This string also
includes braces { a few layers deep { and is 
valid because there are as many closing braces }
as there are open braces } in the string.
}

```

You can include special characters and operations in strings by prefixing them with a caret (^). Special characters include:

| Character | Definition                               |
| --------- | ---------------------------------------- |
| ^"        | Inserts a double quote (").              |
| ^}        | Inserts a closing brace (}).             |
| ^^        | Inserts a caret (^).                     |
| ^/        | Starts a new line.                       |
| ^(line)   | Starts a new line.                       |
| ^-        | Inserts a tab.                           |
| ^(tab)    | Inserts a tab.                           |
| ^(page)   | Starts a new page.                       |
| ^(back)   | Erases one character to the left of the insertion point. |
| ^(null)   | Inserts a null character.                |
| ^(escape) | Inserts an escape character.             |
| ^(letter) | Inserts control-letter (A-Z).            |
| ^(xx)     | Inserts an ASCII character by hexidecimal (xx) number. his format allows for expansion into unicode characters in the future. |

#### 2.11.3 Creation

Use **make** to create a pre-allocated amount of space for an empty string:

```
make string! 40'000 ; space for 40k characters

```

The **to-string** function converts data of other datatypes to a **string!** datatype:

```
probe to-string 29-2-2000
"29-Feb-2000"
probe to-string 123456.789
"123456.789"
probe to-string #888-555-2341
"888-555-2341"

```

Converting a block of data to a string with **to-string** has the effect of doing a **rejoin**, but without evaluating the block's contents:

```
probe to-string [123 456]
"123456"
probe to-string [225.225.225.0 none true 'word]
"225.225.225.0nonetrueword"

```

#### 2.11.4 Related

Use **string?** or **series?** to determine whether a value is an **string!** datatype:

```
print string? "123"
true
print series? "123"
true

```

The functions **form** and **mold** are closely related to strings, as they create strings from other datatypes. The **form**function makes a human readable version of a specified datatype, while **mold** makes a REBOL readable version.

```
probe form "111 222 333"
"111 222 333"
probe mold "111 222 333"
{"111 222 333"}

```

### 2.12 Tag

#### 2.12.1 Concept

Tags are used in HTML and other markup languages to indicate how text fields are to be treated. For example, the tag **<HTML>** at the beginning of a file indicates that it should be parsed by the rules of the Hypertext Markup Language. A tag with a forward slash (/), such as **</HTML>**, indicates the closing of the tag.

Tags are a subset of series, and thus can be manipulated as such:

```
a-tag: <img src="mypic.jpg">
probe a-tag
<img src="mypic.jpg">
append a-tag { alt="My Picture!"}
probe a-tag
<img src="mypic.jpg" alt="My Picture!">

```

#### 2.12.2 Format

Valid tags begin with an open angle bracket (<) and end with a closing bracket (>). For example:

```
<a href="index.html">
<img src="mypic.jpg" width="150" height="200">

```

#### 2.12.3 Creation

The **to-tag** function converts data to the **tag!** datatype:

```
probe to-tag "title"
<title>

```

Use **build-tag** to construct tags, including their attributes. The **build-tag** function takes one argument, a block. In this block, the first word is used as the tag name and the remaining words are processed as attribute value pairs:

```
probe build-tag [a href http://www.rebol.com/]
<a href="http://www.rebol.com/">
probe build-tag [
    img src %mypic.jpg width 150 alt "My Picture!"
]
<img src="mypic.jpg" width="150" alt="My Picture!">

```

#### 2.12.4 Related

Use **tag?** to determine whether a value is an **tag!** datatype.

```
probe tag? <a href="http://www.rebol.com/">
true

```

As tags are a subset of the series pseudotype, use **series?** to check this:

```
probe series? <a href="http://www.rebol.com/">
true

```

The **form** function returns a tag as a string:

```
probe form <a href="http://www.rebol.com/">
{<a href="http://www.rebol.com/">}

```

The **mold** function returns a tag as a string:

```
probe mold <a href="http://www.rebol.com/">
{<a href="http://www.rebol.com/">}

```

The **print** function prints a tag to standard output after doing a **reform** on it:

```
print <a href="http://www.rebol.com/">
<a href="http://www.rebol.com/">

```

### 2.13 URL

#### 2.13.1 Concept

URL is an acronym for Uniform Resource Locator, an Internet standard used to access resources such as web pages, images, files, and email across the network. The best known URL scheme is that used for web locations such as **http://www**.REBOL.com.

URL values are a subset of series, and thus can be manipulated as series:

```
url: http://www.rebol.com/reboldoc.html
probe to-file find/reverse (tail url) "rebol"
%reboldoc.html

```

#### 2.13.2 Format

The first part of a URL indicates its communications protocol, called a scheme. The language supports several schemes, including: web pages (**HTTP:**), file transfer (**FTP:**), newsgroups (**NNTP:**), email (**MAILTO:**), files (**FILE:**), finger (**FINGER:**), whois (**WHOIS:**), small network time (**DAYTIME:**), post office (**POP:**), transmission control (**TCP:**) and domain name service (**DNS:**). These scheme names are followed by characters that are dependent on which scheme being used.

```
http://host.dom/path/file
ftp://host.dom/path/file
nntp://news.some-isp.net/some.news.group
mailto:name@domain
file://host/path/file
finger://user@host.dom
whois://rebol@rs.internic.net
daytime://everest.cclabs.missouri.edu
pop://user:passwd@host.dom/
tcp://host.dom:21
dns://host.dom

```

Some fields are optional. For instance, the host can be followed by a port number if it differs from the default. An FTP URL supplies a default password if one is not specified:

```
ftp://user:password@host.dom/path/file

```

Characters in a URL must conform to Internet standards. Restricted characters must be encoded in hexadecimal by preceding them with the escape character %:

```
probe http://www.somesite.dom/odd%28dir%29/odd%7Bfile%7D.txt
http://www.somesite.dom/odd%28dir%29/odd%7Bfile%7D.txt
print http://www.somesite.dom/odd%28dir%29/odd%7Bfile%7D.txt
http://www.somesite.dom/odd(dir)/odd{file}.txt

```

#### 2.13.3 Creation

The **to-url** function converts blocks to the **url!** datatype, the first element in the block is the scheme, the second element is the domain (with or without **user:pass** and port) the remaining elements are the path and file:

```
probe to-url [http www.rebol.com reboldoc.html]
http://www.rebol.com/reboldoc.html
probe to-url [http www.rebol.com %examples "websend.r"]
http://www.rebol.com/examples/websend.r
probe to-url [http usr:pass@host.com:80 "(path)" %index.html]
http://usr:pass@host.com:80/%28path%29/index.html

```

#### 2.13.4 Related

The datatype word is **url!**.

Use **url?** to test the datatype.

```
probe url? ftp://ftp.rebol.com/
true

```

As urls are a subset of the series pseudotype, use **series?** to check this:

```
probe series? http://www.rebol.com/
true
&nbsp;

```

## 3. Other Values

### 3.1 Character

#### 3.1.1 Concept

Characters are not strings; they are the individual values from which strings are constructed. A character can be a printable, unprintable, or a control character.

#### 3.1.2 Format

A **char!** value is written as a number sign (#) followed by a string enclosed in double quotes. The number sign is necessary to distinguish a character from a string:

```
#"R"    ; the single character: R
"R"     ; a string with the character: R

```

Characters can include escape sequences that begin with a caret(^)and are followed by one or more characters of encoding. This encoding can include the characters **#"^A"** to **#"^Z"** for **control** **A** to **control** **Z** (upper and lower case are the same):

```
#"^A" #"^Z"

```

In addition, if parens are used within the character, they specify a special value. For example, null can be written as:

```
"^@"
"^(null)"
"^(00)"

```

Thes last line is written in hex format (base 16). The parens around the value allow for expansion into 16 bit unicode characters in the future.

Following is a table of control characters that can be used in REBOL.

| Character                  | Definition                |
| -------------------------- | ------------------------- |
| `#"(null)" or #"@"`        | null (zero)               |
| `#"(line)", #"/" or, #"."` | end of line               |
| `#"(tab)" or #"-"`         | horizontal tab            |
| `#"(page)"`                | new page (and page eject) |
| `#"(esc)"`                 | escape                    |
| `#"(back)"`                | backspace                 |
| `#"(del)"`                 | delete                    |
| `#"^"`                     | caret character           |
| `#"^""`                    | quotation mark            |
| `#"(00)" to #"(FF)"`       | hex forms of characters   |

#### 3.1.3 Creation

Characters can be converted to and from other datatypes with the **to-char** function:

```
probe to-char "a"
#"a"
probe to-char "z"
#"z"

```

Characters follow the ASCII standard and can be constructed by specifying a character's numeric equivalent:

```
probe to-char 65
#"A"
probe to-char 52
#"4"
probe to-char 52.3
#"4"

```

Another method of obtaining a character is to get the first character from a string:

```
probe first "ABC"
#"A"

```

While characters in strings are not case sensitive, comparison between individual characters is case sensitive:

```
probe "a" = "A"
true
probe #"a" = #"A"
false

```

However, when used in many types of functions, the comparison is not case sensitive unless you specify that option. Examples are:

```
select [#"A" 1] #"a"
1
select/case [#"A" 1] #"a"
none
find "abcde" #"B"
"bcde"
find/case "abcde" #"B"
none
switch #"A" [#"a" [print true]]
true

```

#### 3.1.4 Related

Use **char?** to determine whether a value is a **char!** datatype.

```
probe char? "a"
false
probe char? #"a"
true

```

Use the **form** function to print a character without the number sign:

```
probe form #"A"
"A"

```

Use **mold** on to print a character with the number sign and double quotes (and escape sequences for those characters that require it.):

```
probe mold #"A"
{#"A"}

```

### 3.2 Date

#### 3.2.1 Concept

Around the world, dates are written in a variety of formats. However, most countries use the **day-month-year**format. One of the few exceptions is the United States, which commonly uses a **month-day-year** format. For example, a date written numerically as 2/1/1999 is ambiguous. The month could be interpreted as either February or January. Some countries use a dash (-), some use a forward slash (/), and others use a period (.) as a separator. Finally, computer people often prefer dates in the year-month-day (ISO) format so they can be easily sorted.

#### 3.2.2 Format

The REBOL language is flexible, allowing **date!** datatypes to be expressed in a variety of formats. For example, the first day of March can be expressed in any of the following formats:

```
probe 1/3/1999
1-Mar-1999
probe 1+++1999
1-Mar-1999
probe 1999+++1  ;ISO format
1-Mar-1999

```

The year can span up to 9999 and down to 1. Leap days (February 29) can only be written for leap years:

```
probe 29-2-2000
29-Feb-2000

```

The fields of dates can be separated with forward slashes (/) or dashes (-). Dates can be written in either a year-month-day format or a day-month-year format:

```
probe 1999-10-5
5-Oct-1999
probe 1999/10/5
5-Oct-1999
probe 5-10-1999
5-Oct-1999
probe 5/10/1999
5-Oct-1999

```

Because the international date formats that are not widely used in the USA, a month name or month abbreviation can also be used:

```
probe 5/Oct/1999
5-Oct-1999
probe 5-October-1999
5-Oct-1999
probe 1999/oct/5
5-Oct-1999

```

When the year is the last field, it can be written as either a four digit or two digit number:

```
probe 5/oct/99
5-Oct-1999
probe 5/oct/1999
5-Oct-1999

```

However, it is preferred to write the year in full. Otherwise, problems occur with date comparison and sorting operations. While two digits can be used to express a year, the interpretation of a two-digit year is relative to the current year and is only valid for 50 years in the future or in the past:

```
probe 28-2-66   ; refers to 1966
28-Feb-1966
probe 12-Mar-20 ; refers to 2020
12-Mar-2020
probe 11+++45   ; refers to 2045, not 1945
11-Mar-2045

```

It is recommended to use a four-digit year to avoid potential problems.

To represent dates in the first century (which is rarely done because the Gregorian calendar did not exist), use leading zeros to represent the century (as in **9-4-0029**).

Dates can also include an optional time field and an optional time zone. The time is separated from the date with a forward slash (/). The time zone is appended using a plus (+) or minus (-), and no spaces are allowed. Time zones are written as a time shift (plus or minus) from GMT. The resolution of the time zone is to the half hour. If the time shift is an integer, it is assumed to be hours:

```
probe 4/Apr/2000/6:00+8:00
4-Apr-2000/6:00+8:00
probe 1999-10-2/2:00-4:00
2-Oct-1999/2:00-4:00
probe 1/1/1990/12:20:25-6
1-Jan-1990/12:20:25

```

There can be no spaces within the date. For example:

```
10 - 5 - 99

```

would be interpreted as a subtraction expression, not a date.

#### 3.2.3 Access

Refinements can be used with a date value to get any of its defined fields:

| Refinement   | Description                          |
| ------------ | ------------------------------------ |
| **/day**     | Gets the day.                        |
| **/month**   | Gets the month.                      |
| **/year**    | Gets the year.                       |
| **/julian**  | Gets the day of the year.            |
| **/weekday** | Gets the weekday (1-7/Mon-Sun).      |
| **/time**    | Gets the time (if present).          |
| **/hour**    | Gets the time's hour (if present)    |
| **/minute**  | Gets the time's minute (if present). |
| **/second**  | Gets the time's second (if present). |
| **/zone**    | Gets the time zone (if present).     |

Here's how these refinements work:

```
some-date: 29-Feb-2000
probe some-date/day
29
probe some-date/month
2
probe some-date/year
2000
days: ["Mon" "Tue" "Wed" "Thu" "Fri" "Sat" "Sun"]
probe pick days some-date/weekday
Tue

```

When a time is present, the time related refinements can be used. The **/hour**, **/minute** and **/second**refinements are used with the **/time** refinement that isolates the time segment of the date value for them to work on:

```
lost-time: 29-Feb-2000/11:33:22.14-8:00
probe lost-time/time
11:33:22.14
probe lost-time/time/hour
11
probe lost-time/time/minute
33
probe lost-time/time/second
22.14
probe lost-time/zone
-8:00

```

#### 3.2.4 Creation

Use the **to-date** function to convert values to a **date!:**

```
probe to-date "5-10-1999"
5-Oct-1999
probe to-date "5 10 1999 10:30"
5-Oct-1999/10:30
probe to-date [1999 10 5]
5-Oct-1999
probe to-date [5 10 1999 10:30 -8:00]
5-Oct-1999/10:30-8:00

```

[!Note When converting to a **date!**, the year must be specified as four digits.

Conversions can be applied to various math operations on dates:

```
probe 5-Oct-1999 + 1
6-Oct-1999
probe 5-10-1999 - 10
25-Sep-1999
probe 5-Oct-1999/23:00 + 5:00
6-Oct-1999/4:00

```

#### 3.2.5 Related

Use **date?** to determine whether a value is a **date!** datatype.

```
probe date? 5/1/1999
true

```

The related function **to-idate** returns a standard Internet date string. The Internet date format is day, date, month, year, time (24-hour clock), and time zone offset from GMT.

```
probe to-idate now
Fri, 30 Jun 2000 14:42:26 -0700

```

The **now** function returns the current date and time in full format including the time zone offset:

```
probe now
30-Jun-2000/14:42:26-7:00

```

### 3.3 Logic

#### 3.3.1 Concept

The **logic!** datatype consists of two states representing **true** and **false**. They are often returned from comparisons such as:

```
age: 100
probe age = 100
true
time: 10:31:00
probe time < 10:30
false
str: "this is a string"
probe (length? str) > 10
true

```

The logic! datatype is most commonly used as parameters to conditional functions such as **if**, **while**, and **until:**

```
if age = 100 [print "Centennial human"]
Centennial human
while [time > 6:30] [
    send person "Wake up!"
    wait [0:10]
]

```

The complement of a logic value is obtained from the **not** function:

```
there: place = "Ukiah" 
if not there [...]

```

#### 3.3.2 Format

Normally, logic values are retrieved from the evaluation of comparison expressions. However, words can be set to a logic value and used to turn the word **on** or **off:**

```
print-me: false
print either print-me ["turned on"]["turned off"]
turned off
print-me: true
print either print-me ["turned on"]["turned off"]
turned on

```

The **false** value is not equivalent to integer zero or **none**. However, in conditional expressions **false** and **none**have the same effect:

```
print-me: none
print either print-me ["turned on"]["turned off"]
turned off

```

Just about any value assigned to a word has the same effect as **true:**

```
print-me: "just a string"
print either print-me ["turned on"]["turned off"]
turned on
print-me: 11-11-1999
print either print-me ["turned on"]["turned off"]
turned on

```

The following words are predefined to hold logic values:

```
true
on     ;same as true
yes    ;same as true
false
off    ;same as false
no     ;same as false

```

So, instead of **true** and **false**, when it makes sense, the words **on** and **off**, or **yes** and **no** can be used instead:

```
print-me: yes
print either print-me ["turned on"]["turned off"]
turned on
print-me: no
print either print-me ["turned on"]["turned off"]
turned off
print-me: on
print either print-me ["turned on"]["turned off"]
turned on
print-me: off
print either print-me ["turned on"]["turned off"]
turned off

```

#### 3.3.3 Creation

The **to-logic** function converts **integer!** or **none!** values to the **logic!** datatype:

```
probe to-logic 0
false
probe to-logic 200
true
probe to-logic none
false
probe to-logic []
true
probe to-logic "a"
true
probe to-logic none
false

```

#### 3.3.4 Related

Use **logic?** to determine whether a value is a **logic!** datatype.

```
probe logic? 1
false
probe logic? on
true
probe logic? false
true

```

Use the functions **form**, **print**, and **mold** to print a logic value:

```
probe form true
true
probe mold false
false
print true
true

```

### 3.4 Money

#### 3.4.1 Concept

There is a wide variety of international symbols for monetary denominations. Some symbols are used before the amount and some after. As a standard for representing international monetary values, the REBOL language uses the United States monetary format, but allows the inclusion of specific denominations.

#### 3.4.2 Format

The **money!** datatype uses standard IEEE floating point numbers allowing up to 15 digits of precision including cents.

The language limits the length to 64 characters. Values that are out of range or cannot be represented in 64 characters are flagged as an error.

Monetary values are prefixed with an optional currency designator, followed by a dollar sign ($). A plus (+) or minus (-) can appear immediately before the first character (currency designator or dollar sign) to indicate sign.

```
$123
-$123
$123.45
US$12
US$12.34
-US$12.34
$12,34
-$12,34
DEM$12,34

```

To break long numbers into readable segments, a single quote (`) can be placed anywhere between two digits within the amount, but not before the amount.

```
probe $1'234.56
$1234.56
probe $1'234'567,89
$1234567.89

```

Do not use commas and periods to break up large amounts, as both these characters represent decimal points.

**The** money! datatype is a hybrid datatype. Conceptually money is scalar--an amount of money. However, because the currency designation is stored as a string, the **money!** datatype has two elements:

- string! - The currency designator string, which can have 3 characters maximum.
- decimal! - The money amount.

To demonstrate this, the following money is specified with the USD prefix:

```
my-money: USD$12345.67

```

Here are the two components:

```
probe first my-money
USD
probe second my-money
12345.67
probe pick my-money 3       ; only two components
none

```

If no currency designator is used, the currency designator string is empty:

```
my-money: $12345.67

probe first my-money
""
probe second my-money
12345.67

```

Various international currencies can be specified in the currency designator, such as:

```
my-money: DKM$12'345,67

probe first my-money
DKM
probe second my-money
12345.67

```

#### 3.4.3 Creation

Use the **to-money** function to convert money from a **string!**, **integer!**, **decimal!**, or **block!**.

```
probe to-money 123
$123.00
probe to-money "123"
$123.00
probe to-money 12.34
$12.34
probe to-money [DEM 12.34]
DEM$12.34
probe to-money [USA 12 34]
USA$12.34

```

Money can be added, subtracted, and compared with other money of the same currency. An error occurs if a different currency is used for such operations (automatic conversions are not currently supplied).

```
probe $100 + $10
$110.00
probe $100 - $50
$50.00
probe equal? DEM$100.11 DEM$100.11
true

```

Money can be multiplied and divided by integers and decimals. Money can also be divided by money, resulting in an integer or decimal.

```
probe $100 + 11
$111.00
probe $100 / 4
$25.00
probe $100 * 5
$500.00
probe $100 - 20.50
$79.50
probe 10 + $1.20
$11.20
probe 10 - $0.25
$9.75
probe $10 / .50
$20.00
probe 10 * $0.75
$7.50

```

#### 3.4.4 Related

Use **money?** to determine whether a value is an **money!** datatype.

```
probe money? USD$12.34
true

```

Use the **form**, **print**, and **mold** functions with a money argument to print a money value with the currency designator and dollar sign ($), as a decimal number with two digits of decimal precision.

```
probe form USD$12.34
USD$12.34
probe mold USD$12.34
USD$12.34
print USD$12.34
USD$12.34

```

### 3.5 None

#### 3.5.1 Concept

The **none!** datatype contains a single value that represents nothing or no value.

The concept of none is not the same as an empty block, empty string, or null character. It is an actual value that represents non-existence.

A **none!** value can be returned from various functions, primarily those involving series (for example, **pick** and **find**).

The REBOL word **none** is defined as a **none!** datatype and contains a **none!** value. The word **none** is not equivalent to **zero** or **false**. However, **none** is interpreted as **false** by many functions.

A **none!** value has many uses such as a return value from series functions like **pick**, **find** and **select:**

```
if (pick series 30) = none [...]

```

In databases, a **none** can be a placeholder for missing values:

```
email-database: [
    "Bobby" bob@rebol.com 40
    "Linda" none 23
    "Sara"  sara@rebol.net 33
]

```

It also can be used as a logic value:

```
secure none

```

#### 3.5.2 Format

The word **none** is predefined to hold a **none** value.

Although **none** is not equivalent to **zero** or **false**, it is valid within conditional expressions and has the same effect as **false:**

```
probe find "abcd" "e"
none
if find "abcd" "e" [print "found"]

```

#### 3.5.3 Creation

The **to-none** function always returns **none**.

#### 3.5.4 Related

Use **none?** to determine whether a value is a **none!** datatype.

```
print none? 1
false
print none? find [1 2 3] 4
true

```

The **form**, **print**, and **mold** functions print the value **none** when passed a **none** argument.

```
probe form none
none
probe mold none
none
print none
none

```

### 3.6 Pair

#### 3.6.1 Concept

A pair! datatype is used to indicate spatial coordinates, such as positions on a display. They are used for both positions and sizes. Pairs are used primarily in REBOL/View.

#### 3.6.2 Format

A pair is specified as integers separated by an **x** character.

```
100x50

1024x800

-50x200

```

#### 3.6.3 Creation

Use **to-pair** to convert block or string values into a pair datatype:

```
p: to-pair "640x480" 
probe p
640x480
p: to-pair [800 600] 
probe p
800x600

```

#### 3.6.4 Related

Use **pair?** to determine whether a value is a **pair!** datatype:

```
probe pair? 400x200
true
probe pair? pair
true

```

Pairs can be used with most integer math operators:

```
100x200 + 10x20

10x20 * 2x4

100x30 / 10x3

100x100 * 3

10x10 + 3

```

Pairs can be viewed by their individual coordinates:

```
pair: 640x480
probe first pair
640
probe second pair
480

```

All pair values support the **/x** and **/y** refinements. These refinements allow the viewing and manipulation of individual pair coordinates.

Viewing individual coordinates:

```
probe pair/x
640
probe pair/y
480

```

Modifying individual coordinates:

```
pair/x: 800
pair/y: 600
probe pair
800x600

```

### 3.7 Refinement

#### 3.7.1 Concept

Refinements are modifiers, similar to adjectives used in natural (human) languages. A refinement indicates a variation in the use of, or extension in the meaning of, a function, object, filename, URL, or path. Refinements are always symbolic in their value.

Refinements are used for functions:

```
block: [1 2]
append/only block [3 4]

```

objects:

```
print system/version

```

files:

```
dir: %docs/core
print read dir/file.txt

```

urls:

```
site: http://www.rebol.com
print read site/index.html

```

#### 3.7.2 Format

Refinements are composed with a slash followed by a valid REBOL word (see the words section below for definition). Examples are:

```
/only
/test1
/save-it

```

Refinements are usually joined to other words, such as in the case of:

```
port: open/binary file

```

But refinements can also be written alone, as is done when specifying refinements to a function:

```
save-data: function [file data /limit /reload] ...

```

#### 3.7.3 Creation

Refinements can be created literally in source code:

```
/test

```

or can be composed from the **to-refinement** word:

```
probe to-refinement "test"
/test

```

#### 3.7.4 Related

To test for a refinement, use the refinement? function:

```
probe refinement? /test
true
probe refinement? 'word
false

```

### 3.8 Time

#### 3.8.1 Concept

The REBOL language supports the standard expression of time in hours, minutes, seconds, and subseconds. Both positive and negative times are permitted.

The **time!** datatype uses relative rather than absolute time. For example, **10:30** is 10 hours and 30 minutes rather than the time of 10:30 A.M. or P.M.

#### 3.8.2 Format

Times are expressed as a set of integers separated by colons (:).. Hours and minutes are required, but seconds are optional. Within each field, leading zeros are ignored:

```
10:30
0:00
18:59
23:59:50
8:6:20
8:6:2

```

The minutes and seconds fields can contain values greater than 60. Values greater than 60 are automatically converted. For instance **0:120:00** is the same as **2:00**.

```
probe 00:120:00
2:00

```

Subseconds are specified using a decimal in the seconds field. Use either a period or a comma as the decimal point. The hours and minutes fields become optional when the decimal is present. Subseconds are encoded to the nano-second, or one billionth of a second:

```
probe 32:59:29.5
32:59:29.5
probe 1:10,25
0:01:10.25
probe 0:0.000000001
0:00:00.000000001
probe 0:325.2
0:05:25.2

```

Times can be followed by **AM** or **PM**, but no space is permitted. **PM** adds 12 hours to the time:

```
probe 10:20PM
22:20
probe 3:32:20AM
3:32:20

```

Times are output in a standard hours, minutes, seconds, and subseconds format, regardless of how they are entered:

```
probe 0:87363.21
24:16:03.21

```

#### 3.8.3 Access

Time values have three refinements that can be used to return specific information about the value:

| Refinement  | Description              |
| ----------- | ------------------------ |
| **/hour**   | Gets the value's hour.   |
| **/minute** | Gets the value's minute. |
| **/second** | Gets the value's second. |

Here's how to use a time value's refinements:

```
lapsed-time: 91:32:12.14
probe lapsed-time/hour
91
probe lapsed-time/minute
32
probe lapsed-time/second
12.14

```

Times with time zones can only be used with the **date!**.

#### 3.8.4 Creation

Times can be converted using the **to-time** function:

```
probe to-time "10:30"
10:30
probe to-time [10 30]
10:30
probe to-time [0 10 30]
0:10:30
probe to-time [10 30 20.5]
10:30:20.5

```

In the previous examples, the values are not evaluated. To evaluate values as mathematical expressions, use the reduce function:

```
probe to-time reduce [10 30 + 5]
10:35

```

In various math operations involving time values, the time values, integers, or decimals are converted as shown below:

```
probe 10:30 + 1
10:30:01
probe 10:00 - 10
9:59:50
probe 0:00 - 10
-0:00:10
probe 5:10 * 3
15:30
probe 0:0:0.000000001 * 1'500'600
0:00:00.0015006
probe 8:40:20 / 4
2:10:05
probe 8:40:20 / 2:20:05
3
probe 8:40:20 // 4:20
0:00:20

```

#### 3.8.5 Related

Use **time?** to determine whether a value is a **time!** datatype:

```
probe time? 10:30
true
probe time? 10.30
false

```

Use the **now** function with the **/time** refinement to return the current local date and time:

```
print now/time
14:42:15

```

Use the **wait** function to wait for a duration, port, or both.

If a value is a **time!** datatype, **wait** delays for that period of time. If a value is a **date!/time!**, **wait** waits until the indicated date and time. If the value is an **integer!** or **decimal!**, the function waits the indicated number of seconds. If the value is a **port**, the function will wait for an event from that port. If a block is specified, it will wait for any of the times or ports to occur. It returns the port that caused the wait to complete or returns **none** if the timeout occurred. For example,

```
probe now/time
14:42:16
wait 0:00:10
probe now/time
14:42:26

```

### 3.9 Tuple

#### 3.9.1 Concept

It is common to represent version numbers, Internet addresses, and RGB color values as a sequence of three or four integers. These types of numbers are called a **tuple!** (as in quintuple) and are represented as a set of integers separated by periods.

```
1.3.0 2.1.120 1.0.2.32     ; version
199.4.80.250 255.255.255.0 ; net addresses/masks
0.80.255 200.200.60        ; RGB colors

```

#### 3.9.2 Format

Each integer field of a **tuple!** datatype can range between 0 and 255. Negative integers produce an error.

Three to ten integers can be specified in a tuple. In the case where only two integers are given, there must be at least two periods, otherwise the value is treated as a decimal.

```
probe 1.2     ; is decimal
1.2
probe type? 1.2
decimal!
probe 1.2.3   ; is tuple
1.2.3
probe 1.2.    ; is tuple
1.2.0
probe type? 1.2.
tuple!

```

#### 3.9.3 Creation

Use the **to-tuple** function to convert data to the **tuple!** datatype:

```
probe to-tuple "12.34.56"
12.34.56
probe to-tuple [12 34 56]
12.34.56

```

#### 3.9.4 Related

Use **tuple?** to determine whether a value is a **tuple!** datatype.

```
probe tuple? 1.2.3.4
true

```

Use the **form** function to print a tuple as a string:

```
probe form 1.2.3.4
1.2.3.4

```

Use the **mold** function to convert a tuple into a string that can be read back into REBOL as a tuple:

```
probe mold 1.2.3.4
1.2.3.4

```

Use the **print** function to print a tuple to standard output after using the **reform** function:

```
print 1.2.3.4
1.2.3.4

```

### 3.10 Words

#### 3.10.1 Concept

Words are the symbols used by REBOL. A word may or may not be a variable, depending on how it is used. Words are often used directly as symbols.

REBOL has no keywords, there are no restrictions on what words are used or how they are used. For instance, you can define your own function called **print** and use it instead of the predefined function for printing values.

There are four different formats for using words, depending on the operation required.

| Action    | Type Word     | Type Test     | Conversion      |
| --------- | ------------- | ------------- | --------------- |
| **word:** | **set-word!** | **set-word?** | **to-set-word** |
| **:word** | **get-word!** | **get-word?** | **to-get-word** |
| **word**  | **word!**     | **word?**     | **to-word**     |
| **'word** | **lit-word!** | **lit-word?** | **to-lit-word** |

#### 3.10.2 Format

Words are composed of alphabetic characters, numbers, and any of the following characters:

```
? ! . ' + - * & | = _ &#126;

```

A word cannot begin with a number, and there are also some restrictions on words that could be interpreted as numbers. For instance, -1 and +1 are numbers, not words.

The end of a word is marked by a space, a newline, or one of the following characters:

```
[ ] ( ) { } " : ; /

```

Thus, the square brackets of a block are not part of a word:

```
[test]

```

The following characters are not allowed in words:

```
@ # $ % ^ ,

```

Words can be of any length, but cannot extend past the end of a line.

```
this-is-a-very-long-word-used-as-an-example

```

Sample words are:

```
Copy print test

number?  time?  date!

image-files  l'image

++ -- == +-

***** *new-line*

left&right left|right

```

The REBOL language is not case-sensitive. The words following words:

```
blue

Blue

BLUE

```

all refer to the same word. The case of the word is preserved when it is printed.

Words can be reused. The meaning of a word is dependent on its context, so words can be reused in different contexts. You can reuse any word, even predefined REBOL words. For instance, the REBOL word **if** can be used in your code differently than how it is used by the REBOL interpreter.

#### 3.10.3 Creation

The **to-word** function converts values to the **word!** datatype.

```
probe to-word "test"
test

```

The **to-set-word** function converts values to the **set-word!** datatype.

```
probe make set-word! "test"
test:

```

The **to-get-word** function converts values to the **get-word!** datatype.

```
probe to-get-word "test"
:test

```

The **to-lit-word** function converts values to the **lit-word!** datatype.

```
probe to-lit-word "test"
'test

```

#### 3.10.4 Related

Use **word?**, **set-word?**, **get-word?**, and **lit-word?** to test the datatype.

```
probe word? second [1 two "3"]
true
if set-word? first [word: 10] [print "it is set"]
it is set
probe get-word? second [pr: :print]
true
probe lit-word? first ['foo bar]
true
```