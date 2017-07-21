# Block Series

## Contents:

- [1. Blocks of Blocks](#section-1)
- [2. Paths for Nested Blocks](#section-2)
- [3. Arrays](#section-3)
  - [3.1 Creating Arrays](#section-3.1)
  - [3.2 Initial Values](#section-3.2)
- [4. Composing Blocks](#section-4)

## 1. Blocks of Blocks

When a block appears as a value within another block, it counts as a single value regardless of how many values it contains. For example:

```
values: [
    "new" [1 2]
    %file1.txt ["one" ["two" %file2.txt]]
]
probe values
["new" [1 2] %file1.txt ["one" ["two" %file2.txt]]]

```

The **length?** of `values` is four. The second and fourth values are counted as single values:

```
print length? values
4

```

The block values within the `values` block can be used as a block as well. In the following examples, **second** is used to extract the second value from `values`.

To print the block, type:

```
probe second values
[1 2]

```

To get the length of the block, type:

```
print length? second values
2

```

To print the data type of the block, type:

```
print type? second values
block

```

In the same way, series operations can be performed on other types of series values in blocks. In the following examples, **pick** is used to extract `%file1`.`txt` from `values`.

To look at the value, type:

```
probe pick values 3
%file1.txt

```

To get the length of the value:

```
print length? pick values 3
9

```

to see the data type of the value:

```
print type? pick values 3
file

```

## 2. Paths for Nested Blocks

The path notation is useful for nested blocks.

The fourth value in `values` is a block containing another block. The following examples use a path to get information about this value.

To look at nested values, type:

```
probe values/4
["one" ["two" %file2.txt]]
probe values/4/2
["two" %file2.txt]

```

To get the lengths of nested values, type:

```
print length? values/4
2
print length? values/4/2
2

```

To see what the data type of a nested value, type:

```
print type? values/4
block
print type? values/4/2
block

```

The two series values in the fourth value's block can also be accessed.

To look at the values, type:

```
probe values/4/2/1
two
probe values/4/2/2
%file2.txt

```

To get the lengths of the values:

```
print length? values/4/2/1
3
print length? values/4/2/2
9

```

To see what data type the values are:

```
print type? values/4/2/1
string
print type? values/4/2/2
file

```

To modify the values:

```
change (next values/4/2/1) "o"
probe values/4/2/1
too
change/part (next find values/4/2/2 ".") "r" 3
probe values/4/2/2
%file2.r

```

The above examples illustrate REBOL's ability to operate on values nested inside blocks. Note that in the last series of examples, **change** is used to modify a string and file series three layers deep in `values`. Printing out the values block produces:

```
probe values
["new" [1 2] %file1.txt ["one" ["too" %file2.r]]]

```

## 3. Arrays

Blocks are used for arrays.

An example of a statically defined two dimensional array is:

```
arr: [
    [1   2   3  ]
    [a   b   c  ]
    [$10 $20 $30]
]

```

You can obtain the values of an array with the series extraction functions:

```
probe first arr
[1 2 3]
probe pick arr 3
[$10.00 $20.00 $30.00]
probe first first arr
1

```

You can also use paths to obtain values from the array:

```
probe arr/1
[1 2 3]
probe arr/3
[$10.00 $20.00 $30.00]
probe arr/3/2
$20.00

```

Paths can also be used to change the values in an array:

```
arr/1/2: 20

```

probe arr/1 == [1 20 3]

```
arr/3/2: arr/3/1 + arr/3/3

```

probe arr/3/2 == $40.00

### 3.1 Creating Arrays

The **array** function creates arrays dynamically. The function takes an argument that is either an integer or a block of integers and returns a block that is the array. By default, the cells of an array are initialized to `none`. To initialize array cells to some other value, use the /initial refinement explained in the next section.

When array is supplied with a single integer, a one-dimensional array of that size is returned:

```
arr: array 5
probe arr
[none none none none none]

```

When a block of integers is provided, the array has multiple dimensions. Each integer provides the size of the corresponding dimension.

Here is an example of a two dimensional array that has six cells, two rows of three columns:

```
arr: array [2 3]
probe arr
[[none none none] [none none none]]

```

This can be made into a three dimensional array by adding another integer to the block:

```
arr: array [2 3 2]
foreach lst arr [probe lst]
[[none none] [none none] [none none]]
[[none none] [none none] [none none]]

```

The block of integers that is passed to **array** can be as big as your memory will support.

### 3.2 Initial Values

To initialize the cells of an array to a value other than `none`, use the **/initial** refinement. This refinement takes one argument: the initial value. Here are some examples:

```
arr: array/initial 5 0
probe arr
[0 0 0 0 0]
arr: array/initial [2 3] 0
probe arr
[[0 0 0] [0 0 0]]
arr: array/initial 3 "a"
probe arr
["a" "a" "a"]
arr: array/initial [3 2] 'word
probe arr
[[word word] [word word] [word word]]
arr: array/initial [3 2 1] 11:11
probe arr
[[[11:11] [11:11]] [[11:11] [11:11]] [[11:11] [11:11]]]

```

## 4. Composing Blocks

The **compose** function is handy for creating blocks from dynamic values. It can be used for creating both data and code.

The **compose** function takes a block as an argument and returns a block that has each value in the argument block. Values in parentheses are evaluated before the block is returned. For example:

```
probe compose [1 2 (3 + 4)]
[1 2 7]
probe compose ["The time is" (now/time)]
["The time is" 10:32:45]

```

If the values in parentheses return a block, that block's individual values are used:

```
probe compose [a b ([c d])]
[a b c d]

```

To prevent this, you need to enclose the result in an extra block:

```
probe compose [a b ([[c d]])]
[a b [c d]]

```

An empty block inserts nothing:

```
probe compose [a b ([]) c d]
[a b c d]
```

When compose is given a block that contains sub-blocks, the sub-blocks are not evaluated, even if they contain parentheses:

```
probe compose [a b [c (d e)]]
[a b [c (d e)]]

```

If you would like the sub-blocks to be evaluated, use the **/deep** refinement. The **/deep** refinement causes all parentheses to be evaluated, regardless of where they are:

```
probe compose/deep [a b [c (d e)]]
[a b [c d e]]
```