# Expressions

## Contents:

- [1. Overview](#section-1)
- [2. Blocks](#section-2)
- [3. Values](#section-3)
  - [3.1 Direct and Indirect Values](#section-3.1)
  - [3.2 Datatypes of Values](#section-3.2)
- [4. Evaluating Expressions](#section-4)
  - [4.1 Evaluating Console Input](#section-4.1)
  - [4.2 Evaluating Simple Values](#section-4.2)
  - [4.3 Evaluating Blocks](#section-4.3)
  - [4.4 Reducing Blocks](#section-4.4)
  - [4.5 Evaluating Scripts](#section-4.5)
  - [4.6 Evaluating Strings](#section-4.6)
  - [4.7 Evaluation Errors](#section-4.7)
- [5. Words](#section-5)
  - [5.1 Word Names](#section-5.1)
  - [5.2 Word Usage](#section-5.2)
  - [5.3 Setting Words](#section-5.3)
  - [5.4 Getting Words](#section-5.4)
  - [5.5 Literal Words](#section-5.5)
  - [5.6 Unset Words](#section-5.6)
  - [5.7 Protecting Words](#section-5.7)
- [6. Conditional Evaluation](#section-6)
  - [6.1 Conditional Blocks](#section-6.1)
  - [6.2 Any and All](#section-6.2)
  - [6.3 Conditional Loops](#section-6.3)
  - [6.4 Common Mistakes](#section-6.4)
- [7. Repeated Evaluation](#section-7)
  - [7.1 Loop](#section-7.1)
  - [7.2 Repeat](#section-7.2)
  - [7.3 For](#section-7.3)
  - [7.4 Foreach](#section-7.4)
  - [7.5 Forall and Forskip](#section-7.5)
  - [7.6 Forever](#section-7.6)
  - [7.7 Break](#section-7.7)
- [8. Selective Evaluation](#section-8)
  - [8.1 Select](#section-8.1)
  - [8.2 Switch](#section-8.2)
- [9. Stopping Evaluation](#section-9)
- [10. Trying Blocks](#section-10)

## 1. Overview

The foremost goal of REBOL is to establish a standard method of communication that spans all computer systems. REBOL provides a simple, direct means of expressing any kind of information with optimal flexibility and minimal syntax. For example, examine the following line:

```
Sell 100 shares of "Acme" at $47.97 per share

```

The line looks a lot like English making it easy to compose if you are sending it and easy to understand if you are receiving it. However, this line is actually a valid expression in REBOL, so your computer could also understand and act on it. (Note that the line is a "dialect" of REBOL. It can be in-directly evaluated. More on this concept below.)

REBOL provides a common language between you and your computer. In addition, if your computer sends this expression to your stock broker's computer, which is also running REBOL, your stock broker's computer can understand the expression and act on it. So, REBOL provides a common language between computers. And, the line could be sent to millions of other computer systems that could also act on it.

The following line is another example of a REBOL expression:

```
Reschedule exam for 2-January-1999 at 10:30

```

The expression shown in the above example (written in another dialect) may have come from your doctor typing it, or perhaps it originated from an application that was run by your doctor. It does not matter. What is important is that the expression can be acted upon regardless of the type of computer, hand-held device, kiosk, or television console you are using.

The data values (numbers, strings, prices, dates, and times) in all of the expressions shown in the previous examples are standardized valid REBOL formats. The words, however, depend on a specific context of interpretation to convey their meaning. Words such as `sell`, `at`, and `read` have different meanings in different contexts. The words are relative expressions -- their meaning is context dependent.

Expressions can be processed in one of two ways: **directly** by the REBOL interpreter, or **indirectly** by a REBOL script. An expression processed indirectly is called a **dialect**. The previous examples are dialects, so they are processed by a script. The following example is not a dialect and is processed directly by the REBOL interpreter:

```
send master@rebol.com read http://www.rebol.com

```

In this example the words **send** and **read** are functions that are processed by the REBOL interpreter.

The distinction REBOL makes is that **information is either directly or indirectly interpreted**. The distinction is not whether information is code or data, but how it is processed. In REBOL code is often handled as data and data is frequently processed as code, so the traditional division between code and data blurs. How information is processed determines whether it is code or data.

## 2. Blocks

REBOL Expressions are based on this concept: you combine **values** and **words** into **blocks**.

In scripts, a block is normally enclosed with square brackets [ ]. Everything within the square brackets is part of the block. The block contents can span any number of lines, and its format is completely freeform. The following examples show various ways of formatting block content:

```
[white red green blue yellow orange black]

["Spielberg" "Back to the Future" 1:56:20 MCA]

[
    "Bill"  billg@ms.dom  #315-555-1234
    "Steve" jobs@apl.dom  #408-555-4321
    "Ted"   ted@gw2.dom   #213-555-1010
]

sites: [
    http://www.rebol.com [save %reb.html data]
    http://www.cnn.com   [print data]
    ftp://www.amiga.com  [send cs@org.foo data]
]

```

Some blocks do not require square brackets, because they are implied. For example, in a REBOL script, there are no brackets around the entire script, however, the script content is a block. The square brackets of an **outer-block**of the script are implied. The same is true for expressions typed at the command prompt or for REBOL messages sent between computers--each is an implied block.

Another important aspect of blocks is that they imply additional information. Blocks **group** a set of values in a particular **order**. That is, a block can be used as a data set as well as a sequence. This will be described in more detail in the [Series Chapter](rebolcore-6.html#_Toc487519750).

## 3. Values

REBOL provides a built-in set of **values** that can be expressed and exchanged between all systems. Values are the primary elements for composing all REBOL expressions.

### 3.1 Direct and Indirect Values

Values can be **directly** or **indirectly** expressed.

A directly expressed value is **known** as it is lexically, or literally, written. For instance, the number 10 or the time 10:30 are directly expressed values.

An indirectly expressed value is **unknown** until it is evaluated. The values `none`, `true`, and `false` all require words to represent them. These values are indirectly expressed because they must be evaluated for their values to be known. This is also true of other values, such as lists, hashes, functions, objects.

### 3.2 Datatypes of Values

Every REBOL value is of a particular **datatype**. The datatype of a value defines:

1. The range of possible values for the datatype. For example, the logic datatype can only be true or false.
2. The operations that can be performed. For example, you can add two integers, but you cannot add two logical values.
3. The way in which the values are stored in memory. Some datatypes can be stored directly (such as numbers), while others are stored indirectly (such as strings).

By convention, REBOL datatype words are followed by an exclamation point (!) to help make them stand out. For example:

```
integer!
char!
word!
string!

```

**Datatype Words are Just Words**

The words used for datatypes are just like any other words in REBOL. There is nothing magic about the ! used to represent them.

See the [Values Appendix](rebolcore-16.html#_Toc487519750) for a description of all the REBOL datatypes.

## 4. Evaluating Expressions

To **evaluate** an expression is to compute its value. REBOL operates by evaluating the series of expressions constituting a script and then returning the result. Evaluating is also called running, processing, or executing a script.

Evaluation is performed on blocks. Blocks can be typed at the console or loaded from a script file. Either way, the process of evaluation is the same.

### 4.1 Evaluating Console Input

Any expression that can be evaluated in a script, can also be evaluated from the REBOL prompt, providing a simple means of testing individual expressions in a script.

For example, if you type the following expression at the console prompt:

```
>> 1 + 2

```

the expression is evaluated and the following result is returned:

```
== 3

```

**About The Code Examples...**

In the example above, the console prompt (>>) and result indicator (==) are shown to give you an idea of how they appear in the console. For the examples that follow, the prompt and result strings are not shown. However, you can assume that these examples can be typed into the console to verify their results.

### 4.2 Evaluating Simple Values

Since the value of directly expressed values is known, they simply return their values. For example, if you type the following line:

```
10:30

```

the value 10:30 is returned. This is the behavior of all directly expressed values. It includes:

```
integer    1234
decimal    12.34
string     "REBOL world!"
time       13:47:02
date       30-June-1957
tuple      199.4.80.1
money      $12.49
pair       100x200
char       #"A"
binary     #{ab82408b}
email      info@rebol.com
issue      #707-467-8000
tag        <IMG SRC="xray.jpg">
file       %xray.jpg
url        http://www.rebol.com/
block      [milk bread butter]

```

### 4.3 Evaluating Blocks

Normally, blocks are **not** evaluated. For example, typing the following block:

```
[1 + 2]

```

returns the same block:

```
[1 + 2]

```

The block is not evaluated; it is simply treated as data.

To evaluate a block, use the **do** function, as shown in the following example:

```
do [1 + 2]
3

```

The **do** function returns the result of the evaluation. In the previous example, the number 3 is returned.

If a block contains multiple expressions, only the result of the last expression is returned:

```
do [
    1 + 2
    3 + 4
]
7

```

In this example, both expressions are evaluated, but only the result of the 3 + 4 expression is returned.

There are a number of functions such as **if**, **loop**, **while**, and **foreach** that evaluate a block as part of their function. These functions are discussed in detail later in this chapter, but here are a few examples:

```
if time > 12:30 [print "past noon"]
past noon
loop 4 [print "looping"]
looping
looping
looping
looping

```

This is important to remember: blocks are treated as data until they are explicitly evaluated by a function. Only a function can cause them to be evaluated.

### 4.4 Reducing Blocks

When you evaluate a block with **do**, only the value of its last expression is returned as a result. However, there are times when you want the values of all the expressions in a block to be returned. To return the results of all of the expressions in a block, use the **reduce** function. In the following example, **reduce** is used to return the results of both expressions in the block:

```
reduce [
    1 + 2
    3 + 4
]
[3 7]

```

In the above example, the block was **reduced** to its evaluation results. The **reduce** function returns results in a block.

The **reduce** function is important because it enables you to create blocks of expressions that are evaluated and passed to other functions. **Reduce** evaluates each expression in a block and puts the result of that expression into a new block. That new block is returned as the result of **reduce**.

Some functions, like **print**, use **reduce** as part of their operation, as shown in the following example:

```
print [1 + 2  3 + 4]
3 7

```

The **rejoin**, **reform**, and **remold** functions also use **reduce** as part of their operation, as shown in the following examples:

```
print rejoin [1 + 2  3 + 4]
37
print reform [1 + 2  3 + 4]
3 7
print remold [1 + 2  3 + 4]
[3 7]

```

The **rejoin**, **reform**, and **remold** functions are based on the **join**, **form**, and **mold** functions, but reduce their blocks first.

### 4.5 Evaluating Scripts

The **do** function can be used to evaluate entire scripts. Normally, **do** evaluates a block, as shown in the following example:

```
do [print "Hello!"]
Hello!

```

But, when **do** evaluates a file name instead of a block, the file will be loaded into the interpreter as a block, then evaluated as shown in the following example:

```
do %script.r

```

**A REBOL Header is Required**

For a script file to be evaluated, it must include a valid REBOL header, which is described in the [Scripts Chapter](rebolcore-5.html#_Toc487519750). The header identifies that the file contains a script and not just random text.

### 4.6 Evaluating Strings

The **do** function can be used to evaluate expressions that are found within text strings. For example, the following expression:

```
do "1 + 2"
3

```

returns the result `3`. First the string is converted to a block, then the block is evaluated.

Evaluating strings can be handy at times, but it should be done only when necessary. For example, to create a REBOL console line processor, type the following expression:

```
forever [probe do ask "=> "]

```

The above expression would prompt you with `=>` and wait for you to type a line of text. The text would then be evaluated, and its result would be printed. (Of course, it's not really quite this simple, because the script could have produced an error.)

Unless it is necessary, evaluating strings is not generally a good practice. Evaluating strings is less efficient than evaluating blocks, and the context of words in a string is not known. For example, the following expression:

```
do form ["1" "+" "2"]

```

is much less efficient than typing:

```
do [1 + 2]

```

REBOL blocks can be constructed just as easily as strings, and blocks are better for expressions that need to be evaluated.

### 4.7 Evaluation Errors

Errors may occur for many different reasons during evaluation. For example, if you divide a number by zero, evaluation is stopped and an error is displayed

```
100 / 0
** Math Error: Attempt to divide by zero.
** Where: 100 / 0

```

A common error is using a word before it has been defined:

```
size + 10
** Script Error: size has no value.
** Where: size + 10

```

Another common error is not providing the proper values to a function in an expression:

```
10 + [size]
** Script Error: Cannot use add on block! value.
** Where: 10 + [size]

```

Sometimes errors are not so obvious, and you will need to experiment to determine what is causing the error.

## 5. Words

Expressions are built from values and words. Words are used to represent meaning. A word can represent an idea or it can represent a specific value.

In the previous examples in this chapter, a number of words were used within expressions without explanation. For instance, the **do**, **reduce**, and **try** words are used, but not explained.

Words are evaluated somewhat differently than directly expressed values. When a word is evaluated, its value is looked up, evaluated, and returned as a result. For example, if you type the following word:

```
zero
0

```

the value `0` is returned. The word **zero** is predefined to be the number zero. When the word is looked up, a zero is found and is returned.

When words like **do** and **print** are looked up, their values are found to be functions, rather than simple values. In such cases, the function is evaluated, and the result of the function is returned.

### 5.1 Word Names

Words are composed of alphabetic characters, numbers, and any of the following characters:

```
? ! . ' + - * & | = _ ~

```

A word cannot begin with a number, and there are also some restrictions on words that could be interpreted as numbers. For example, -1 and +1 are numbers, not words.

The end of a word is marked by a space, a new line, or one of the following characters:

```
[ ] ( ) { } " : ; /

```

Thus, the brackets of a block are not part of a word. For example, the following block contains the word `test` :

```
[test]

```

The following characters are not allowed in words as they cause words to be misinterpreted or to generate an error:

```
@ # $ % ^ ,

```

Words can be of any length, but words cannot extend past the end of a line:

```
this-is-a-very-long-word-used-as-an-example

```

The following lines provide examples of valid words:

```
Copy print test
number?  time?  date!
image-files  l'image
++ -- == +-
***** *new-line*
left&right left|right

```

REBOL is not case sensitive. The following words all refer to the same word:

```
blue
Blue
BLUE

```

The case of a word is preserved when it is printed.

Words can be reused. The meaning of a word is dependent on its context, so words can be reused in different contexts. There are no keywords in REBOL. You can reuse any word, even those that are predefined in REBOL. For instance, you can use the word **if** in your code differently than the REBOL interpreter uses this word.

**Pick Good Words**

Pick the words you use carefully. Words are used to associate meaning. If you pick your words well, it will be easier for you and others to understand your scripts.

### 5.2 Word Usage

Words are used in two ways: as **symbols** or as **variables**. In the following block, words are used as symbols for colors.

```
[red green blue]

```

In the following line:

```
print second [red green blue]
green

```

the words have no meaning other than their use as names for colors. All words used within blocks serve as symbols until they are evaluated.

When a word is evaluated, it is used as a variable. In the previous example, the words **print** and **second** are variables that hold native functions which perform the required processing.

A word can be written in four ways to indicate how it is to be treated, as shown in [Word Formats](rebolcore-4.html#22570).

| Format  | What It Does                             |
| ------- | ---------------------------------------- |
| `word`  | Evaluates the word. This is the most natural and common way to write words. If the word holds a function, it will be evaluated. Otherwise, the value of the word will be returned. |
| `word:` | Defines or sets the value of a word. It is given a new value. The value can be anything, including a function. See [Setting Words](rebolcore-4.html#_Toc487519727) below. |
| `:word` | Gets the word's value, but doesn't evaluate it. This is useful for referring to functions and other data without evaluating them. See [Getting Words](rebolcore-4.html#_Toc487519728) below. |
| `'word` | Treats the word as a symbol, but does not evaluate it. The word itself is the value. |

### 5.3 Setting Words

A word followed by a colon (:) is used to define or set its value:

```
age: 42
lunch-time: 12:32
birthday: 20-March-1990
town: "Dodge City"
test: %stuff.r

```

You can set a word to be any type of value. In the previous examples, words are defined to be integer, time, date, string, and file values. You can also set words to be more complex types of values. For example, the following words are set to block and function values:

```
towns: ["Ukiah" "Willits" "Mendocino"]
code: [if age > 32 [print town]]
say: func [item] [print item]

```

**Why Words Are Set This Way**

In many langages words are set with an equal sign, such as:

```
age = 42

```

In REBOL words are set with a colon. The reason for this is important. It makes the set operation on words into a single lexical value. The representation for the set operation is **atomic**.

The difference between the two approaches can be seen in this example.

```
print length? [age: 42]
2
print length? [age = 42]
3

```

REBOL is a **reflective** language, it is able to manipulate its own code. This method of setting values allows you to write code that easily manipulates **set-word** operations as a single unit.

Of couse, the other reason is that the equal sign (=) is used as a comparision operator.

Multiple words can be set at one time by cascading the word definitions. For example, each of the following words are set to `42:`

```
age: number: size: 42

```

Words can also be set with the **set** function:

```
set 'time 10:30

```

In this example, the line sets the word `time` to 10:30. The word `time` is written as a literal (using a single quote) so that it will not be evaluated.

The **set** function can also set multiple words:

```
set [number num ten] 10

print [number num ten]
10 10 10

```

In the above example, notice that the words do not need to be quoted because they are within a block, which is not evaluated. The **print** function shows that each word is set to the integer `10`.

If **set** is provided a block of values, each of the individual values are set to the words. In this example, one, two, and three are set to 1, 2, and 3:

```
set [one two three] [1 2 3]

print three
3
print [one two three]
1 2 3

```

See the [Words Section](rebolcore-16.html#_Toc487520074) in the [Values Appendix](rebolcore-16.html#_Toc487519750) for more about setting words.

### 5.4 Getting Words

To get the value of a word that was previously defined, place a colon (:) at the front of the word. A word prefixed with a colon obtains the value of the word, but does not evaluate it further if it is a function. For example, the following line:

```
drucken: :print

```

defines a new word, `drucken` (which is German for print), to refer to the same function **print** does. This is possible because **:print** returns the function for **print**, but does not evaluate it.

Now, `drucken` performs the same function as **print** :

```
drucken "test"
test

```

Both **print** and `drucken` are set to the same value, which is the function that does printing.

This can also be accomplished with the **get** function. When given a literal word, **get** returns its value, but does not evaluate it:

```
stampa: get 'print

stampa "test"
test

```

The ability to get the value of a word is also important if you want to determine what the value is without evaluating it. For example, you can determine if a word is a native function using the following line:

```
print native? :if
true

```

Here the get returns the function for **if**. The **if** function is not evaluated, but rather it is passed to the **native?**function which checks if it is a native datatype. Without the colon, the **if** function would be evaluated, and, because it has no arguments, an error would occur.

### 5.5 Literal Words

The ability to deal with a word as a literal is useful. Both **set** and **get**, as well as other functions like **value?**, **unset**, **protect**, and **unprotect**, expect a literal value.

Literal words can be written in one of two ways: by prefixing the word with a single quotation mark, also known as a tick, (`) or by placing the word in a block.

You can use a tick in front of a word that is evaluated:

```
word: 'this

```

In the above example, the `word` variable is set to the literal word `this`, not to the value of `this`. The `word`variable just uses the name symbolically. The example below shows that if you print the value of the word, you will see the this word:

```
print word
this

```

You can also obtain literal words from an unevaluated block. In the following example, the **first** function fetches the first word from the block. This word is then set to the word variable.

```
word: first [this and that]

```

Any word can be used as a literal. It may or may not refer to a value. For example, in the example below the word `here` has no value. The word **print** does have a value, but it can still be used as a literal because literal words are not evaluated.

```
word: 'here
print word
here
word: 'print
print word
print

```

The next example illustrates the importance of literal values:

```
video: [
    title "Independence Day"
    length 2:25:24
    date   4/july/1996
]
print select video 'title
Independence Day

```

In this example, the word `title` is searched for in a block. If the tick was missing from `title`, then its natural value would be used. If `title` has no natural value, an error is displayed.

See the [Words Section](rebolcore-16.html#_Toc487520074) in the [Values Appendix](rebolcore-16.html#_Toc487519750) for more information about word literals.

### 5.6 Unset Words

A word that has no value is `unset`. If an unset word is evaluated, an error will occur:

```
>> outlook
** Script Error: outlook has no value.
** Where: outlook

```

The error message in the previous example indicates that the word has not been set to a value. The word is unset. Do not confuse this with a word that has been set to `none`, which is a valid value.

A previously defined word can be unset at any time using **unset** :

```
unset 'word

```

When a word is unset, its value is lost.

To determine if a word has been set, use the **value?** function, which takes a literal word as its argument:

```
if not value? 'word [print "word is not set"]
word is not set

```

Determining whether a word is set can be useful in scripts that call other scripts. For instance, a script may set a default parameter that was not previously set:

```
if not value? 'test-mode [test-mode: on]

```

### 5.7 Protecting Words

You can prevent a word from being set with the **protect** function:

```
protect 'word

```

An attempt to redefine a protected word causes an error:

```
word: "here"
** Script Error: Word word is protected, cannot modify.
** Where: word: "here"

```

A word can be unprotected as well using **unprotect** :

```
unprotect 'word
word: "here"

```

The **protect** and **unprotect** functions also accept a block of words:

```
protect [this that other]

```

Important function and system words can be protected using the **protect-system** function. Protecting function and system words is especially useful for beginners who might accidentally set important words. If **protect-system** is placed in your `user`.r file, then all predefined words are protected.

## 6. Conditional Evaluation

As previously mentioned, blocks are not normally evaluated. A **do** function is required to force a block to be evaluated. There are times when you may need to conditionally evaluate a block. The following section describes several ways to do this.

### 6.1 Conditional Blocks

The **if** function takes two arguments. The first argument is a condition and the second argument is a block. If the condition is `true` , the block is evaluated, otherwise it is not evaluated.

```
if now/time > 12:00 [print "past noon"]
past noon

```

The condition is normally an expression that evaluates to `true` or `false` ; however, other values can also be supplied. Only a `false` or a `none` value prevents the block from being evaluated. All other values (including zero) are treated as `true`, and cause the block to be evaluated. This can be useful for checking the results of **find**, **select**, **next**, and other functions that return `none` :

```
string: "let's talk about REBOL"
if find string "talk" [print "found"]
found

```

The **either** function extends **if** to include a third argument, which is the block to evaluate if the condition is false:

```
either now/time > 12:00 [
    print "after lunch"
][
    print "before lunch"
]
after lunch

```

The **either** function also interprets a `none` value as `false`.

Both the **if** and **either** functions return the result of evaluating their blocks. In the case of an **if**, the block value is only returned if the block is evaluated; otherwise, a `none` is returned. The **if** function is useful for conditional initialization of variables:

```
flag: if time > 13:00 ["lunch eaten"]

print flag
lunch eaten

```

Making use of the result of the **either** function, the previous example could be rewritten as follows:

```
print either now/time > 12:00 [
    "after lunch"
][
    "before lunch"
]
after lunch

```

Since both **if** and **either** are functions, their block arguments can be any expression that results in a block when evaluated. In the following examples, words are used to represent the block argument for **if** and **either**.

```
notice: [print "Wake up!"]
if now/time > 7:00 notice
Wake up!
notices: [
    [print "It's past sunrise!"]
    [print "It's past noon!"]
    [print "It's past sunset!"]
]
if now/time > 12:00 second notices
It's past noon!
sleep: [print "Keep sleeping"]
either now/time > 7:00 notice sleep
Wake up!

```

The conditional expressions used for the first argument of both **if** and **either** can be composed from a wide variety of comparison and logic functions. Refer to the [Math Chapter](rebolcore-11.html#_Toc487519750) for more information.

**Avoid This Common Mistake**

The most commonly made mistake in REBOL is to forget the second block on **either** or add a second block to **if**. These examples both creator hard-to-find errors:

```
either age > 10 [print "Older"]

if age > 10 [print "Older"] [print "Younger"]

```

These types of errors may be difficult to detect, so keep this in mind if these functions do not seem to be doing what you expect.

### 6.2 Any and All

The **any** and **all** functions offer a shortcut to evaluating some types of conditional expressions. These functions can be used in a number of ways:either in conjunction with **if**, **either**, and other conditional functions, or separately.

Both **any** and **all** accept a block of expressions, which is evaluated one expression at a time. The **any** function returns on the first true expression, and the **all** function returns on the first false expression. Keep in mind that a false expression can also be `none`, and that a true expression is any value other than `false` **or** `none`.

The **any** function returns the first value that is not `false`, otherwise it returns `none`. The **all** function returns the last value if all the expressions are not `false`, otherwise it returns**** `none`.

Both the **any** and **all** functions only evaluate as much as they need. For example, once **any** has found a true expression, none of the remaining expressions are evaluated. Here is an example of using **any** :

```
size: 50
if any [size < 10 size > 90] [
    print "Size is out of range."
]

```

The behavior of **any** is also useful for setting default values. For example, the following lines set a number to `100`, but only when its value is `none` :

```
number: none
print number: any [number 100]
100

```

Similarly, if you have various potential values, you can use the first one that actually has a value (is not `none` ):

```
num1: num2: none
num3: 80
print number: any [num1 num2 num3]
80

```

You can use **any** with functions like **find** to always return a valid result:

```
data: [123 456 789]
print any [find data 432 999]
999

```

Similarly, **all** can be used for conditions that require all expressions to be `true` :

```
if all [size > 10 size < 90] [print "Size is in range"]
Size is in range

```

You can verify that values have been set up before evaluating a function:

```
a: "REBOL/"
b: none
probe all [string? a string? b append a b]
none
b: "Core"
probe all [string? a string? b append a b]
REBOL/Core

```

### 6.3 Conditional Loops

The **until** and **while** functions repeat the evaluation of a block until a condition is met.

The **until** function repeats a block until the evaluation of the block returns `true` (that is, not `false` or `none` ). The evaluation block is always evaluated at least once. The **until** function returns the value of its block.

The example below will print each word in the color block. The block begins by printing the first word of the block. It then moves to the next color for each color in the block. The **tail?** function checks for the end of the block, and will return `true`, which will cause the **until** function to exit.

```
color: [red green blue]
until [
    print first color
    tail? color: next color
]
red
green
blue

```

The **break** function can be used to escape from the **until** loop at any time.

The **while** function repeats the evaluation of its two block arguments while the first block returns `true`. The first block is the condition block, the second block is the evaluation block. When the condition block returns `false` or `none`, the expression block will no longer be evaluated and the loop terminates.

Here is a similar example to that show above. The **while** loop will continue to print a color while there are still colors to print.

```
color: [red green blue]
while [not tail? color] [
    print first color
    color: next color
]
red
green
blue

```

The condition block can contain any number of expressions, so long as the last expression returns the condition. To illustrate this, the next example adds a print to the condition block. This will print the index value of the color. It will then check for the tail of the color block, which is the condition used for the loop.

```
color: [red green blue]
while [
    print index? color
    not tail? color
][
    print first color
    color: next color
]
1
red
2
green
3
blue
4

```

The last value of the block is returned from the **while** function.

A **break** can be used to escape from the loop at any time.

### 6.4 Common Mistakes

Conditional expressions are only false when they return `false` or `none`, and they are `true` when they return any other value. All of the conditional expressions in the following examples return `true`, even the zero and empty block values:

```
if true [print "yep"]
yep
if 1 [print "yep"]
yep
if 0 [print "yep"]
yep
if [] [print "yep"]
yep

```

The following conditional expressions return `false` :

```
if false [print "yep"]

if none [print "yep"]

```

Do not enclose conditional expressions in a block. Conditional expressions enclosed in blocks, always return a `true` result:

```
if [false] [print "yep"]
yep

```

Do not confuse **either** with **if**. For example, if you intend to write:

```
either some-condition [a: 1] [b: 2]

```

but write this instead:

```
if some-condition [a: 1] [b: 2]

```

the **if** function would ignore the second block. This would not cause an error, but the second block would never get evaluated.

The opposite is also true. If you write the following line, omitting a second block:

```
either some-condition [a: 1]

```

the **either** function will not evaluate the correct code and may produce an erroneous result.

## 7. Repeated Evaluation

The **while** and **until** functions above where used to loop until a condition was met. There are also several functions that let you loop for a specified a number of times.

### 7.1 Loop

The **loop** function evaluates a block a specified number of times. The following example prints a line of 40 dashes:

```
loop 40 [prin "-"]
----------------------------------------

```

Note that the **prin** function is similar to the **print** function, but prints its argument without a line termination.

The **loop** function returns the value of the final evaluation of the block:

```
i: 0
print loop 40 [i: i + 10]
400

```

### 7.2 Repeat

The **repeat** function extends **loop** by allowing you to monitor the loop counter. The **repeat** function's first argument is a word that will be used to hold the count value:

```
repeat count 3 [print ["count:" count]]
count: 1
count: 2
count: 3

```

The final block value is also returned:

```
i: 0
print repeat count 10 [i: i + count]
55

```

In the previous examples, the `count` word only has its value within the **repeat** block. In other words, the value of `count` is local to the block. After **repeat** finishes, `count` returns to any previous set value.

### 7.3 For

The **for** function extends **repeat** by allowing the starting value, the ending value, and the increment to the value to be specified. Any of the values can be positive or negative.

The example below begins at zero and counts to 50 by incrementing 10 each time through the loop.

```
for count 0 50 10 [print count]
0
10
20
30
40
50

```

The **for** function cycles through the loop up to and including the ending value. However, if the count exceeds the ending value, the loop is still terminated. The example below specifies an ending value of 55. That value will never be hit because the loop increments by 10 each time. The loop stops at 50.

```
for count 0 55 10 [prin [count " "]]
0 10 20 30 40 50

```

The next example shows how to count down. It begins at four and counts down to zero one at a time.

```
for count 4 0 -1 [print count]
4
3
2
1
0

```

The **for** function also works for decimal numbers, money, times, dates, series, and characters. Be sure that both the starting and ending values are of the same datatype. Here are several examples of using the **for** loop with other datatypes.

```
for count 10.5 0.0 -1 [prin [count " "]]
10.5 9.5 8.5 7.5 6.5 5.5 4.5 3.5 2.5 1.5 0.5
for money $0.00 $1.00 $0.25 [prin [money " "]]
$0.00 $0.25 $0.50 $0.75 $1.00
for time 10:00 12:00 0:20 [prin [time " "]]
10:00 10:20 10:40 11:00 11:20 11:40 12:00
for date 1-jan-2000 4-jan-2000 1 [prin [date " "]]
1-Jan-2000 2-Jan-2000 3-Jan-2000 4-Jan-2000
for char #"a" #"z" 1 [prin char]
abcdefghijklmnopqrstuvwxyz

```

The **for** function also works on series. The following example uses **for** on a string value. The word `end` is defined as the string with its current index at the `d` character. The **for** function moves through the string series one character at a time and stops when it reaches the character position defined to `end:`

```
str: "abcdef"
end: find str "d"
for s str end 1 [print s]
abcdef
bcdef
cdef
def

```

### 7.4 Foreach

The **foreach** function provides a convenient way to repeat the evaluation of a block for each element of a series. It works for all types of block and string series.

In the example below, each word in the block will be printed:

```
colors: [red green blue]
foreach color colors [print color]
red
green
blue

```

In the next example, each character in a string will be printed:

```
string: "REBOL"
foreach char string [print char]
R
E
B
O
L

```

In the example below, each filename in a directory block will be printed:

```
files: read %.
foreach file files [
    if find file ".t" [print file]
]
file.txt
file2.txt
newfile.txt
output.txt

```

When a block contains groups of values that are related, the **foreach** function can fetch all the values of the group at the same time. For example, here is a block that contains a time, string, and price. By providing the **foreach**function with a block of words for the group, each of their values can be fetched and printed.

```
movies: [
     8:30 "Contact"      $4.95
    10:15 "Ghostbusters" $3.25
    12:45 "Matrix"       $4.25
]

foreach [time title price] movies [
    print ["watch" title "at" time "for" price]
]
watch Contact at 8:30 for $4.95
watch Ghostbusters at 10:15 for $3.25
watch Matrix at 12:45 for $4.25

```

In the above example, the **foreach** value block, [`time` `title` `price`], specifies that three values are to be fetched from `movies` for each evaluation of the block.

The variables used to hold the **foreach** values are local to the block. Their value are only set within the block that is being repeated. Once the loop has exited, the variables return to their previously set values.

### 7.5 Forall and Forskip

Similar to **foreach**, the **forall** function evaluates a block for every value in a series. However, there are some important differences. The **forall** function is handed the series that is set to the beginning of the loop. As it proceeds through the loop, **forall** modifies the position within the series.

```
colors: [red green blue]
forall colors [print first colors]
red
green
blue

```

In the above example, after each evaluation of the block, the series is advanced to its next position. When **forall**returns, the `color` index is at the tail of the series.

To continue to use the series you will need to return it to its head position with the following line:

```
colors: head colors

```

The **forskip** function evaluates a block for groups of values in a series. The second argument to **forskip** is the count of how many elements to move forward after each cycle of the loop.

Like **forall**, **forskip** is handed the series with the series index set to where it is to begin. Then, **forskip**modifies the index position as it continues the loop. After each evaluation of the body block, the series index is advanced by the skip amount to its next index position. The following example demonstrates **forskip** :

```
movies: [
     8:30 "Contact"      $4.95
    10:15 "Ghostbusters" $3.25
    12:45 "Matrix"       $4.25
]

forskip movies 3 [print second movies]
Contact
Ghostbusters
Matrix

```

In the above example, **forskip** returns with the `movies` series at its tail position. You will need to use the **head**function to return the series back to its head position.

### 7.6 Forever

The **forever** function evaluates a block endlessly or until a it encounters the **break** function.

The following example uses **forever** to check for the existence of a file every ten minutes:

```
forever [
    if exists? %datafile [break]
    wait 0:10
]

```

### 7.7 Break

You can stop the repeated evaluation of a block with the **break** function. The **break** function is useful when a special condition is encountered and the loop must be stopped. The **break** function works with all types of loops.

In the following example, the loop will **break** if a number is greater than 5.

```
repeat count 10 [
    if (random count) > 5 [break]
    print "testing"
]
testing
testing
testing

```

The **break** function does not return a value from the loop unless a **/return** refinement is used:

```
print repeat count 10 [
    if (random count) > 5 [break/return "stop here"]
    print "testing"
    "normal exit"
]
testing
testing
testing
stop here

```

In the above example, if the repeat terminates without the condition occurring, the block returns the string `normal`exit. Otherwise, **break/return** will return the string `stop` here.

## 8. Selective Evaluation

There are several methods to selectively evaluate expressions in REBOL. These methods provide a way for evaluation to branch many different ways, based on a key value.

### 8.1 Select

The **select** function is often used to obtain a particular value or block, given a target value. If you define a block of values and actions, you can use **select** to search for the action that corresponds to a value.

```
cases: [
    center [print "center"]
    right  [print "right"]
    left   [print "left"]
]
action: select cases 'right
if action [do action]
right

```

In the previous example, the `select` function finds the word `right` and returns the block that follows it. (If for some reason the block was not found, then `none` would have been returned.) The block is then evaluated. The values used in the example are words, but they can be any kind of value:

```
cases: [
     5:00 [print "everywhere"]
    10:30 [print "here"]
    18:45 [print "there"]
]
action: select cases 10:30
if action [do action]
here

```

### 8.2 Switch

The **select** function is used so often that there is a special version of it called **switch**, which includes the evaluation of the resulting block. The **switch** function makes it easier to perform inline selective evaluation. For instance, to switch on a simple numeric case:

```
switch 22 [
    11 [print "here"]
    22 [print "there"]
]
there

```

The **switch** function also returns the value of the block it evaluates, so the previous example can also be written as:

```
str: copy "right "

print switch 22 [
    11 [join str "here"]
    22 [join str "there"]
]
right there

```

and:

```
car: pick [Ford Chevy Dodge] random 3
print switch car [
    Ford  [351 * 1.4]
    Chevy [454 * 5.3]
    Dodge [154 * 3.5]
]
2406.2

```

The cases can be any valid datatype, including numbers, strings, words, dates, times, urls, and files. Here are some examples:

Strings:

```
person: "kid"
switch person [
    "dad" [print "here"]
    "mom" [print "there"]
    "kid" [print "everywhere"]
]
everywhere

```

Words:

```
person: 'kid
switch person [
    dad [print "here"]
    mom [print "there"]
    kid [print "everywhere"]
]
everywhere

```

Datatypes:

```
person: 123
switch type?/word [
    string! [print "a string"]
    binary! [print "a binary"]
    integer! [print "an integer number"]
    decimal! [print "a decimal number"]
]
an integer number

```

Files:

```
file: %rebol.r
switch file [
    %user.r [print "here"]
    %rebol.r [print "everywhere"]
    %file.r [print "there"]
]
everywhere

```

URLs:

```
url: ftp://ftp.rebol.org
switch url [
    http://www.rebol.com [print "here"]
    http://www.cnet.com [print "there"]
    ftp://ftp.rebol.org [print "everywhere"]
]
everywhere

```

Tags:

```
tag: <LI>
print switch tag [
    <PRE>   ["Preformatted text"]
    <TITLE> ["Page title"]
    <LI>    ["Bulleted list item"]
]
Bulleted list item

```

Times:

```
time: 12:30
switch time [
     8:00 [send wendy@domain.dom "Hey, get up"]
    12:30 [send cindy@rebol.dom "Join me for lunch."]
    16:00 [send group@every.dom "Dinner anyone?"]
]

```

#### 8.2.1 Default Case

A default case can be specified when none of the other cases match. Use the **default** refinement to specify a default:.

```
time: 7:00
switch/default time [
     5:00 [print "everywhere"]
    10:30 [print "here"]
    18:45 [print "there"]
] [print "nowhere"]
nowhere

```

#### 8.2.2 Common Cases

If you have common cases, where the result would be the same for several values, you can define a word to hold a common block of code:

```
case1: [print length? url]   ; the common block

url: http://www.rebol.com
switch url [
    http://www.rebol.com case1
    http://www.cnet.com [print "there"]
    ftp://ftp.rebol.org case1
]
20

```

#### 8.2.3 Other Cases

More than just blocks can be evaluated for cases. This example evaluates the file that corresponds to a day of the week:

```
switch now/weekday [
    1 %monday.r
    5 %friday.r
    6 %saturday.r
]

```

So, if it's Friday, the `friday`.r file is evaluated and its result is returned from the switch. This type of evaluation also works for URLs:

```
switch time [
     8:30 ftp://ftp.rebol.org/wakeup.r
    10:30 http://www.rebol.com/break.r
    18:45 ftp://ftp.rebol.org/sleep.r
]

```

The cases for **switch** are enclosed in a block, and therefore can be defined apart from the switch statement:

```
schedule: [
     8:00 [send wendy@domain.dom "Hey, get up"]
    12:30 [send cindy@dom.dom "Join me for lunch."]
    16:00 [send group@every.dom "Dinner anyone?"]
]

switch 8:00 schedule

```

## 9. Stopping Evaluation

Evaluation of a script can be stopped at any time by pressing the escape key (ESC) on the keyboard or by using the **halt** and **quit** functions.

The **halt** function stops evaluation and returns you to the REBOL console prompt:

```
if time > 12:00 [halt]

```

The **quit** function stops evaluation and exits the REBOL interpreter:

```
if error? try [print test] [quit]

```

## 10. Trying Blocks

There are times when you want to evaluate a block, but should an error occur, you do not want to stop the evaluation of the rest of your script.

For example, you might be performing a number division, but do not want your script to stop if a divide-by-zero occurs.

The **try** function allows you to catch errors during the evaluation of a block. It is almost identical to **do**. The **try**function will normally return the result of the block; however, if an error occurs, it will return an error value instead.

In the following example, when the divide by zero occurs, the script will pass an error back to the try function, and evaluation will continue from that point.

```
for num 5 0 -1 [
    if error? try [print 10 / num] [print "error"]
]
2
2.5
3.33333333333333
5
10
error

```

More about error handling can be found in the [Errors Appendix](rebolcore-17.html#_Toc487519750).