# Dispatch - Function Summary

## Summary:

Wait for a block of ports. As events happen, dispatch port handler blocks.

## Usage:

**dispatch port-block**

## Arguments:

**port-block** - Block of port handler pairs (port can be timeout too). (must be: block)

## Description:

The DISPATCH function helps you setup complex WAIT situations that involve multiple ports (for example, multiple Internet connections).

The argument passed to DISPATCH is a block that contains ports and actions for those ports. The port value can be a port datatype or a timeout value (the number of seconds as an integer or decimal, or a time datatype for hours, minutes, and seconds).

The dispatch function then proceeds to wait for the ports provided, or the timeout if provided. As ports signal their changes, each port is processed according to the action block provided. If a timeout occurs, its action block is processed.

```
port-block: [
    tcp-port1 [print "port1 woke up"]
    tcp-port2 [do port2-wakeup-call]
    tcp-port3 [handle-port3]
    tcp-port4 [if do-port4 ['break]]
    0:01:00   [do-periodic-processing]
]
dispatch port-block
```

Normally, the DISPATCH function will wait forever, processing the ports and timeouts that have been specified. However, if a port action block returns the word BREAK, the DISPATCH function is terminated and will exit.

Only a single timeout can be specified. If multiple timeouts values are specified, only the first one is used.

Note: The WAIT awake function callbacks provide a useful alternative to using DISPATCH, and they work well with GUI code. The WAIT awake functions are callback functions that are evaluted directly by the WAIT function when it awakes. A special system queue keeps the list of awake functions.

## Related:

[**wait**](http://www.rebol.com/docs/words/wwait.html) - Waits for a duration, port, or both.