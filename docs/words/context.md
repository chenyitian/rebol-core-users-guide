# Context - Function Summary

## Summary:

Defines a unique (underived) object.

## Usage:

**context blk**

## Arguments:

**blk** - Object variables and values. (must be: block)

## Description:

This function creates a unique new object. It is just a shortcut for MAKE OBJECT!.

```
person: context [
  name: "Fred"
  age: 24
  birthday: 20-Jan-1986
  language: "REBOL"
]
probe person

make object! [
  name: "Fred"
  age: 24
  birthday: 20-Jan-1986
  language: "REBOL"
]
```

```
person2: make person [
  name "Bob"
]
probe person2

make object! [
  name: "Fred"
  age: 24
  birthday: 20-Jan-1986
  language: "REBOL"
]
```

## Related:

[**make**](http://www.rebol.com/docs/words/wmake.html) - Constructs and returns a new value.