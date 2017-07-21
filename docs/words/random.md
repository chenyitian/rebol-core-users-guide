# Random - Function Summary

## Summary:

Returns a random value of the same datatype.

## Usage:

**random value**

## Arguments:

**value** - Maximum value of result

## Refinements:

**/seed** - Restart or randomize

**/secure** - Returns a cryptographically secure random number.

**/only** - Return single value from series.

## Description:

The value passed can be used to restrict the range of the random result. For integers random begins at one, not zero, and is inclusive of the value given. (This conforms to the indexing style used for all series datatypes, allowing random to be used directly with functions like PICK.)

```
loop 4 [print random 10]
6
7
2
3
```

```
lunch: ["Italian" "French" "Japanese" "American"]
print pick lunch random 4
American
```

```
loop 3 [print random true]
true
false
false
```

```
loop 5 [print random 1:00:00]
0:57:12
0:16:07
0:38:50
0:00:57
0:43:06
```

To initialize the random number generator to a random state, you can seed it with a value (to repeat the sequence) or the current time to start a unique seed.

```
random/seed 123
```

```
random/seed now
```

That last line is a good example to provide a fairly random starting value for the random number generator.

RANDOM can also be used on all series datatypes:

```
print random "abcdef"
dafebc
```

```
print random [1 2 3 4 5]
4 3 1 2 5
```

It will return a series that contains the same number of elements. To cut it down, you can use CLEAR:

```
key: random "abcdefghijklmnopqrstuv0123456789"
clear skip key 6
print key
6gemlf
```

Here's an example password generator. Add more partial words to get more variations:

```
syls: ["ca" "ru" "lo" "ek" "-" "." "!"]
print rejoin random syls
.-caloekru!
```

## Related:

[**now**](http://www.rebol.com/docs/words/wnow.html) - Returns the current local date and time.