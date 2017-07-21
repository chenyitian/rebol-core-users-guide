# Math

## Contents:

- [1. Overview](#section-1)
- [2. Scalar Data Types](#section-2)
- [3. Evaluation Order](#section-3)
- [4. Standard Functions and Operators](#section-4)
  - [4.1 absolute](#section-4.1)
  - [4.2 add](#section-4.2)
  - [4.3 complement](#section-4.3)
  - [4.4 divide](#section-4.4)
  - [4.5 multiply](#section-4.5)
  - [4.6 negate](#section-4.6)
  - [4.7 random](#section-4.7)
  - [4.8 remainder](#section-4.8)
  - [4.9 subtract](#section-4.9)
- [5. Type Conversion](#section-5)
- [6. Comparison Functions](#section-6)
  - [6.1 equal](#section-6.1)
  - [6.2 greater](#section-6.2)
  - [6.3 greater-or-equal](#section-6.3)
  - [6.4 lesser](#section-6.4)
  - [6.5 lesser-or-equal](#section-6.5)
  - [6.6 not equal to](#section-6.6)
  - [6.7 same](#section-6.7)
  - [6.8 strict-equal](#section-6.8)
  - [6.9 strict-not-equal](#section-6.9)
- [7. Logarithmic Functions](#section-7)
  - [7.1 exp](#section-7.1)
  - [7.2 log-10](#section-7.2)
  - [7.3 log-2](#section-7.3)
  - [7.4 log-e](#section-7.4)
  - [7.5 power](#section-7.5)
  - [7.6 square-root](#section-7.6)
- [8. Trigonometric Functions](#section-8)
  - [8.1 arccosine](#section-8.1)
  - [8.2 arcsine](#section-8.2)
  - [8.3 arctangent](#section-8.3)
  - [8.4 cosine](#section-8.4)
  - [8.5 sine](#section-8.5)
  - [8.6 tangent](#section-8.6)
- [9. Logic Functions](#section-9)
  - [9.1 and](#section-9.1)
  - [9.2 or](#section-9.2)
  - [9.3 xor](#section-9.3)
  - [9.4 complement](#section-9.4)
  - [9.5 not](#section-9.5)
- [10. Errors](#section-10)
- [10.1 Attempt to divide by zero](#section-10.1)
- [10.2 Math or number overflow](#section-10.2)
- [10.3 Positive number required](#section-10.3)
- [10.4 Cannot use operator on datatype! value](#section-10.4)

## 1. Overview

REBOL provides a comprehensive set of mathematical and trigonometric operations. Many of these operators can handle multiple datatypes, including integer, decimal, money, tuple, time, and date. Some of these datatypes may even be mixed, or coerced.

## 2. Scalar Data Types

The mathematical functions of REBOL operate in a consistent manner over a wide range of scalar (numerical) data types. These data types include:

| Datatype     | Description                              |
| ------------ | ---------------------------------------- |
| **Integer!** | 32 bit numbers without decimal point     |
| **Decimal!** | 64 bit floating point numbers            |
| **Money!**   | currency with 64 bit floating point number |
| **Time!**    | hours, minutes, seconds, and sub-seconds |
| **Date!**    | day, month, year, time, time zone        |
| **Pair!**    | graphical position or size               |
| **Tuple!**   | versions, colors, network addresses      |

The following are a few examples that show a range of math operations over the scalar data types. Notice that operators produce useful results for each data type.

The **integer** and **decimal** data types:

```
print 2 + 1
3
print 2 - 1
1
print 2 * 10
20
print 20 / 10
2
print 21 // 10
1
print 2.2 + 1
3.2
print 2.2 - 1
1.2
print 2.2 * 10
22
print 2.2 / 10
0.22
print random 10
5

```

The **time** data type:

```
print 2:20 + 1:40
4:00
print 2:20 + 5
2:20:05
print 2:20 + 60
2:21
print 2:20 + 2.2
2:20:02.2
print 2:20 - 1:20
1:00
print 2:20 - 5
2:19:55
print 2:20 - 120
2:18
print 2:20 * 2
4:40
print 2:20 / 2
1:10
print 2:20:01 / 2
1:10:00.5
print 2:21 // 2
0:00
print - 2:20
-2:20
print random 10:00
5:30:52

```

The **date** data type:

```
print 1-Jan-2000 + 1
2-Jan-2000
print 1-Jan-2000 - 1
31-Dec-1999
print 1-Jan-2000 + 31
1-Feb-2000
print 1-Jan-2000 + 366
1-Jan-2001
birthday: 7-Dec-1944
print ["I've lived" (now/date - birthday) "days."]
I've lived 20305 days.
print random 1-1-2000
29-Apr-1695

```

The **money** data type:

```
print $2.20 + $1
$3.20
print $2.20 + 1
$3.20
print $2.20 + 1.1
$3.30
print $2.20 - $1
$1.20
print $2.20 * 3
$6.60
print $2.20 / 2
$1.10
print $2.20 / $1.10
2
print $2.21 // 2
$0.21
print random $10.00
$6.00

```

The **pair** data type:

```
print 100x200 + 10x20
110x220
print 10x10 + 3
13x13
print 10x20 * 2x4
20x80
print 100x100 * 3
300x300
print 100x30 / 10x3
10x10
print 100x30 / 10
10x3
print 101x32 // 10x3
1x2
print 101x32 // 10
1x2
print random 100x20
67x12

```

The **tuple** data type:

```
print 1.2.3 + 3.2.1
4.4.4
print 1.2.3 - 1.0.1
0.2.2
print 1.2.3 * 3
3.6.9
print 10.20.30 / 10
1.2.3
print 11.22.33 // 10
1.2.3
print 1.2.3 * 1.2.3
1.4.9
print 10.20.30 / 10.20.30
1.1.1
print 1.2.3 + 7
8.9.10
print 1.2.3 - 1
0.1.2
print random 10.20.30
8.18.12

```

## 3. Evaluation Order

There are two rules to remember when evaluating mathematical expressions:

- Expressions are evaluated from left to right.
- Operators take precedence over functions.

The evaluation of expressions from left to right is independent of the type of operator that is used. For example:

```
print 1 + 2 * 3
9

```

In the example above, notice that the result is not seven, as would be the case if multiplication took precedence over addition.

**Important Note**

The way mathematical expressions are evaluated from left to right regardless of the operator is different than many other computer languages. Many languages have rules of precedence that you must remember that determine the order of evaluation of operators. For example, a multiply is done before an add. Some languages have 10 or more such rules.

In REBOL, rather than requiring users to remember the precedence of operators, you only need to remember the left-to-right rule. More importantly, for advanced code such as expressions that handle expressions (in reflection, for example) you do not need to reorder terms based on precedence. The evaluation order is kept simple.

For most math expressions, the left-to-right evaluation rule works quite well and is easy to remember. However, because this rule is different from other languages, it can be a source of programming errors, so watch out.

The best solution is to check your work. You can also use parentheses if necessary to clarify your expression (see below), and you can always type your expression at the console to verify your result.

If you need to evaluate in some other order, reorder the expression or use parentheses:

```
print 2 * 3 + 1
7
print 1 + (2 * 3)
7

```

When functions are mixed with operators, the operators are evaluated first, then the functions:

```
print absolute -10 + 5
5

```

In the above example, the addition is performed first, and its result is provided to the **absolute** function.

In the next example:

```
print 10 + sine 30 + 60
11

```

the expression is evaluated in this order:

```
30 + 60 => 90
sine 90 => 1
10 + 1 => 11
print

```

To change the order such that the **sine** of 30 is done first, use parentheses:

```
print 10 + (sine 30) + 60
70.5

```

or reorder the expression:

```
print 10 + 60 + sine 30
70.5

```

## 4. Standard Functions and Operators

This section describes the standard math functions and operators used in REBOL.

### 4.1 absolute

The expressions:

```
absolute value

abs value

```

return the absolute value of `value`.

Works with **integer**, **decimal**, **money**, **time**, **pair** data types.

```
print absolute -10
10
print absolute -1.2
1.2
print absolute -$1.2
$1.20
print absolute -10:20
10:20
print absolute -10x-20
10x20

```

### 4.2 add

The expressions:

```
value1 + value2

add value1 value2

```

return the result of adding `value1` to `value2`.

Works with **integer**, **decimal**, **money**, **time**, **tuple**, **pair**, **date**, **char** data types.

```
print 1 + 2
3
print 1.2 + 3.4
4.6
print 1.2.3 + 3.4.5
4.6.8
print $1 + $2
$3.00
print 1:20 + 3:40
5:00
print 10x20 + 30x40
40x60
print #"A" + 10
K
print add 1 2
3

```

### 4.3 complement

The expression:

```
complement value

```

returns the numeric complement (bitwise complement) of a value.

Works with **integer**, **decimal**, **tuple** data types.

```
print complement 10
-11
print complement 10.5
-11
print complement 100.100.100
155.155.155

```

### 4.4 divide

The expressions:

```
value1 / value2

divide value1 value2

```

return the result of dividing `value1` by `value2`.

Works with **integer**, **decimal**, **money**, **time**, **tuple**, **pair**, **char** data types.

```
print 10 / 2
5
print 1.2 / 3
0.4
print 11.22.33 / 10
1.2.3
print $12.34 / 2
$6.17
print 1:20 / 2
0:40
print 10x20 / 2
5x10
print divide 10 2
5

```

### 4.5 multiply

The expressions:

```
value1 * value2

multiply value1 value2

```

return the result of multiplying `value1` by `value2`.

Works with **integer**, **decimal**, **money**, **time**, **tuple**, **pair**, **char** data types.

```
print 10 * 2
20
print 1.2 * 3.4
4.08
print 1.2.3 * 3.4.5
3.8.15
print $10 * 2
$20.00
print 1:20 * 3
4:00
print 10x20 * 3
30x60
print multiply 10 2
20

```

### 4.6 negate

The expressions:

```
- value

negate value

```

change the sign of the `value`.

Works with **integer**, **decimal**, **money**, **time**, **pair**, **char** data types.

```
<A name=_Toc487519923>print - 10
-10
print - 1.2
-1.2
print - $10
-$10.00
print - 1:20
-1:20
print - 10x20
-10x-20
print negate 10
-10

```

### 4.7 random

The expression:

```
random value

```

returns a random value that is less than or equal to value given.

Note that for integers **random** begins at 1, `not` 0, and is inclusive of the value given. This allows **random** to be used directly with functions like **pick**.

When a decimal is used the result is a decimal data type rounded to an integer.

The **/seed** refinement restarts the random generator. Use the **/seed** refinement with **random** first it if you want unique random number generation. You can use the current date and time to make the seed more random:

```
random/seed now

```

Works with **integer**, **decimal**, **money**, **time**, **tuple**, **pair**, **date**, **char**, **string**, **block** data types.

```
print random 10
5
print random 10.5
2
print random 100.100.100
79.95.66
print random $100
$32.00
print random 10:30
6:37:33
print random 10x20
2x4
print random 30-Jun-2000
27-Dec-1171

```

### 4.8 remainder

The expressions:

```
value1 // value2

remainder value1 value2

```

return the remainder of dividing `value1` by `value2`.

Works with **integer**, **decimal**, **money**, **time**, **tuple**, **pair** data types.

```
print 11 // 2
1
print 11.22.33 // 10
1.2.3
print 11x22 // 2
1x0
print remainder 11 2
1

```

### 4.9 subtract

The expressions:

```
value1 - value2

subtract value1 value2

```

return the result of subtracting `value2` from `value1`.

Works with **integer**, **decimal**, **money**, **time**, **tuple**, **pair**, **date**, **char** data types.

```
print 2 - 1
1
print 3.4 - 1.2
2.2
print 3.4.5 - 1.2.3
2.2.2
print $2 - $1
$1.00
print 3:40 - 1:20
2:20
print 30x40 - 10x20
20x20
print #"Z" - 1
Y
print subtract 2 1
1

```

## 5. Type Conversion

When math operations are performed between data types, normally the non-integer or non-decimal data type is returned. When integers are combined with decimals, a decimal data type is returned.

## 6. Comparison Functions

All comparison functions return either `true` or `false`.

### 6.1 equal

The expressions:

```
value1 = value2

equal? value1 value2

```

return `true` if the first and second values are equal.

Works with **integer**, **decimal**, **money**, **time**, **date**, **tuple**, **char** and **series** data types.

```
print 11-11-99 = 11-11-99
true
print equal? 111.112.111.111 111.112.111.111
true
print #"B" = #"B"
true
print equal? "a b c d" "A B C D"
true

```

### 6.2 greater

The expressions:

```
value1 > value2

greater? value1 value2

```

return `true` if the first value is greater than the second value.

Works with **integer**, **decimal**, **money**, **time**, **date**, **tuple**, **char** and **series** data types.

```
print 13-11-99 > 12-11-99
true
print greater? 113.111.111.111 111.112.111.111
true
print #"C" > #"B"
true
print greater? [12 23 34] [12 23 33]
true

```

### 6.3 greater-or-equal

The expressions:

```
value1 >= value2

greater-or-equal? value1 value2

```

return `true` if the first value is greater than or equal to the second value.

Works with **integer**, **decimal**, **money**, **time**, **date**, **tuple**, **char** and **series** data types.

```
print 11-12-99 >= 11-11-99
true
print greater-or-equal? 111.112.111.111 111.111.111.111
true
print #"B" >= #"A"
true
print greater-or-equal? [b c d e] [a b c d]
true

```

### 6.4 lesser

The expressions:

```
value1 < value2

lesser? value1 value2

```

return `true` if the first value is less than second value.

Works with **integer**, **decimal**, **money**, **time**, **date**, **tuple**, **char** and **series** data types:

```
print 25 < 50
true
print lesser? 25.3 25.5
true
print $2.00 < $2.30
true
print lesser? 00:10:11 00:11:11
true

```

### 6.5 lesser-or-equal

The expressions:

```
value1 <= value2

lesser-or-equal? value1 value2

```

return `true` if the first value is less than or equal to the second value.

Works with **integer**, **decimal**, **money**, **time**, **date**, **tuple**, **char** and **series** data types.

```
print 25 <= 25
true
print lesser-or-equal? 25.3 25.5
true
print $2.29 <= $2.30
true
print lesser-or-equal? 11:11:10 11:11:11
true

```

### 6.6 not equal to

The expressions:

```
value1 <> value2

not-equal? value1 value2

```

return `true` if the first and second values are not equal.

Works with **integer**, **decimal**, **money**, **time**, **date**, **tuple**, **char** and **series** data types.

```
print 26 <> 25
true
print not-equal? 25.3 25.5
true
print $2.29 <> $2.30
true
print not-equal? 11:11:10 11:11:11
true

```

### 6.7 same

The expressions:

```
value1 =? value2

same? value1 value2

```

return `true` if two words refer to the same value. For instance, when you want to see if two words are referencing the same index in a series.

Work with all data types.

```
reference-one: "abcdef"
reference-two: reference-one
print same? reference-one reference-two
true
reference-one: next reference-one
print same? reference-one reference-two
false
reference-two: next reference-two
print same? reference-one reference-two
true
reference-two: copy reference-one
print same? reference-one reference-two
false

```

### 6.8 strict-equal

The expressions:

```
value1 == value2

strict-equal? value1 value2

```

return `true` if the first and second values are strictly the same. Can be used as a case-sensitive version of the **equal?** (**** = ) operator for strings and to differentiate between integers and decimals when their values are the same.

Works with all data types.

```
print strict-equal? "abc" "ABC"
false
print equal? "abc" "ABC"
true
print strict-equal? "abc" "abc"
true
print strict-equal? 1 1.0
false
print equal? 1 1.0
true
print strict-equal? 1.0 1.0
true

```

### 6.9 strict-not-equal

The expression:

```
strict-not-equal? value1 value2

```

returns `true` if the first and second values are strictly not the same. Can be used as a case-sensitive version of the **not-equal?** (**** <> ) operator for strings and to differentiate between integers and decimals when their values are the same.

Works with all data types.

```
print strict-not-equal? "abc" "ABC"
true
print not-equal? "abc" "ABC"
false
print strict-not-equal? "abc" "abc"
false
print strict-not-equal? 1 1.0
true
print not-equal? 1 1.0
false
print strict-not-equal? 1.0 1.0
false

```

## 7. Logarithmic Functions

### 7.1 exp

The expression:

```
exp value

```

raises E (natural number) to the power of `value`.

### 7.2 log-10

The expression:

```
log-10 value

```

returns the base-10 logarithm of `value`.

### 7.3 log-2

The expression:

```
log-2 value

```

returns the base-2 logarithm of `value`.

### 7.4 log-e

The expression:

```
log-e value

```

returns the base-E (natural number) log. of `value`.

### 7.5 power

The expressions:

```
value1 ** value2

power value1 value2

```

return the result of raising `value1` to `value2` power.

### 7.6 square-root

The expression:

```
square-root value

```

returns the square root of `value`.

## 8. Trigonometric Functions

The trigonometric functions deal in degrees. Use the **/radians** refinement with any of the trigonometric functions to operate in and return radians.

### 8.1 arccosine

The expression:

```
arccosine value

```

returns the trigonometric arccosine of `value`.

### 8.2 arcsine

The expression:

```
arcsine value

```

returns the trigonometric arcsine of `value`.

### 8.3 arctangent

The expression:

```
arctangent value

```

returns the trigonometric arctangent of `value`.

### 8.4 cosine

The expression:

```
cosine value

```

returns the trigonometric cosine of `value`.

### 8.5 sine

The expression:

```
sine value

```

returns the trigonometric sine of `value`.

### 8.6 tangent

The expression:

```
tangent value

```

returns the trigonometric tangent of `value`.

## 9. Logic Functions

Logic functions can be performed on logic values and on some scalar values including **integer**, **char**, **tuple**, and **bitset**. When working with logic values, the logic functions return boolean values. When working with other types of values, the logic functions on the bits.

### 9.1 and

The **and** function compares two logic values and returns `true` if they are both true**** :

```
print (1 < 2) and (2 < 3)
true
print (1 < 2) and (4 < 3)
false

```

When used with integers, the **and** function compares bit for bit and returns `1` if both bits are `1`, or `0` if neither bit is `1`:

```
print 3 and 5
1

```

### 9.2 or

The **or** function compares two logic values and returns `true` if either of them are true or `false` or if both are false****:

```
print (1 < 2) or (2 < 3)
true
print (1 < 2) or (4 < 3)
true
print (3 < 2) or (4 < 3)
false

```

When used with integers, **or** compares bit for bit and returns `1` if either bit is `1` or **0** if both bits are 0:

```
print 3 or 5
7

```

### 9.3 xor

The **xor** function compares two logic values and returns `true` if and only if one of the values is true and the other is false.

```
print (1 < 2) xor (2 < 3)
false
print (1 < 2) xor (4 < 3)
true
print (3 < 2) xor (4 < 3)
false

```

When used with integers, **xor** compares bit for bit and returns `1` if and only if one bit is `1` and the other `0` . Otherwise, it returns `0` :

```
print 3 xor 5
6

```

### 9.4 complement

The **complement** function returns the logic or bitwise complement of a value. It is used for bitmask integer numbers and inverting bitsets.

```
print complement true
false
print complement 3
-4

```

### 9.5 not

For a logic value **not** returns `true` if the value is false and `false` if the value is true. It does not perform numerical bitwise operations.

```
print not true
false
print not false
true

```

## 10. Errors

Math errors are reported when an illegal operation is performed or when an overflow or underflow occurs. The following errors may be encountered in math operations.

### 10.1 Attempt to divide by zero

An attempt was made to divide a number by 0.

```
1 / 0
** Math Error: Attempt to divide by zero
** Where: connect-to-link
** Near: 1 / 0

```

### 10.2 Math or number overflow

An attempt was made to process a number too large for REBOL to handle.

```
1E+300 + 1E+400
** Math Error: Math or number overflow
** Where: connect-to-link
** Near: 1 / 0

```

### 10.3 Positive number required

An attempt was made to process a negative number with a math operator that accepts only positive numbers.

```
log-10 -1
** Math Error: Positive number required
** Where: connect-to-link
** Near: log-10 -1

```

### 10.4 Cannot use operator on datatype! value

An attempt was made to process incompatible data types. The data type of the second argument in the operation is returned as listed.

```
10:30 + 1.2.3
** Script Error: Cannot use add on time! value
** Where: connect-to-link
** Near: 10:30 + 1.2.3
```