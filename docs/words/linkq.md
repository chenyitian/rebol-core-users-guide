# Link? - Function Summary

## Summary:

Returns true if REBOL/Link capability is enabled.

## Usage:

**link?**

## Description:

Returns TRUE if you are running an IOS-client enabled version of REBOL.

```
print link?
false
```

Note that this function may not be available in older versions of REBOL. To define a similar value add this to your code:

```
link?: value? 'send-server
```