# Bind - Function Summary

## Summary:

Binds words to a specified context.

## Usage:

**bind words known-word**

## Arguments:

**words** - A block of words or single word. (must be: block any-word)

**known-word** - A reference to the target context. (must be: any-word object port)

## Refinements:

**/copy** - Deep copies block before binding it.

## Description:

Binds meaning to words in a block. That is, it gives words a context in which they can be interpreted. This allows blocks to be exchanged between different contexts, which permits their words to be understood. For instance a function may want to treat words in a global database as being local to that function.

The second argument to BIND is a word from the context in which the block is to be bound. Normally, this is a word from the local context (e.g. one of the function arguments), but it can be a word from any context within the system.

BIND will modify the block it is given. To avoid that, use the /COPY refinement. It will create a new block that is returned as the result.

```
words: [a b c]
fun: func [a b c][print bind words 'a]
fun 1 2 3
fun "hi" "there" "fred"
1 2 3
hi there fred
```

```
words: [a b c]
object: make object! [
  a: 1
  b: 2
  c: 3
  prove: func [] [print bind words 'a]
]
object/prove
1 2 3
```

```
settings: [start + duration]
schedule: function [start] [duration] [
  duration: 1:00
  do bind settings 'start
]
print schedule 10:30
11:30
```

## Related:

[**do**](http://www.rebol.com/docs/words/wdo.html) - Evaluates a block, file, URL, function, word, or any other value.
[**does**](http://www.rebol.com/docs/words/wdoes.html) - A shortcut to define a function that has no arguments or locals.
[**func**](http://www.rebol.com/docs/words/wfunc.html) - Defines a user function with given spec and body.
[**function**](http://www.rebol.com/docs/words/wfunction.html) - Defines a user function with local words.
[**make**](http://www.rebol.com/docs/words/wmake.html) - Constructs and returns a new value.
[**use**](http://www.rebol.com/docs/words/wuse.html) - Defines words local to a block.