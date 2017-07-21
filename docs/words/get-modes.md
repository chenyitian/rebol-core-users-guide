# Get-modes - Function Summary

## Summary:

Returns mode settings for a port.

## Usage:

**get-modes target modes**

## Arguments:

**target** - The target argument. (must be: file url block port)

**modes** - The modes argument. (must be: word block)

## Description:

This function returns a block of special modes for file and network ports. GET-MODES takes a port and a block of modes that are being requested. It returns a block of mode names and their values (which can in turn be passed back to SET-MODES).

```
port: open/binary %test-file
probe get-modes port [direct binary]
[direct: false binary: true]
```

The example above shows that the port is opened for binary access but not for direct access.

A shortcut to query a single mode is to specify a single mode word as the argument:

```
probe get-modes port 'binary
true
```

In this case GET-MODES only returns the value directly, rather than a block.

Another form of GET-MODES takes a name-value block that is of the same format as SET-MODES.

```
probe get-modes port [direct: none binary: none]
[direct: false binary: true]
```

Here the values specified are ignored.

GET-MODES supports a few special modes which return a list of applicable modes for a port. They are: file-modes, copy-modes, network-modes, and port-modes. If any of these modes are specified in a GET-MODES request then the response contains a block of matching modes which are available on the current operating system (and it may vary between systems).

```
probe get-modes port 'file-modes
[creation-date access-date modification-date owner-write archived hidden system]
```

You can actually use the returned value to get the values of all available modes:

```
modes: get-modes port 'file-modes
probe get-modes port modes
[creation-date: 8-Mar-2004/23:35:40-8:00 access-date: 8-Mar-2004/0:00-8:00 modification-date: 8-Mar-2004/23:35:42-8:00 owner-write: true archived: true hidden: false system: false]
```

Be sure to close the port when you have completed your queries and changes:

```
close port
```

The complete list of all modes includes (note that not all modes are supported by all operating systems. See REBOL 2.5 addendum for more information):

```
file-modes: [
	status-change-date
	modification-date
	access-date
	backup-date
	creation-date
	owner-name
	group-name
	owner-id
	group-id
	owner-read
	owner-write
	owner-delete
	owner-execute
	group-read
	group-write
	group-delete
	group-execute
	world-read
	world-write
	world-delete
	world-execute
	comment
	script
	archived
	system
	hidden
	hold
	pure
	type
	creator
]
```

```
Port-modes: [
	read
	write
	binary
	lines
	no-wait
	direct
]
```

```
Network-modes: [
	broadcast
	multicast-groups
	type-of-service
	keep-alive
	receive-buffer-size
	send-buffer-size
	multicast-interface
	multicast-ttl
	multicast-loopback
	no-delay
	interfaces
]
```

For example, to obtain a list of network interfaces for your computer system:

```
port: open tcp://:10000
probe get-modes port 'interfaces
close port
[
	make object! [
		name: "if16777219"
		addr: 10.10.10.95
		netmask: 255.255.255.0
		broadcast: 10.10.10.255
		dest-addr: none
		flags: [broadcast multicast]
	] 
	make object! [
		name: "lo0"
		addr: 127.0.0.1
		netmask: 255.0.0.0
		broadcast: none
		dest-addr: none
		flags: [multicast loopback]
	]]
```

See the REBOL/Core Addendum for a complete description of GET-MODES and SET-MODES.

## Related:

[**open**](http://www.rebol.com/docs/words/wopen.html) - Opens a new port connection.
[**read**](http://www.rebol.com/docs/words/wread.html) - Reads from a file, url, or port-spec (block or object).
[**set-modes**](http://www.rebol.com/docs/words/wset-modes.html) - Changes mode settings for a port.
[**write**](http://www.rebol.com/docs/words/wwrite.html) - Writes to a file, url, or port-spec (block or object).