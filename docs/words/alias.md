# Alias - Function Summary

## Summary:

Creates an alternate spelling for a word.

## Usage:

**alias word name**

## Arguments:

**word** - Word to alias (must be: word)

**name** - Name of alias (must be: string)

## Description:

Create an alias for a word. The alias will be identical in every respect to the aliased word (symbol comparison and value referencing). Be careful not to confuse alias with setting another word to the same value. The alias cannot be set if the word already appears anywhere within the script or has been used in any way prior to being aliased.

```
alias 'print "stampa"
do {stampa "MONDO Rebol"}
MONDO Rebol
```

## Related:

[**get**](http://www.rebol.com/docs/words/wget.html) - Gets the value of a word.
[**set**](http://www.rebol.com/docs/words/wset.html) - Sets a word or block of words to specified value(s).