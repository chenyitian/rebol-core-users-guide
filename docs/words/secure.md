# Secure - Function Summary

## Summary:

Specifies security policies (access levels and directories). Return prior settings.

## Usage:

**secure level**

## Arguments:

**level** - Levels are: quit, throw, ask, allow. Query will return settings. (must be: word block)

## Description:

This function controls file and network access. It uses a dialect to specify security "sandboxes" that allow or deny access. You can set different security levels and multiple sandboxes for networking, files, and specific files and directories.

The argument to the SECURE function can be a word or a block. If you provide a word, a global security level is set for all accesses. If you provide a block, you can specify separate security for files, directories, and networking.

For example, if you write:

```
secure ask
```

the user will be prompted on all file and network accesses. But, if you provide a block as the argument:

```
secure [
	net quit
	file ask
	%./ allow
]
```

you will disable networking (will force a quit if attempted), but ask for user approval for all file access, except to the local directory (which will be allowed).

As you can see, the security dialect consists of a block of paired values. The first value in the pair specifies what is being secured (file or net), and the second value specifies the level of security (allow, ask, throw, quit). The second value can also be a block to further specify read and write security.

The security levels are:

ALLOW - removes all READ and/or WRITE restrictions.

ASK - restricts immediate READ and/or WRITE access and prompts the user for each access attempt, requiring approval before the operation may be completed.

THROW - denies READ and/or WRITE access, throwing an error when a restricted access attempt is made.

QUIT - denies READ and/or WRITE access and quits the script when restricted access is attempted.

For example, to allow all network access, but to quit on any file access:

```
secure [
	net allow ;allows any net access
	file quit ;any file access will cause the program to quit
]
```

If a block is used instead of a security level word, it can contain pairs of security levels and access types. This lets you specify a greater level of detail about the security you require. The access types allowed are:

READ - controls read access.

WRITE - controls write, delete, and rename access.

EXECUTE - controls execute access.

ALL - controls all access.

The pairs are processed in the order they appear, with later pairs modifying the effect of earlier pairs. This permits setting one type of access without explicitly setting all others. For example:

```
secure [
	net allow
	file [
		ask all
		allow read
		quit execute
	]
]
```

The above sets the security level to ask for all operations except for reading (which is allowed).

This technique can also be used for individual files and directories. For example:

```
secure [
	net allow
	file quit
	%source/ [ask read]
	%object/ [allow all]
]
```

will prompt the user if an attempt is made to read the %source directory, but it will allow all operations on the %object directory. Otherwise, it uses the default (quit).

If no security access level is specified for either network or file access, it defaults to ASK. The current settings will not be modified if an error occurs parsing the security block argument.

The SECURE function returns the prior security settings before the new settings were made. This is a block with the global network and file settings followed by file or directory settings. The word QUERY can also be used to obtain the current security settings without modifying them:

```
probe secure query
[net allow library allow shell allow file allow]
```

Using QUERY, you can modify the current security level by querying the current settings, modifying them, then using the secure function to set the new values.

Note that lowering the security level produces a change security settings requestor to the user. The exception is when the REBOL session is running in quiet mode which will, instead, terminate the REBOL session. No request is generated when security levels are raised. Note that the security request includes an option to allow all access for the remainder of the scripts processing.

When running REBOL, the -s argument can be provided on the command line to specify an initial security of:

```
secure allow
```

The +s argument will specify:

```
secure quit
```

You can also use the --secure argument to specify any other default security level on REBOL startup.

## Related:

[**open**](http://www.rebol.com/docs/words/wopen.html) - Opens a new port connection.
[**read**](http://www.rebol.com/docs/words/wread.html) - Reads from a file, url, or port-spec (block or object).
[**write**](http://www.rebol.com/docs/words/wwrite.html) - Writes to a file, url, or port-spec (block or object).