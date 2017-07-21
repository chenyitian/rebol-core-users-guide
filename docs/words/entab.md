# Entab - Function Summary

## Summary:

Converts spaces in a string to tabs. (tab size 4)

## Usage:

**entab string**

## Arguments:

**string** - The string argument. (must be: any-string)

## Refinements:

**/size** - Specifies the number of spaces per tab.

**number** - The number argument. (must be: integer)

## Description:

The REBOL language default tab-size is four spaces. Use the /SIZE refinement for other sizes such as eight. ENTAB will only place tabs at the beginning of the line (prior to the first non-space character).

The series passed to this function is modified as a result.

```
text: {
	no
	tabs
	in
	this
	sentence
} 
remove head remove back tail text
probe text
{	no
	tabs
	in
	this
	sentence
}
```

```
probe entab copy text
{^-^-no
^-^-tabs
^-^-in
^-^-this
^-^-sentence
}
```

```
print entab copy text
		no
		tabs
		in
		this
		sentence
```

```
probe entab/size copy text 2
{^-^-^-^-no
^-^-^-^-tabs
^-^-^-^-in
^-^-^-^-this
^-^-^-^-sentence
^-}
```

```
print entab/size copy text 2
				no
				tabs
				in
				this
				sentence
```

The opposite function is DETAB which converts tabs back to spaces:

```
probe entab text
{^-^-no
^-^-tabs
^-^-in
^-^-this
^-^-sentence
}
```

```
probe detab text
{	no
	tabs
	in
	this
	sentence
}
```

## Related:

[**detab**](http://www.rebol.com/docs/words/wdetab.html) - Converts tabs in a string to spaces. (tab size 4)