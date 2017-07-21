# Wait - Function Summary

## Summary:

Waits for a duration, port, or both.

## Usage:

**wait value**

## Arguments:

**value** - The value argument. (must be: number time port block none)

## Refinements:

**/all** - Returns all events in a block

## Description:

If the value is a TIME, delay for that period. If the value is a DATE/TIME, wait until that DATE/TIME. If the value is an INTEGER or DECIMAL, wait that number of seconds. If the value is a PORT, wait for an event from that port. If a block is specified, wait for any of the times or ports to occur. Return the port that caused the wait to complete or return NONE if the timeout occurred.

```
print now/time
1:00:38
```

```
wait 1
print now/time
1:00:39
wait 0:00:01
print now/time
1:00:40
```