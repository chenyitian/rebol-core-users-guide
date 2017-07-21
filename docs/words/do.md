# Do - Function Summary

## Summary:

Evaluates a block, file, URL, function, word, or any other value.

## Usage:

**do value**

## Arguments:

**value** - Normally a file name, URL, or block

## Refinements:

**/args** - If value is a script, this will set its system/script/args

**arg** - Args passed to a script. Normally a string.

**/next** - Do next expression only. Return block with result and new position.

## Description:

Accepts a block, or LOADs a string, file, or URL into a block, then evaluates the expressions of the block. Files and URLs must have a valid REBOL header. Elements are evaluated left to right. When an element encountered is a function requiring arguments, the function's arguments are first evaluated then passed to the function before it is evaluated. The value of final evaluation is returned.

The /ARGS refinement allows you to pass arguments to another script and is used with a file, or URL. Arguments passed with /ARGS are stored in system/script/args within the context of the loaded script.

The /NEXT refinement returns a block consisting of two elements. The first element is the evaluated return of the first expression encountered. The second element is the original block with the current index placed after the last evaluated expression.

```
print do [1 + 2]
3
```

```
print do "1 + 2"
3
```

```
do "repeat n 3 [print n]"
1
2
3
```

```
do [print "doing"]
doing
```

```
blk: [
	[print "test"]
	[loop 3 [print "loop"]]
]
do second blk
loop
loop
loop
```

```
do first blk
test
```

```
blk: [
	[1 + 2]
	[3 * 4]
	[6 / 3]
]
while [not empty? blk][
	set [value blk] do/next blk
	print value
]
3
12
2
```

## Related:

[**load**](http://www.rebol.com/docs/words/wload.html) - Loads a file, URL, or string. Binds words to global context.
[**loop**](http://www.rebol.com/docs/words/wloop.html) - Evaluates a block a specified number of times.
[**reduce**](http://www.rebol.com/docs/words/wreduce.html) - Evaluates an expression or block expressions and returns the result.
[**repeat**](http://www.rebol.com/docs/words/wrepeat.html) - Evaluates a block a number of times or over a series.