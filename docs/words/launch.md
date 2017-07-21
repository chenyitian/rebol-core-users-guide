# Launch - Function Summary

------

## Summary:

Launches a new REBOL interpreter process.

## Usage:

**launch value**

## Arguments:

**value** - The command-line arguments (must be: any-string)

## Refinements:

**/reboot** - Reserved

**/uninstall** - Restart with uninstall option

**/link** - Reserved

**url** - The url argument.

**/quit** - Launch first, then quit

**/secure-cmd** - Reserved

**/as-is** - No quotes around command line argument

## Description:

The LAUNCH function is used to run REBOL scripts as a separate process. When LAUNCH is called, a new process is created and passed the script file name or URL to be processed. The process is created as a subprocess of the main REBOL process.

Launch has certain restrictions depending on the REBOL system used. Also, within Unix/Linux systems, launch will use the same shell standard files as the main REBOL process, and output will be merged.

```
launch %calculator.r

launch http://www.rebol.com/scripts/news.r
```