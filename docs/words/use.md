# Use - Function Summary

## Summary:

Defines words local to a block.

## Usage:

**use words body**

## Arguments:

**words** - Local word(s) to the block (must be: block word)

**body** - Block to evaluate (must be: block)

## Description:

The first block contains a list of words which will be local to the second block. The second block will be evaluated and its results returned from the USE.

```
total: 1234
nums: [123 321 456]
use [total] [
	total: 0
    foreach n nums [total: total + n]
    print total
]
900
print total
1234
```

