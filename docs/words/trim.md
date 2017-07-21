# Trim - Function Summary

## Summary:

Removes whitespace from a string. Default removes from head and tail.

## Usage:

**trim series**

## Arguments:

**series** - The series argument. (must be: series port)

## Refinements:

**/head** - Removes only from the head.

**/tail** - Removes only from the tail.

**/auto** - Auto indents lines relative to first line.

**/lines** - Removes all line breaks and extra spaces.

**/all** - Removes all whitespace.

**/with** - The with refinement.

**str** - Same as /all, but removes characters in 'str'. (must be: char string)

## Description:

The default for TRIM is to remove whitespace characters (tabs and spaces) from the heads and tails of every line of a string.

```
str: "  string   "
probe trim str
"string"
```

When a string includes multiple lines, the head and tail whitespace will be trimmed from each line (but not within the line):

```
str: {
	Now is the winter
	of our discontent
	made glorious summer
	by this sun of York.
}
probe trim str
{Now is the winter
of our discontent
made glorious summer
by this sun of York.
}
```

The final line terminator is preserved.

Note that TRIM modifies the string in the process.

```
str: "  string   "
trim str
probe str
"string"
```

TRIM does not copy the string. If that's what you want, then use TRIM with COPY to copy the string before trimming it.

Several refinements to TRIM are available. To trim just the head and/or tail of a string you can use the /HEAD or /TAIL refinements.

```
probe trim/head "  string  "
"string  "
```

```
probe trim/tail "  string  "
"  string"
```

```
probe trim/head/tail "  string  "
"string"
```

When using /HEAD or /TAIL, multiple lines are not affected:

```
probe trim/head {  line 1
	line 2
	line 3
}
{line 1
	line 2
	line 3
}
```

To trim just the head and tail of a multiline string, but none of its internal spacing:

```
str: {  line 1
	line 2
		line 3
			line 4
				line 5  }
probe trim/head/tail str
{line 1
	line 2
		line 3
			line 4
				line 5}
```

If you use TRIM/LINES then all lines and extra spaces will be removed from the text. This is useful for word wrapping and web page kinds of applications.

```
str: {
	Now   is
	the
	winter
}
probe trim/lines str
"Now is the winter"
```

You can also remove /ALL space:

```
probe trim/all " Now is   the winter "
"Nowisthewinter"
```

```
str: {
	Now   is
	the
	winter
}
probe trim/all str
"Nowisthewinter"
```

One of the most useful TRIM refinements is /AUTO which will do a "smart" trim of the indentation of text lines. This mode detects the indentation from the first line and preserves indentation for the lines to follow:

```
probe trim/auto {
	line 1
		line 2
		line 3
			line 4
	line 5
}
{line 1
	line 2
	line 3
		line 4
	line 5
}
```

This is useful for sections of text that are embedded within code and indented to the level of the code.

To trim other characters, the /WITH refinement is provided. It takes an additional string that specifies what characters to be removed.

```
str: {This- is- a- line.}
probe trim/with str "-"
"This is a line."
```

```
str: {This- is- a- line.}
probe trim/with str "- ."
"Thisisaline"
```

## Related:

[**clear**](http://www.rebol.com/docs/words/wclear.html) - Removes all values from the current index to the tail. Returns at tail.
[**parse**](http://www.rebol.com/docs/words/wparse.html) - Parses a series according to rules.
[**remove**](http://www.rebol.com/docs/words/wremove.html) - Removes value(s) from a series and returns after the remove.