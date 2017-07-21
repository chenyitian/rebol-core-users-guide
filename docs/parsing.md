# Parsing

## Contents:

- [1. Overview](#section-1)
- [2. Simple Splitting](#section-2)
- [3. Grammar Rules](#section-3)
- [4. Skipping Input](#section-4)
- [5. Match Types](#section-5)
- [6. Recursive Rules](#section-6)
- [7. Evaluation](#section-7)
  - [7.1 Return Value](#section-7.1)
  - [7.2 Expressions in Rules](#section-7.2)
  - [7.3 Copying the Input](#section-7.3)
  - [7.4 Marking the Input](#section-7.4)
  - [7.5 Modifying the String](#section-7.5)
  - [7.6 Using Objects](#section-7.6)
  - [7.7 Debugging](#section-7.7)
- [8. Dealing with Spaces](#section-8)
- [9. Parsing Blocks and Dialects](#section-9)
  - [9.1 Matching Words](#section-9.1)
  - [9.2 Matching Datatypes](#section-9.2)
  - [9.3 Characters Not Allowed](#section-9.3)
  - [9.4 Dialect Examples](#section-9.4)
  - [9.5 Parsing Sub-blocks](#section-9.5)
- [10. Summary of Parse Operations](#section-10)
  - [10.1 General Forms](#section-10.1)
  - [10.2 Specifying Quantity](#section-10.2)
  - [10.3 Skipping Values](#section-10.3)
  - [10.4 Getting Values](#section-10.4)
  - [10.5 Using Words](#section-10.5)
  - [10.6 Value Matches (block parsing only)](#section-10.6)
  - [10.7 Datatype Words](#section-10.7)

## 1. Overview

Parsing splits a sequence of characters or values into smaller parts. It can be used for recognizing characters or values that occur in a specific order. In addition to providing a powerful, readable, and maintainable approach to regular expression pattern matching, parsing enables you to create your own custom languages for specific purposes.

The **parse** function has the general form:

```
parse series rules

```

The `series` argument is the input that is parsed and can be a string or a block. If the argument is a string, it is parsed by character. If the argument is a block, it is parsed by value.

The `rules` argument specifies how the `series` argument is parsed. The `rules` argument can be a string for simple types of parsing or a block for sophisticated parsing.

The **parse** function also accepts two refinements: **/all** and **/case**. The **/all** refinement parses all the characters within a string, including all delimiters, such as space, tab, newline, comma, and semicolon. The **/case**refinement parses a string based on case. When **/case** is not specified, upper and lower cases are treated the same.

## 2. Simple Splitting

A simple form of **parse** is for splitting strings:

```
parse string none

```

The **parse** function splits the input argument, `string`, into a block of multiple strings, breaking each string wherever it encounters a delimiter, such as a space, tab, newline, comma, or semicolon. The `none` argument indicates that no other delimiters other than these. For example:

```
probe parse "The trip will take 21 days" none
["The" "trip" "will" "take" "21" "days"]

```

Similarly,

```
probe parse "here there,everywhere; ok" none
["here" "there" "everywhere" "ok"]

```

In the example above, notice that the commas and semicolons have been removed from the resulting strings.

You can specify your own delimiters in the second argument to **parse**. For example, the following code parses a telephone number with dash (-) delimiters:

```
probe parse "707-467-8000" "-"
["707" "467" "8000"]

```

The next example uses equal (=) and double quote (") as the delimiters:

```
probe parse <IMG SRC="test.gif" WIDTH="123"> {="}
["IMG" "SRC" "test.gif" "WIDTH" "123"]

```

The next example parses a string based on commas only; any other delimiters are ignored. Consequently, the spaces within the strings are not removed:

Normally when you parse strings, any whitespace (space, tab, lines) are automatically processed as delimiters. To avoid that action, you can use the `/any` refinement. Compare these two examples:

```
parse "Test This" ""
["Test" "This"]
parse/all "Test This" ""
["Test This"]

```

In the second, you can see that the space was not treated as a delimiter.

Here is another example:

```
probe parse/all "Harry, 1011 Main St., Ukiah" ","
["Harry" " 1011 Main St." " Ukiah"]

```

You can also parse strings that contain null characters as separators (such as certain types of data files):

```
parse/all nulled-string "^(null)"

```

## 3. Grammar Rules

The **parse** function accepts grammar rules that are written in a **dialect** of REBOL. Dialects are sub-languages of REBOL that use the same lexical form for all datatypes, but allow a different ordering of the values within a block. Within this dialect the grammar and vocabulary of REBOL is altered to make it similar in structure to the well known BNF (Backus-Naur Form) which is commonly used to specify language grammars, network protocols, header formats, etc.

To define rules, use a block to specify the sequence of the inputs. For instance, if you want to parse a string and return the characters "the phone", you can use a rule:

```
parse string ["the phone"]

```

To allow any number of spaces or no spaces between the words, write the rule like this:

```
parse string ["the" "phone"]

```

You can indicate alternate rules with a vertical bar (|). For example:

```
["the" "phone" | "a" "radio"]

```

accepts strings that match any of the following:

```
the phone
a radio

```

A rule can contain blocks that are treated as sub-rules. The following line:

```
[ ["a" | "the"] ["phone" | "radio"] ]

```

accepts strings that match any of the following:

```
a phone
a radio
the phone
the radio

```

For increased readability, write the sub-rules as a separate block and give them a name to help indicate their purpose:

```
article: ["a" | "the"]
device: ["phone" | "radio"]
parse string [article device]

```

In addition to matching a single instance of a string, you can provide a count or a range that repeats the match. The following example provides a count:

```
[3 "a" 2 "b"]

```

which accepts strings that match:

```
aaabb

```

The next example provides a range:

```
[1 3 "a" "b"]

```

which accepts strings that match any of the following:

```
ab aab aaab

```

The starting point of a range can be zero, meaning that it is optional.

```
[0 3 "a" "b"]

```

accepts strings that match any of the following:

```
b ab aab aaab

```

Use **some** to specify that one or more characters are matched. Use **any** to specify that zero or more characters are matched. For example, **some** used in the following line:

```
[some "a" "b"]

```

accepts strings that contain one or more characters `a` and `b:`

```
ab aab aaab aaaab

```

The next example uses **any:**

```
[any "a" "b"]

```

which accepts strings that contain zero or more characters `a` or `b:`

```
b ab aab aaab aaaab

```

The words **some** and **any** can also be used on blocks. For example:

```
[some ["a" | "b"]]

```

accepts strings that contain any combination of the characters `a` and `b`.

Another way to express that a character is optional is to provide an alternate choice of `none:`

```
["a" | "b" | none]

```

This example accepts strings that contain `a` or `b` or `none`.

The `none` is useful for specifying optional patterns or for catching error cases when no pattern matches.

## 4. Skipping Input

The **skip**, **to**, and **thru** words allow input to be skipped.

Use **skip** to skip a single character, or use it with a **repeat** to skip over multiple characters:

```
["a" skip "b"]
["a" 10 skip "b"]
["a" 1 10 skip]

```

To skip until a specific character is found, use **to:**

```
["a" to "b"]

```

The previous example starts parsing at `a` and ends at `b` but does not include `b`.

To include the ending character, use **thru:**

```
["a" thru "b"]

```

The previous example starts parsing at `a`, ends at `b`, and includes `b`.

The following rule finds the title of an HTML page and prints it:

```
page: read http://www.rebol.com/
parse page [thru <title> copy text to </title>]
print text
REBOL Technologies

```

The first **thru** finds the title tag and goes immediately past it. Next, the input string is copied into a variable called `text` until the ending tag is found (but it doesn't go past it, or the text would include the tag).

## 5. Match Types

When parsing strings, these datatypes and words can be used to match characters in the input string:

| Match Type   | Description                         |
| ------------ | ----------------------------------- |
| **"abc"**    | match the entire string             |
| **#"c"**     | match a single character            |
| **tag**      | match a tag string                  |
| **end**      | match to the end of the input       |
| **(bitset**) | match any specified char in the set |

To use all of these words (except bitset, which is explained below) in a single rule, use:

```
[<B> ["excellent" | "incredible"] #"!" </B> end]

```

This example parses the input strings:

```
<B>excellent!</B>
<B>incredible!</B>

```

The **end** specifies that nothing follows in the input stream. The entire input has been parsed. It is optional depending on whether the **parse** function's return value is to be checked. Refer to the [Evaluation section](#_Toc487519945) below for more information.

The **bitset** datatype deserves more explanation. Bitsets are used to specify collections of characters in an efficient manner. The **charset** function enables you to specify individual characters or ranges of characters. For example, the line:

```
digit: charset "0123456789"

```

defines a character set that contains digits. This allows rules like:

```
[3 digit "-" 3 digit "-" 4 digit]

```

which can parse phone numbers of the form:

```
707-467-8000

```

To accept any number of digits, it is common to write the rule:

```
digits: [some digit]

```

A character set can also specify ranges of characters. For instance, the `digit` character set could have be written as:

```
digit: charset [#"0" - #"9"]

```

Alternatively, you can combine specific characters and ranges of characters:

```
the-set: charset ["+-." #"0" - #"9"]

```

To expand on this, here is the alphanumeric set of characters:

```
alphanum: charset [#"0" - #"9" #"A" - #"Z" #"a" - #"z"]

```

Character sets can also be modified with the **insert** and **remove** functions, or combinations of sets can be created with the **union** and **intersect** functions. This line copies the digit character set and adds a dot to it:

```
digit-dot: insert copy digit "."

```

The following lines define useful character sets for parsing:

```
digit: charset [#"0" - #"9"]
alpha: charset [#"A" - #"Z" #"a" - #"z"]
alphanum: union alpha digit

```

## 6. Recursive Rules

Here is an example of rule set that parses mathematical expressions and gives a precedence (a priority) to the math operators used:

```
expr:    [term ["+" | "-"] expr | term]
term:    [factor ["*" | "/"] term | factor]
factor:  [primary "**" factor | primary]
primary: [some digit | "(" expr ")"]
digit:   charset "0123456789"

```

Now we can parse many types of math expressions. The following examples return `true`, indicating that the expressions were valid:

```
probe parse "1 + 2 * ( 3 - 2 ) / 4" expr
true
probe parse "4/5+3**2-(5*6+1)" expr
true

```

Notice in the examples that some of the rules refer to themselves. For instance, the `expr` rule includes `expr`. This is a useful technique for defining repeating sequences and combinations. The rule is **recursive** --it refers to itself.

When using recursive rules, care is required to prevent endless recursion. For instance:

```
expr: [expr ["+" | "-"] term]

```

creates an infinite loop because the first thing `expr` does is use `expr` again.

## 7. Evaluation

Normally, you parse a string to produce some result. You want to do more than just verify that the string is valid, you want to do something as it is parsed. For instance, you may want to pick out substrings from various parts of the string, create blocks of related values, or compute a value.

### 7.1 Return Value

The examples in previous chapters showed how to parse strings, but no results were produced. This is only done to verify that a string has the specified grammar; the value returned from **parse** indicates its success. The following examples show this:

```
probe parse "a b c" ["a" "b" "c"]
true
probe parse "a b" ["a" "c"]
false

```

The **parse** function returns `true` only if it reaches the end of the input string. An unsuccessful match stops the parse of the series. If **parse** runs out of values to search for before reaching the end of the series, it does not traverse the series and returns `false` **:**

```
probe parse "a b c d" ["a" "b" "c"]
false
probe parse "a b c d" [to "b" thru "d"]
true
probe parse "a b c d" [to "b" to end]
true

```

### 7.2 Expressions in Rules

Within a rule, you can include a REBOL expression to be evaluated when **parse** reaches that point in the rule. Parentheses are used to indicate such expressions:

```
string: "there is a phone in this sentence"
probe parse string [
    to "a"
    to "phone" (print "found phone")
    to end
]
found phone
true

```

The example above parses the string `a` `phone` and prints the message `found` `phone` after the match is complete. If the strings `a` or `phone` are missing and the parse can not be done, the expression is not evaluated.

Expressions can appear anywhere within a rule, and multiple expressions can occur in different parts of a rule. For instance, the following code prints different strings depending on what inputs were found:

```
parse string [
    "a" | "the"
    to "phone" (print "answer") |
    to "radio" (print "listen") |
    to "tv"    (print "watch")
]
answer
string: "there is the radio on the shelf"

parse string [
    "a" | "the"
    to "phone" (print "answer") |
    to "radio" (print "listen") |
    to "tv"    (print "watch")
]
listen

```

Here is an example that counts the number of times the HTML pre-format tag appears in a text string:

```
count: 0
page: read http://www.rebol.com/docs/dictionary.html
parse page [any [thru <pre> (count: count + 1)]]
print count
777

```

### 7.3 Copying the Input

The most common action done with **parse** is to pick up parts of the string being parsed. This is done with **copy**, and it is followed by the name of a variable to which you want to copy the string. The following example parses the title of a web page:

```
parse page [thru <title> copy text to </title>]
print text
REBOL/Core Dictionary

```

The example works by skipping over text until it finds the <title> tag. That's where it starts making a copy of the input stream and setting a variable called `text` to hold it. The copy operation continues until the closing <title> tag is found.

The copy action also can be used with entire rule blocks. For instance, for the rule:

```
[copy heading ["H" ["1" | "2" | "3"]]

```

the heading string contains the entire `H1`, `H2`, or `H3` string. This also works for large multi-block rules.

### 7.4 Marking the Input

The **copy** action makes a copy of the substring that it finds, but that is not always desirable. In some cases, it is better to save the current position of the input stream in a variable.

NOTE: The **copy** word as used in parse is different from the **copy** function used in REBOL expressions. Parse uses a dialect of REBOL, and **copy** has a different meaning within that dialect.

In the following example, the `begin` variable holds a reference to the `page` input string just after <title>. The`ending` refers to the `page` string just before ``. These variables can be used in the same way as they would be used with any other series.

```
parse page [
    thru <title> begin: to </title> ending:
    (change/part begin "Word Reference Guide" ending)
]

```

You can see the above parse expression actually changed the contents of the title:

```
parse page [thru <title> copy text to </title>]
print text
Word Reference Guide

```

Here is another example that marks the position of every table tag in an HTML file:

```
page: read http://www.rebol.com/index.html
tables: make block! 20
parse page [
    any [to "<table" mark: thru ">"
        (append tables index? mark)
    ]
]

```

The `tables` block now contains the position of every tag:

```
foreach table tables [
    print ["table found at index:" table]
]
table found at index: 836
table found at index: 2076
table found at index: 3747
table found at index: 3815
table found at index: 4027
table found at index: 4415
table found at index: 6050
table found at index: 6556
table found at index: 7229
table found at index: 8268

```

NOTE: The current position in the input string can also be modified. The next section explains how this is done.

### 7.5 Modifying the String

Now that you know how to obtain the position of the input series, you also can use other series functions on it, including **insert**, **remove**, and **change**. To write a script that replaces all question marks (?) with exclamation marks (!), write:

```
str: "Where is the turkey? Have you seen the turkey?"
parse str [some [to "?" mark: (change mark "!") skip]]
print str
Where is the turkey! Have you seen the turkey!

```

The **skip** at the tail advances the input over the new character, which is not necessary in this case, but it is a good practice.

As another example, to insert the current time everywhere the word `time` appears in some text, write:

```
str: "at this time, I'd like to see the time change"
parse str [
    some [to "time"
        mark:
        (remove/part mark 4  mark: insert mark now/time)
        :mark
    ]
]
print str
at this 14:42:12, I'd like to see the 14:42:12 change

```

Notice the `:mark` word used above. It sets the input to a new position. The **insert** function returns the new position just past the insert of the current time. The word `:mark` is used to set the input to that position.

### 7.6 Using Objects

When parsing large grammar from a set of rules, variables are used to make the grammar more readable. However, the variables are global and may become confused with other variables that have the same name somewhere else in the program.

The solution to this problem is to use an object to make all the rule words local to a context. For instance:

```
tag-parser: make object! [
    tags: make block! 100
    text: make string! 8000
    html-code: [
        copy tag ["<" thru ">"] (append tags tag) |
        copy txt to "<" (append text txt)
    ]
    parse-tags: func [site [url!]] [
        clear tags clear text
        parse read site [to "<" some html-code]
        foreach tag tags [print tag]
        print text
    ]
]
tag-parser/parse-tags http://www.rebol.com

```

### 7.7 Debugging

As rules are written, there are times debugging is needed. Specifically, you may want to know how far you got in the parsing of a rule.

The **trace** function can be used to watch the parse operation progress, but this can output thousands of lines that are difficult to review.

A better way is to insert debugging expressions into the parse rules. As an example, to debug the rule:

```
[to "<IMG" "SRC" "=" filename ">"]

```

insert a the **print** function after key sections to monitor your progress through the rule:

```
[to "<IMG" (print 1) "SRC" "=" (print 2)
    filename (print 3) ">"]

```

This example prints `1`, `2`, and `3` as the rule is processed.

Another approach is to print out part of the input string as the parse happens:

```
[
   to "<IMG" here: (print here)
   "SRC" "=" here: (print here)
    filename here: (print here) ">"
]

```

If this is done often, you can create a rule for it:

```
here: [where: (print where)]

[
   to "<IMG" here
   "SRC" "=" here
    filename here ">"
]

```

The **copy** function can also be used to indicate what substrings were parsed as the rule was handled.

## 8. Dealing with Spaces

The **parse** function normally ignores all intervening whitespace between patterns that it scans. For instance, the rule:

```
["a" "b" "c"]

```

returns strings that match:

```
abc
a bc
ab c
a b c
a  b  c

```

and other similarly spaced combinations.

To enforce a specific spacing convention, use **parse** with the **/all** refinement. In the preceeding example, this refinement causes **parse** to only match the first case (abc).

```
parse/all "abc" ["a" "b" "c"]

```

Specifying the /**** all refinement forces every character in the input stream to be dealt with, including the default delimiters, such as space, tab, newline.

To handle spaces in your rules, create a character set that specifies the valid space characters:

```
spacer: charset reduce [tab newline #" "]

```

If you want a single space character between each letter write:

```
["a" spacer "b" spacer "c"]

```

To allow multiple space characters, write:

```
spaces: [some spacer]
["a" spaces "b" spaces "c"]

```

For more sophisticated grammars, create a character set that lets you scan a string up to a space character.

```
non-space: complement spacer
to-space: [some non-space | end]
words: make block! 20
parse/all text [
    some [copy word to-space (append words word) spacer]
]

```

The preceding example builds a block of all of its words. The **complement** function inverts the character set. Now it contains everything **except** the spacing characters you defined earlier. The `non-space` character set contains all characters except space characters. The `to-space` rule accepts one or more characters up to a space character or the end of the input stream. The main rule expects to begin with a word, copy that word up to a space, then skip the space character and begin the next word.

## 9. Parsing Blocks and Dialects

Blocks are parsed similar to strings. A set of rules specify the order of expected values. However, unlike the parsing of strings, the parsing of blocks is not concerned with characters or delimiters. Parsing of blocks is done at the value level, making the grammar rules easier to specify and operation many times faster.

Block parsing is the easiest way to create REBOL **dialects**. Dialects are sub-languages of REBOL that use the same lexical form for all data types but allow a different ordering of the values within a block. The values do not need to conform to the normal order required by REBOL function arguments. Dialects are able to provide greater expressive power for specific domains of use. For instance, the parser rules themselves are specified as a dialect.

### 9.1 Matching Words

When parsing a block, to match against a word specify the word as a literal:

```
'name
'when
'empty

```

### 9.2 Matching Datatypes

You can match a value of any datatype by specifying the data type word. See Datatype Matches below.

| Datatype Word | Description               |
| ------------- | ------------------------- |
| string!       | matches any quoted string |
| time!         | matches any time          |
| date!         | matches any date          |
| tuple!        | matches any tuple         |

NOTE: Don't forget the "!" that is part of the name or an error will be generated.

### 9.3 Characters Not Allowed

The **parse** operations allowed for blocks are those that deal with specific characters. For instance, a match cannot be specified to the first letter of a word or string, nor to spacing or newline characters.

### 9.4 Dialect Examples

A few concise examples help illustrate the parsing of blocks:

```
block: [when 10:30]
print parse block ['when 10:30]
print parse block ['when time!]
parse block ['when set time time! (print time)]

```

Notice that a specific word can be matched by using its literal word in the rule (as in the case of `'when` ). A datatype can be specified rather than a value, as in the lines above containing **time!**. In addition, a variable can be set to a value with the **set** operation.

As with strings, alternate rules can be specified when parsing blocks:

```
rule: [some [
    'when set time time! |
    'where set place string! |
    'who set persons [word! | block!]
]]

```

These rules allow information to be entered in any order:

```
parse [
    who Fred
    where "Downtown Center"
    when 9:30
] rule
print [time place persons]

```

This example could have used variable assignment, but it illustrates how to provide alternate input ordering.

Here's another example that evaluates the results of the parse:

```
rule: [
    set count integer!
    set str string!
    (loop count [print str])
]
parse [3 "great job"] rule
parse [3 "hut" 1 "hike"] [some rule]

```

Finally, here is a more advanced example:

```
rule: [
    set action ['buy | 'sell]
    set number integer!
    'shares 'at
    set price money!
    (either action = 'sell [
            print ["income" price * number]
            total: total + (price * number)
        ][
            print ["cost" price * number]
            total: total - (price * number)
        ]
    )
]

total: 0
parse [sell 100 shares at $123.45] rule
print ["total:" total]

total: 0
parse [
    sell 300 shares at $89.08
    buy  100 shares at $120.45
    sell 400 shares at $270.89
] [some rule]
print ["total:" total]

```

It should be noted that this is one way how expressions that use the **dialect** concept first described in Chapter 4 can be **evaluated**.

### 9.5 Parsing Sub-blocks

When parsing a block, if a sub-block is found, it is treated as a single value that is of the **block!** datatype. However, to parse a sub-block, you must invoke the parser recursively on the sub-block. The **into** word provides this capability. It expects that the next value in the input block is a sub-block to be parsed. This is as if a **block!**datatype had been provided. If the next value is not a **block!** datatype, the match fails and **into** looks for alternates or exits the rule. If the next value is a block, the parser rule that follows the **into** word is used to begin parsing the sub-block. It is processed in the same way as a sub-rule.

```
rule: [date! into [string! time!]]
data: [10-Jan-2000 ["Ukiah" 10:30]]
print parse data rule

```

All of the normal parser operations can be applied to **into**.

```
rule: [
    set date date!
    set info into [string! time!]]
]
data: [10-Jan-2000 ["Ukiah" 10:30]]
print parse data rule

print info

rule: [date! copy items 2 into [string! time!]]
data: [10-Jan-2000 ["Ukiah" 10:30] ["Rome" 2:45]]
print parse data rule

probe items

```

## 10. Summary of Parse Operations

### 10.1 General Forms

| Operator | Description                 |
| -------- | --------------------------- |
| &vert;        | alternate rule              |
| [block]  | sub-rule                    |
| (paren)  | evaluate a REBOL expression |

### 10.2 Specifying Quantity

| Operator | Description                  |
| -------- | ---------------------------- |
| none     | match nothing                |
| opt      | zero or one time             |
| some     | one or more times            |
| any      | zero or more times           |
| 12       | repeat pattern 12 times      |
| 1 12     | repeat pattern 1 to 12 times |
| 0 12     | repeat pattern 0 to 12 times |

### 10.3 Skipping Values

| Operator | Description                              |
| -------- | ---------------------------------------- |
| skip     | skip a value (or multiple if repeat given) |
| to       | advance input to a value or datatype     |
| thru     | advance input thru a value or datatype   |

### 10.4 Getting Values

| Operator | Description                              |
| -------- | ---------------------------------------- |
| set      | set the next value to a variable         |
| copy     | copy the next match sequence to a variable |

### 10.5 Using Words

| Operator | Description                              |
| -------- | ---------------------------------------- |
| word     | look-up value of a word                  |
| word:    | mark the current input series position   |
| :word    | set the current input series position    |
| 'word    | matches the word literally (parse block) |

### 10.6 Value Matches (block parsing only)

| Operator | Description                 |
| -------- | --------------------------- |
| "fred"   | matches the string "fred"   |
| %data    | matches the file name %data |
| 10:30    | matches the time 10:30      |
| 1.2.3    | matches the tuple 1.2.3     |

### 10.7 Datatype Words

| Word  | Description                          |
| ----- | ------------------------------------ |
| type! | matches anything of a given datatype |