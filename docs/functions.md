# Chapter 9 - Functions

## Contents:

[1. Overview](#section-1)
[2. Evaluating Functions](#section-2)
  [2.1 Arguments](#section-2.1)
  [2.2 Argument Data Types](#section-2.2)
  [2.3 Refinements](#section-2.3)
  [2.4 Function Values](#section-2.4)
[3. Defining Functions](#section-3)
  [3.1 Interface Specifications](#section-3.1)
  [3.2 Literal Arguments](#section-3.2)
  [3.3 Get Arguments](#section-3.3)
  [3.4 Defining Refinements](#section-3.4)
  [3.5 Local Variables](#section-3.5)
  [3.6 Local Variables Containing Series](#section-3.6)
  [3.7 Returning a Value](#section-3.7)
  [3.8 Returning Multiple Values](#section-3.8)
[4. Nested Functions](#section-4)
[5. Unnamed Functions](#section-5)
[6. Conditional Functions](#section-6)
[7. Function Attributes](#section-7)
[8. Forward References](#section-8)
[9. Scope of Variables](#section-9)
[10. Reflective Properties](#section-10)
[11. Online Function Help](#section-11)
[12. Viewing Source Code](#section-12)

## 1. Overview

There are several kinds of functions provided by REBOL:

|      | **Native**    | A function that is evaluated directly by the processor. These are the lowest level functions of the language. |
| ---- | ------------- | ---------------------------------------- |
|      | **Function**  | A higher level function that is defined by a block and is evaluated by evaluating the functions within the block. Also called user-defined functions. |
|      | **Mezzanine** | A name for higher level functions that are a standard part of the language. These are not native functions. |
|      | **Operator**  | A function that is used as an infix operator. Examples are +, -, * and /. |
|      | **Routine**   | A function that is used to call external library functions (REBOL/Command feature). |

## 2. Evaluating Functions

The [Expressions Chapter](rebolcore-4.html) covered the general details of evaluation. The way function arguments are evaluated dictates the general order of words and values in the language. This section goes into more detail on how functions are evaluated.

### 2.1 Arguments

Functions receive arguments and return results. Most functions require one or more arguments; although, some functions, such as **now** (current date and time), do not require any arguments.

The arguments that are supplied to a function are processed by the interpreter and then passed to the function. Arguments are processed in the same way, regardless of the type of function called, be it a native function, operator, user-defined function, or otherwise. For example, the **send** function expects two arguments:

```
friend: luke@rebol.com
message: "message in a bottle"

send friend message

```

The word `friend` is first evaluated and its value (`luke@rebol`.com ) is provided as the first argument to **send**. Next, the word `message` is evaluated, and its value becomes the second argument. Think of the values of the`friend` and `message` variables as being substituted into the line before **send** is done:

```
send luke@rebol.com "message in a bottle"

```

If you provide too few arguments to a function, an error message is returned. For example, the send function expects two arguments and if you send one, an error is returned

```
send friend
** Script Error: send is missing its message argument.
** Where: send friend

```

If too many arguments are provided, the extra values are ignored.

```
send friend message "urgent"

```

In the previous example, **send** already has two arguments, so the string, which is the third argument, is ignored. Notice that no error message occurs. In this case, there were no functions expecting the third argument. However, in some cases the third argument may belong to another function that was evaluated before **send**.

Arguments to a function are evaluated from left to right. This order is followed even when the arguments themselves are functions. For example, if you write:

```
send friend detab copy message

```

the second argument must be computed by evaluating the **detab** function and the **copy** function. The result of the**copy** will be passed to **detab**, and the result of **detab** will be passed to **send**. In the previous example, the **copy**function is taking a single argument, the `message`, and returns a copy of it. The copied message is passed to the **detab** function, which removes the tab characters and returns the detabbed message, which is passed to the **send** function. Notice how the results of functions flow from right to left as the expression is evaluated.

The evaluation that is happening here can be shown by using parentheses to clarify what is evaluated first. (However, the parentheses are not required, and actually slow down the evaluation slightly.)

```
send friend (detab (copy message))

```

The cascading effect of results passed to functions is quite useful. Here is an example that uses **insert** twice within the same expression:

```
file: %image
insert tail insert file %graphics/ %.jpg
print file
graphics/image.jpg

```

In the following example, a directory name and a suffix are added to the base file name. Parentheses can be used to clarify the order of evaluation:

```
insert (tail (insert file %graphics/)) %.jpg

```

**A Note About Parentheses**

Parentheses make good "training wheels" to get started in writing REBOL. However, it won't take long before you can shed this aid and write the expressions directly without the parentheses. Not using parentheses lets the interpreter evaluate expressions quicker.

### 2.2 Argument Data Types

Functions usually require arguments of a specific data type. For example, the first argument to the **send** function can only be an email address or block of email addresses. Any other type of value will produce an error:

```
send 1234 "numbers"
** Script Error: send expected address argument of type: email block.
** Where: send 1234 "numbers"

```

In the previous example, the error message is telling you that the address argument of the **send** function needs to be either an email address or a block.

A quick way to find out what types of arguments are accepted by a function is to type the following at the console prompt:

```
help send
USAGE:
    SEND address message /only /header header-obj
DESCRIPTION:
    Send a message to an address (or block of addresses)
    SEND is a function value.
ARGUMENTS:
    address -- An address or block of addresses (Type: email block)
    message -- Text of message. First line is subject. (Type: any)
REFINEMENTS:
    /only -- Send only one message to multiple addresses
    /header -- Supply your own custom header
        header-obj -- The header to use (Type: object)

```

The `ARGUMENTS` section indicates the data type of each argument. Notice that the second argument can be of any data type. So, it is valid to write:

```
send luke@rebol.com $1000.00

```

### 2.3 Refinements

A refinement specifies a variation in the normal evaluation of a function. Refinements also allow optional arguments to be provided. Refinements are available for both native and user-defined functions.

Refinements are specified by following the function name with a forward slash (/) and a refinement name. For instance:

```
copy/part  (copy just part of a string)

find/tail  (return the tail of the match)

load/markup  (return XML/HTML tags and strings)

```

Functions can also include multiple refinements:

```
find/case/tail (match case and return tail)

insert/only/dup (insert entire block multiple times)

```

You have seen the **copy** function used to make a copy of a string. By default, **copy** returns a copy of its argument:

```
string: "no time like the present"
print copy string
no time like the present

```

Using the **/part** refinement, **copy** returns part of the string:

```
print copy/part string 7
no time

```

In the previous example, the **/part** refinement specifies that only seven characters of the string are copied.

To review what refinements are allowed on a function such as **copy**, use online help:

```
help copy
USAGE:
    COPY value /part range /deep
DESCRIPTION:
     Returns a copy of a value.
     COPY is an action value.
ARGUMENTS:
     value -- Usually a series (Type: series port bitset)
REFINEMENTS:
     /part -- Limits to a given length or position.
         range -- (Type: number series port)
     /deep -- Also copies series values within the block.

```

Notice that the **/part** refinement requires an additional argument. Not all refinements require additional arguments. For example, the **/deep** refinement specifies that **copy** make copies of all its sub-blocks. No other arguments are required.

When multiple refinements are used with a function, the order of the extra arguments is determined by the order in which the refinements are specified. For example:

```
str: "test"
insert/dup/part str "this one" 4 5
print str
this this this this test

```

Reversing the order of the **/dup** and **/part** refinement changes the order of the arguments. You can see the difference:

```
str: "test"
insert/part/dup str "this one" 4 5
print str
thisthisthisthisthistest

```

The refinements indicate the order of the arguments.

### 2.4 Function Values

The previous examples describe how functions return values when they are evaluated. Sometimes, however, you want to obtain the function as a value, not the value it returns. This can be done by preceding the function name with a colon or using the **get** function. For example, to set a word, `pr`, to the **print** function, you would write:

```
pr: :print

```

You could also write:

```
pr: get `print

```

Now **pr** is equivalent to the **print** function:

```
pr "this is a test"
this is a test

```

## 3. Defining Functions

You can define functions that work in the same way as native functions. These are called **user-defined** functions. User-defined functions are of the **function!** data type.

You can make simple functions that require no arguments with the **does** function. This example defines a new function that prints the current time:

```
print-time: does [print now/time]
print-time
10:30

```

The **does** function returns a value, which is the new function. In the example, the `print-time` word is set to the function. However, this function value can be set to a word, passed to another function, returned as the result of a function, saved in a block, or immediately evaluated.

Functions that require arguments are made with the **func** function, which accepts two arguments:

```
func spec body

```

The first argument is a block that specifies the interface to the function. It includes a description of the function, its arguments, the types allowed for arguments, descriptions of the arguments, and other items. The second argument is a block of code that is evaluated whenever the function is evaluated.

Here is an example of a new function called `sum:`

```
sum: func [arg1 arg2] [arg1 + arg2]

```

The newly defined function accepts two arguments, as specified in the first block. The second block is the body of the function, which, when evaluated, adds the two arguments together. The new function is returned as a value from **func** and the `sum` word is set to it. Here it is in use:

```
print sum 123 321
444

```

The result of `arg1` being added to `arg2` is returned and printed.

**Func is Defined in REBOL**

**Func** is a function that makes other functions. It performs a make on the **function!** data type. **Func** is defined as:

```
func: make function! [args body] [
    make function! args body
]

```

### 3.1 Interface Specifications

The first block of a function definition is called its **interface** **specification**. This block includes a description of the function, its arguments, the data types allowed for arguments, descriptions of the arguments, and other items.

The interface specification is a dialect of REBOL (because it has different evaluation rules than normal code). The specification block has the format:

```
[
    "function description"
    [optional-attributes]

    argument-1 [optional-type]
    "argument description"

    argument-2 [optional-type]
    "argument description"

    ...

    /refinement
    "refinement description"

    refinement-argument-1 [optional-type]
    "refinement argument description"

    ...
]

```

The fields of the specification block are:

|      | **Description**                     | A short description of the function. This is a string that can be accessed by other functions such as help to output descriptions of functions. |
| ---- | ----------------------------------- | ---------------------------------------- |
|      | **Attributes**                      | A block that describes special properties of the function, such as its behavior on errors. It may be expanded in the future to include flags for optimizations. |
|      | **Argument**                        | A variable that is used to access an argument from within the body of the function. |
|      | **Arg Type**                        | A block that identifies the data types that are accepted by the function. If a data type not identified in this block is passed to the function, an error will occur. |
|      | **Arg Description**                 | A short description of the argument. Like the function description, this can be accessed by other functions such as help. |
|      | **Refinement**                      | A refinement word that indicates special behavior is required of the function. |
|      | **Refinement Description**          | A short description of the refinement.   |
|      | **Refinement Argument**             | A variable that is used by the refinement. |
|      | **Refinement Argument Type**        | A block that identifies the data types that are accepted by the refinement. |
|      | **Refinement Argument Description** | A short description of the refinement argument. |

All of these fields are optional.

As an example, the argument block of the `sum` function (defined in a previous example) is expanded to restrict the type of arguments accepted. It also includes a description of the function and its expected arguments.

```
sum: func [
    "Return the sum of two numbers."
    arg1 [number!] "first number"
    arg2 [number!] "second number"
][
    arg1 + arg2
]

```

Now, the data type of the arguments is automatically checked, catching errors like:

```
print sum 1 "test"
** Script Error: sum expected arg2 argument of type: number.
** Where: print sum 1 "test"

```

To allow additional argument data types, more than one can be given:

```
sum: func [
    "Return the sum of two numbers."
    arg1 [number! tuple! money!] "first number"
    arg2 [number! tuple! money!] "second number"
][
    arg1 + arg2
]

print sum 1.2.3 3.2.1
4.4.4
print sum $1234 100
$1334.00

```

Now the `sum` function accepts a number, tuple, or monetary value as arguments. If within the function you need to distinguish what data type was passed, you can use the data type test functions:

```
if tuple? arg1 [print arg1]

if money? arg2 [print arg2]

```

Because the `sum` function provided description strings, the **help** function now supplies useful information about it:

```
help sum
USAGE:
    SUM arg1 arg2
DESCRIPTION:
     Return the sum of two numbers.
     SUM is a function value.
ARGUMENTS:
     arg1 -- first number (Type: number tuple money)
     arg2 -- second number (Type: number tuple money)

```

### 3.2 Literal Arguments

As described earlier, the interpreter evaluates the arguments of functions and passes them to the function body. However, there are times when you do not want function arguments evaluated. For instance, if you need to pass a word and access it from the function body, you do not want it evaluated as an argument. The **help** function, which expects a word, is a good example:

```
help print

```

To prevent **print** from being evaluated, the **help** function must specify that its argument should not be evaluated.

To specify that an argument not be evaluated, precede the argument name with a single quote (indicates a literal word). For example:

```
zap: func [`var] [set var 0]

test: 10
zap test
print test
10

```

The `var` argument is preceded with a single quote, which instructs the interpreter to obtain the argument without evaluating it first. The argument is passed as the word. For example:

```
say: func [`var] [probe var]
say test
test

```

The example prints the word that is passed as an argument.

Another example is a function that increments a variable by one and returns its result (similar to the ++ increment function in C):

```
++: func ['word] [set word 1 + get word]

count: 0
++ count
print count
1
print ++ count
2

```

### 3.3 Get Arguments

Function arguments can also specify that a word's value be fetched but not evaluated. This is similar to the literal arguments described above, but rather than passing the word, the value of the word is passed without being evaluated.

To specify that an argument be fetched but not evaluated, precede the argument name with a colon. For example, the following function accepts functions as arguments:

```
print-body: func [:fun] [probe second :fun]

```

The sample function prints the body of a function that is passed to it. The argument is preceded by a colon, which indicates that the value of the word should be obtained, but not further evaluated.

```
print-body reform
[form reduce value]
print-body rejoin
[
    if empty? block: reduce block [return block]
    append either series? first block [copy first block] [
        form first block] next block
]

```

### 3.4 Defining Refinements

Refinements can be used to specify variation in the normal evaluation of a function as well as provide optional arguments. Refinements are added to the function specification block as a word preceded by a forward slash (/).

Within the body of the function, the refinement word is used as a logic value to determine if the refinement was provided when the function was called.

For example, the following code adds a refinement to the `sum` function, which was defined in a previous example:

```
sum: func [
    "Return the sum of two numbers."
    arg1 [number!] "first number"
    arg2 [number!] "second number"
    /average "return the average of the numbers"
][
    either average [arg1 + arg2 / 2][arg1 + arg2]
]

```

The `sum` function specifies the `/average` refinement. In the body of the function, the word is tested with the either function, which returns true when the refinement is specified.

```
print sum/average 123 321
222

```

To specify a refinement that accepts additional arguments, follow the refinement with the arguments definitions:

```
sum: func [
    "Return the sum of two numbers."
    arg1 [number!] "first number"
    arg2 [number!] "second number"
    /times "multiply the result"
    amount [number!] "how many times"
][
    either times [arg1 + arg2 * amount][arg1 + arg2]
]

```

The `amount` is only valid when the `times` refinement is true. Here is an example:

```
print sum/times 123 321 10
4440

```

Do not forget to check the refinement word before using the additional arguments. If a refinement argument is used without the refinement being specified, it will have a `none` value.

### 3.5 Local Variables

A local variable is a word whose value is defined within the scope of a function. Changes to a local variable only affect the function in which the variable is defined. If the same word is used outside of the function, it will not be affected by the changes to the local variable of the same name.

Argument variables and refinements are local variables. Their values are defined within the scope of the function. By convention, additional local variables can be specified with the **/local** refinement. The **/local** refinement is followed by a list of words that are used as local variables within the function.

```
average: func [
    block "Block of numbers"
    /local total length
][
    total: 0
    length: length? block
    foreach num block [total: total + num]
    either length > 0 [total / length][0]
]

```

Here the `total` and `length` words are local to the function.

Another method of creating local words is to use the **function** function, which is identical to **func**, but accepts a separate block that contains the local words:

```
average: function [
    block "Block of numbers"
][
    total length
][
    total: 0
    length: length? block
    foreach num block [total: total + num]
    either length > 0 [total / length][0]
]

```

In this example, notice that the **/local** refinement is not used with the **function** function. The **function**function creates the refinements for you.

If a local variable is used before its value has been set within the body of its function, it will have a `none` value.

### 3.6 Local Variables Containing Series

Local variables that hold series need to be copied if the series is used multiple times. For example, if you want the `stars` string to be the same each time you call the `start-name` function, you should write:

```
star-name: func [name] [
    stars: copy "**"
    insert next stars name
    stars
]

```

Otherwise, if you write:

```
star-name: func [name] [
    stars: "**"
    insert next stars name
    stars
]

```

you will be using the same string each time and each time the function is used the pervious name will appear within the result.

```
print star-name "test"
*test*
print star-name "this"
*thistest*

```

**This is Important**

The concept described above is important to remember. If you forget it, you will observe odd results in your programs.

### 3.7 Returning a Value

As you know from the [Expressions Chapter](rebolcore-4.html#_Toc487519750), blocks return their last value when they return from evaluation:

```
do [1 + 3  5 + 7]
12

```

This is also true for functions. The last value is returned as the value of the function:

```
sum: func [a b] [
    print a
    print b
    a + b
]

print sum 123 321
123
321
444

```

In addition, the **return** function can be used to stop the evaluation of a function at any point and return a value:

```
find-value: func [series value] [
    forall series [
        if (first series) = value [
            return series
        ]
    ]
    none
]

probe find-value [1 2 3 4] 3
[3 4]

```

In the example, if the value is found, the function returns the series at the position of the match. Otherwise, the function returns `none`.

To stop a function evaluation without returning a value, use the **exit** function:

```
source: func [
    "Print the source code for a word"
    'word [word!]
][
    prin join word ": "
    if not value? word [print "undefined" exit]
    either any [
        native? get word op? get word action? get word
    ][
        print ["native" mold third get word]
    ][print mold get word]
]

```

### 3.8 Returning Multiple Values

To return more than one value from a function, use a block. You can do this easily by returning a block that has been reduced.

For example:

```
find-value: func [series value /local count] [
    forall series [
        if (first series) = value [
            reduce [series  index? series]
        ]
    ]
    none
]

```

The function returns a block that holds the series and the index value where the value was found.

```
probe find-value [1 2 3 4] 3
[[3 4] 3]

```

The **reduce** is necessary to create a block of values from the block of words that it is given. Do not return the local variables themselves. That is not a supported mode of operation (currently).

To easily set variables to the return value of the function, use **set:**

```
set [block index] find-value [1 2 3 4] 3
print block
3 4
print index
3

```

## 4. Nested Functions

Functions can define other functions. The sub-functions can be global, local, or returned as a result, depending on their purpose.

For example, to create a global function from within a function, assign it to a global variable:

```
make-timer: func [code] [
    timer: func [time] code
]
make-timer [wait time]
timer 5

```

To make a local function, assign it to a local variable:

```
do-timer: func [code delay /local timer] [
    timer: func [time] code
    timer delay
    timer delay
]
do-timer [wait time] 5

```

The `timer` function only exists during the period when the `do-timer` function is being evaluated.

To return a function as a result:

```
make-timer: func [code] [
    func [time] code
]
timer: make-timer [wait time]
timer 5

```

**Use Correct Local Variables**

You should avoid using variables that are local to the top level function as an unevaluated part of the nested function. For example:

```
make-timer: func [code delay] [
    timer: func [time] [wait time + delay]
]

```

In the example, the `delay` word dynamically belongs to the `make-timer` function. This should be avoided, as the `delay` value will change in subsequent calls to `make-timer`.

## 5. Unnamed Functions

Function names are variables. In REBOL, a variable is a variable, regardless of what it holds. There is nothing special about function variables.

Furthermore, functions do not require names. You can create a function and immediately evaluate it, store it in a block, pass it as an argument to a function, or return it as a result from a function. Such functions are unnamed.

Here is an example that creates a block of unnamed functions:

```
funcs: []
repeat n 10 [
    append funcs func [t] compose [t + (n * 100)]
]
print funcs/1 10
110
print funcs/5 10
510

```

Functions can also be created and passed to other functions. For instance, when you use **sort** with your own comparison, you provide a function as an argument:

```
sort/compare data func [a b] [a > b]

```

## 6. Conditional Functions

Because functions are created dynamically by evaluation, you can determine how you want a function created, based on other information. This is a way to provide conditional code as is found in the macro or preprocessor sub-languages of other programming languages. Within the REBOL language this type of conditional code is done with normal REBOL code.

For instance, you may want to create a debugging version of a function that prints additional information:

```
test-mode: on

timer: either test-mode [
    func [delay] [
        print "delaying..."
        wait delay
        print "resuming"
    ]
][
    func [delay] [wait delay]
]

```

Here you will create one of two functions, based on the test-mode you are running. This can also be written shorter as:

```
timer: func [delay] either test-mode [[
    print "delaying..."
    wait delay
    print "resuming"
]][[wait delay]]

```

## 7. Function Attributes

Function attributes provide control over specific function behaviors, such as the method a function uses to handle errors or to exit. The attributes are an optional block of words within the interface specifications.

There are currently two function attributes: **catch** and **throw**.

Error messages typically are displayed when they occur within the function. If the **catch** attribute is specified, errors that are thrown within the function are caught automatically by the function. The errors are not displayed within the function but at the point where the function was used. This is useful if you are providing a function library (mezzanine functions) and don't want the error to be displayed within your function, but where it was called:

```
root: func [[catch] num [number!]] [
    if num < 0 [
        throw make error! "only positive numbers"
    ]
    square-root num
]

root 4
2
root -4
**User Error: only positive numbers
**Where: root -4

```

Notice that in this example, the error occurs where `root` was called even though the actual error was generated in the body of the function. This is because the **catch** attribute was used.

Without the **catch** attribute, the error would occur within the `root` function:

```
root: func [num [number!]] [
    square-root num
]
root -4
** Math Error: Positive number required.
** Where: square-root num

```

The user may not know anything about the internals of the `root` function. So the error message would be confusing. The user only knows about `root`, but the error was in **square-root**.

Do not get the **catch** attribute mixed up with the **catch** function. Although they are similar, the **catch** function can be applied to any block that is evaluated.

The **throw** attribute allows you to write your own control functions, such as **for**, **foreach**, **if**, **loop**, and**forever**, by allowing your functions to pass the **return** and **exit** operations. For example, this loop function:

```
loop-time: func [time block] [
    while [now/time < time] block
]

```

evaluates a block until a specific time has been reached or passed. This loop can then be used within a function:

```
do-job: func [job][
    loop-time 10:30 [
        if error? try [page: read http://www.rebol.com]
            [return none]
    ]
    page
]

```

Now, what happens when the `[return` none] block is evaluated? Because this block is evaluated by the `loop-time` function, the return occurs in that function, not in `do-job`.

This can be prevented with the **throw** attribute:

```
loop-time: func [[throw] time block] [
    while [now/time < time] block
]

```

The **throw** attribute causes a **return** or **exit** that has occurred within the block to be thrown up to the previous level, which is the next function causing `do-job` to return.

## 8. Forward References

Sometimes a script needs to refer to a function before it has been defined. This can be done as long as the variable for the function is not evaluated before it is defined.

```
buy: func [item] [
    append own item
    sell head item   ; appears before it is defined
]

sell: func [item] [
    remove find own item
]

```

## 9. Scope of Variables

The context of variables is called their `scope`. The broad scope of variables is that of global and local. REBOL uses a form of static scoping, which is called `definitional` scoping. The scope of a variable is determined when its context is defined. In the case of a function, it is determined by when the function is defined.

All of the local variables defined within a function are scoped relative to that function. Nested functions and objects are able to access their parent's words.

```
a-func: func [a] [
    print ["a:" a]
    b-func: func [b] [
        print ["b:" b]
        print ["a:" a]
        print a + b
    ]
    b-func 10
]
a-func 11
a: 11
b: 10
a: 11
21

```

Note here that the `b-func` has access to the `a-func` variable.

Words that are bound outside of a function maintain those bindings even when evaluated within a function. This is the result of static scoping, and it allows you to write your own block evaluation functions (like **if**, **while**, **loop** ).

For example, here is a signed **if** function that evaluates one of three blocks based on the sign of a conditional value:

```
ifs: func [
    "If positive do block 1, zero do block 2, minus do 3"
    condition block1 block2 block3
][
    if positive? condition [return do block1]
    if negative? condition [return do block3]
    return do block2
]

print ifs 12:00 - now/time ["morning"]["noon"]["night"]
night

```

The blocks passed may contain the same words used within the `ifs` function without interfering with the words defined local to the function. This is because the words passed to the function are not bound to the function.

The next example passes the words `block1`, `block2` and `block3` to `ifs` as pre-defined words. The `ifs` function does not get confused between the words passed as arguments and the words of the same name defined locally:

```
block1: "morning right now"
block2: "just turned noon"
block3: "evening time"

print ifs (12:00 - now/time) [block1][block2][block3]
evening time

```

## 10. Reflective Properties

The specification of all functions can be obtained and manipulated during run-time. For example, you can print the specification block for a function with:

```
probe third :if
[
    "If condition is TRUE, evaluates the block."
    condition
    then-block [block!]
    /else "If not true, evaluate this block"
    else-block [block!]
]

```

The body code of functions can be obtained with:

```
probe second :append
[
    head either only [
        insert/only tail series :value
    ][
        insert tail series :value
    ]
]

```

Functions can be dynamically queried during evaluation. This is how the **help** and **source** functions work and how errors messages are formatted.

In addition, this feature is useful for creating your own unique versions of existing functions. For example, a user-defined print function can be created that has exactly the same specification as **print**, but sends its output to a string rather than the display:

```
output: make string! 1000

print-str: func third :print [
    repend output [reform :value newline]
]

```

The name of the argument used for print-str is obtained from the interface specification for print. You can examine that specification with:

```
probe third :print
[
    "Outputs a value followed by a line break."
    value "The value to print"
]

```

## 11. Online Function Help

Useful information about all functions of the system can be retrieved with the **help** function:

```
help send
USAGE:
    SEND address message /only /header header-obj
DESCRIPTION:
     Send a message to an address (or block of addresses)
     SEND is a function value.
ARGUMENTS:
     address -- An address or block of addresses (Type: email block)
     message -- Text of message. First line is subject. (Type: any)
REFINEMENTS:
     /only -- Send only one message to multiple addresses
     /header -- Supply your own custom header
         header-obj -- The header to use (Type: object)

```

All of this information comes from the definition of the function. Help can be obtained for all types of functions, not just natives or built-in functions. The help function can also be used for user-defined functions. The documentation that is displayed about a function is provided when the function is defined.

You can also search for help on functions that contain various patterns. For instance, at the command prompt, you could type

```
Help "path"
Found these words:
     clean-path     (function)
     lit-path!      (datatype)
     lit-path?      (action)
     path!          (datatype)
     path-thru      (function)
     path?          (action)
     set-path!      (datatype)
     set-path?      (action)
     split-path     (function)
     to-lit-path    (function)
     to-path        (function)
     to-set-path    (function)

```

to display all the words that contain the string `path`.

To view a list of all functions available in REBOL, type **what** at the command prompt.

```
what
* [value1 value2]
** [number exponent]
+ [value1 value2]
- [value1 value2]
/ [value1 value2]
// [value1 value2]
< [value1 value2]
<= [value1 value2]
<> [value1 value2]
= [value1 value2]
== [value1 value2]
=? [value1 value2]
> [value1 value2]
>= [value1 value2]
? ['word]
?? ['name]
about []
abs [value]
absolute [value]
...

```

## 12. Viewing Source Code

Another technique for learning about REBOL and for saving time in writing your own function is to look at how many of the REBOL mezzanine functions are defined. You can use the **source** function to do this.

```
source source
source: func [
    "Prints the source code for a word."
    'word [word!]
][
    prin join word ": "
    if not value? word [print "undefined" exit]
    either any [native? get word op? get word action? get word] [
        print ["native" mold third get word]
    ] [print mold get word]
]

```

Here the **source** function is used to print its own source code.

Note that you cannot see the source code for native functions because they exist only as machine code. However, the source function will display the native function interface specification. For example:

```
source add
add: native [
    "Returns the result of adding two values."
    value1 [number! pair! char! money! date! time! tuple!]
    value2 [number! pair! char! money! date! time! tuple!]
]
```