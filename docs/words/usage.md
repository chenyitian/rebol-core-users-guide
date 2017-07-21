# Usage - Function Summary

------

## Summary:

Prints command-line arguments.

## Usage:

**usage**

## Description:

Displays REBOL command line arguments, including options and examples.

```
usage
The command line usage is:

	REBOL <options> <script> <arguments>

All fields are optional. Supported options are:

	--cgi (-c)       Check for CGI input
	--do expr        Evaluate expression
	--link url       Connect to Link
	--help (-?)      Display this usage information
	--nowindow (-w)  Do not open a window
	--noinstall (-i) Do not install (Link, View)
	--quiet (-q)     Don't print banners
	--reinstall (+i) Force an install (Link, View)
	--script file    Explicitly specify script
	--secure level   Set security: allow ask throw quit
	--trace (-t)     Enable trace mode
	--uninstall (-u) Uninstall REBOL (Link, View)

Other command line options:

	+q               Force not quiet (Link, View)
	-s               No security
	+s               Full security
	-- args          Provide args without a script

Examples:

	REBOL script.r
	REBOL -s script.r
	REBOL script.r 10:30 test@domain.dom
	REBOL script.r --do "verbose: true"
	REBOL -cswq
	REBOL --cgi --secure throw --script cgi.r "debug: true"
```

SDK and special versions of REBOL may not include usage information.

## Related:

[**?**](http://www.rebol.com/docs/words/wq.html) - Prints information about words and values.
[**help**](http://www.rebol.com/docs/words/whelp.html) - Prints information about words and values.