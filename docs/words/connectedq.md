# Connected? - Function Summary

## Summary:

Returns TRUE when connected to the Internet.

## Usage:

**connected?**

## Description:

This function returns true if connected over the network. Note, however, that this function differs between REBOL View and Link, and it may not be a clear indicator of a true connection to the Internet.

In View, this function returns TRUE if the Internet interface is available. This does not mean that the computer is actually connected to the Internet, because that can only be determined by actually connecting to another computer, such as a web server. For example, the function may return true, but your computer may have lost its Internet connection because your modem hung-up or local network went down.

```
print connected?
true
```

A way to actually check for an Internet connection is to try to open a port to an known server. For example, this code will return TRUE if an Internet connection can be made:

```
print not error? try [close open tcp://hq.rebol.net:80]
true
```

Note, however, that if the rebol.com site is not available or unreachable, this line of code will return FALSE.

In REBOL/Link, the connected? function will return TRUE if the Link client is currently connected to the IOS server. Note however that the script must include the Link-app header type, and be launched from within the Link environment.