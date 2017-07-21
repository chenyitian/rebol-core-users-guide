# Chapter 2 - Operation

## Contents:

[1. Installing REBOL](#section-1)
  [1.1 Distribution Files](#section-1.1)
  [1.2 Home Environment Variable](#section-1.2)
  [1.3 Network Setup](#section-1.3)
  [1.4 Proxy and Firewall Settings](#section-1.4)
  [1.5 License Agreement](#section-1.5)
[2. Starting REBOL](#section-2)
  [2.1 From an Icon](#section-2.1)
  [2.2 From a Shell](#section-2.2)
  [2.3 From Another Application](#section-2.3)
  [2.4 Security Issues](#section-2.4)
  [2.5 Program Arguments](#section-2.5)
  [2.6 Script File](#section-2.6)
  [2.7 Specifying Options](#section-2.7)
  [2.8 File Redirection](#section-2.8)
  [2.9 Script Arguments](#section-2.9)
  [2.10 Startup Files](#section-2.10)
[3. Quitting REBOL](#section-3)
[4. Using the Console](#section-4)
  [4.1 Mulitple Line Input](#section-4.1)
  [4.2 Interrupting a Script](#section-4.2)
  [4.3 History Recall](#section-4.3)
  [4.4 Word Completion](#section-4.4)
  [4.5 Busy Indicator](#section-4.5)
  [4.6 Network Connections](#section-4.6)
  [4.7 Virtual Terminal](#section-4.7)
[5. Getting Help](#section-5)
  [5.1 Online Help](#section-5.1)
  [5.2 Viewing Source Code](#section-5.2)
  [5.3 Download Documents](#section-5.3)
  [5.4 Script Library](#section-5.4)
  [5.5 User Mailing List](#section-5.5)
  [5.6 Contacting Us](#section-5.6)
[6. Errors](#section-6)
  [6.1 Error Messages](#section-6.1)
  [6.2 Redirecting Errors](#section-6.2)
[7. Upgrading](#section-7)

## 1. Installing REBOL

REBOL installation takes only a few seconds and is very easy, non-intrusive, and non-disruptive.

For REBOL/Core the only installation procedure is to uncompress the distribution files and store them in any directory on your system.

For other REBOL products, installation may require you to provide additional information, such as where to store related files. Refer to the release notes that are included with the distribution files.

### 1.1 Distribution Files

REBOL/Core includes these primary distribution files:

|      | **rebol (.exe)** | An executable program that starts the REBOL console. |
| ---- | ---------------- | ---------------------------------------- |
|      | **rebol.r**      | A system bootstrap file. (Not required to run REBOL.) |
|      | **setup.html**   | Information about set-up and installation. |
|      | **changes.html** | Changes found in recent releases.        |
|      | **license.txt**  | REBOL license agreement.                 |

Other files may be provided, depending on the REBOL product and version.

### 1.2 Home Environment Variable

Although it is not required, if your operating system sets the HOME environment variable, REBOL will use it to locate its startup files. On many operating systems such as UNIX or Linux, the HOME variable may be set by default already. (So you do not need to set it yourself).

### 1.3 Network Setup

The first time you start REBOL, it prompts you for network information. This information is optional. Some protocols, such as email or FTP, require an email address or an email server name. In addition, if you are behind a firewall or use a proxy server, you need to provide specific information to access the Internet.

To set up your network:

1. Type your email address. For example, name@example.com.
2. Type the name of your email server. For example: mail.example.com. Use the name of the email server you normally use. If you are not sure of the name of the server, contact your network administrator or Internet service provider for the name of your SMTP (email) server.
3. Specify whether you use a proxy server. If you are directly connected to the Internet with a modem or ethernet, type N (no). If you use a proxy or firewall, provide the required information as described in [Proxy and Firewall Settings](#_Toc487519637) below.

Once the startup questions are answered, REBOL creates a `user`.`r` file and places your network settings in it. You can change these settings at any time by editing the `user`.`r` file.

### 1.4 Proxy and Firewall Settings

Frequently, organizations use a firewall or proxy server to protect access to and from the Internet. Before REBOL can access the Internet through these systems, you need to provide some additional information.

To provide proxy server information:

1. When REBOL asks if you use a proxy server, answer by typing Y (yes).
2. Type the name of your proxy host. This is the computer or firewall on your network serving as a proxy.
3. Type the port number used by the proxy host for proxy requests. Typically, this is port 1080, but this can vary. If you don't know the port number, check your Web browser settings or ask your network administrator.

REBOL defaults to using a SOCKS proxy protocol. You can specify some other type of proxy by editing the `user`.`r`file and supplying the **set-net** function with the appropriate identification for the type of proxy being used. The following settings are supported:

```
socks   - use the latest SOCKS version (5)
socks5  - use socks5 proxy
socks4  - use socks4 proxy
generic - use generic CERN proxy
none    - use no proxy
```

These settings are provided as the sixth argument to the **set-net** function called in the `user`.`r` file. For more information about modifying the proxy settings in the `user`.r file, refer to the [Network Protocols Chapter](rebolcore-13.html#_Toc487519750).

### 1.5 License Agreement

The REBOL end-user license agreement that you agreed to when you downloaded or installed REBOL can be viewed at any time from the REBOL console by typing `license` at the REBOL prompt.

## 2. Starting REBOL

REBOL runs on a large variety of systems. You start REBOL the same way you start other applications on your system. Depending on the specific operating system, REBOL can be started from one or more of the following: an icon, the command shell, or other applications.

### 2.1 From an Icon

REBOL can be started by double-clicking the REBOL program icon, an associated ``.r file, or a REBOL shortcut icon.

If you double-click on the program icon, REBOL boots, displays the console, and provides you with a prompt.

If you want to launch REBOL with a script, you can do so in the following ways:

- Drag the script to the program icon
- Associate the file with the REBOL program
- Create a shortcut or alias icon with program and script information.

See your operating system manual for more information.

### 2.2 From a Shell

From a shell command line, go to the directory that contains the `rebol`.`exe` file (or `rebol` on non-Windows systems), and type rebol or ./rebol.

On some operating systems, such as UNIX, you can create alias shell commands that are able to run REBOL with a set of arguments and files. In addition, UNIX enables you to create shell scripts that include a path, such as:

```
!#/path/to/rebol

```

in the top line of the script file. When you type the name of the script file at the command prompt, UNIX will launch REBOL to execute the script.

### 2.3 From Another Application

For writing and debugging REBOL scripts, it is handy to set up your favorite text editor to run REBOL and pass it the script file you are editing. Each text editor does this differently.

For instance, in the Premia Codewright editor you can use the language compiler options to set up REBOL. Specify the REBOL program rather than a compiler. Then you can press a single key that saves the script and evaluates it.

### 2.4 Security Issues

By default, security is set to prevent scripts from modifying any of your files or directories.

#### 2.4.1 Port Security

The **secure** function provides flexibility in setting and controlling the security features of REBOL. The current security settings are returned as a result of calling the **secure** function.

Security settings use a REBOL dialect, that is, a language within a language. The normal dialect consists of a block of paired values. The `first` value in the pair specifies what is being secured:

|      | **file** | specifies file security.    |
| ---- | -------- | --------------------------- |
|      | **net**  | specifies network security. |

A file name or directory path allows you to specify security levels for a specific file or directory.

The `second` value in the pair specifies the level of security. This can be either a security level word or a block of words. The security level words are:

|      | **allow** | allow access with no restrictions.       |
| ---- | --------- | ---------------------------------------- |
|      | **ask**   | ask permission if any restricted access occurs. |
|      | **throw** | throw an error if any restricted access occurs. |
|      | **quit**  | quit this REBOL session if any restricted access occurs. |

For example, to allow all network access, but to quit on any file access:

```
secure [
    net allow ;allows any net access
    file quit ;any file access will cause the program to quit
]

```

If a block is used instead of a security level word, it can contain pairs of security levels and access types. This lets you specify a greater level of detail about the security you require. The access types allowed are:

|      | **read**  | controls read access.                    |
| ---- | --------- | ---------------------------------------- |
|      | **write** | controls write, delete and rename access. |
|      | **all**   | controls all access.                     |

The pairs are processed in the order they appear, with later pairs modifying the effect of earlier pairs. This permits setting one type of access without explicitly setting all others. For example:

```r
secure [
    net allow
    file [
        ask all
        allow read
    ]
]
```

The above sets the security level to **ask** for all operations except for reading which is to be allowed. This technique can also be used for individual files and directories. For example:

```
secure [
    net allow
    file quit
    %source/ [ask read]
]

```

asks if an attempt is made to read the `%source` directory. Otherwise, it uses the default (**quit**).

There is a special case in which the **secure** function takes a single word argument that must be one of the security access levels. In that case, the security level for all network and file access is set to that level.

```
secure quit

```

The **secure** function also accepts **none**, allowing access with no restrictions (same as **allow** ).

```
secure none

```

The default security level is now:

```
secure [
    net allow
    file [
        ask all
        allow read
    ]
]

```

If no security access level is specified for either network or file access, it defaults to **ask**. The current settings will`not` be modified if an error occurs parsing the security block argument.

#### 2.4.2 Prior Security Settings

The **secure** function now returns the prior security settings before the new settings were made. This is a block with the global network and file settings followed by file or directory settings. The **query** word can be used to obtain the settings without modifying them.

```
current-security: secure query

```

You can modify the current security level by querying the current settings, modifying them, then using the **secure**function to set the new values.

Lowering the security level produces a `change` security settings request. The exception is when the REBOL session is running in `quiet` mode which will, instead, terminate the REBOL session. No query is generated when security levels are raised. Note that the security request now includes an option to allow all access for the remainder of the scripts processing.

When running REBOL from the shell, the **-s** argument is equivalent to:

```
secure allow

```

and the **+s** arguments is equivalent to:

```
secure quit

```

You can now follow the **--secure** argument with one of the security access levels for both network and file access:

```
rebol --secure throw

```

### 2.5 Program Arguments

There are a number of arguments that can be specified in a shell command line, in a batch script, or in the properties of an icon. To view the arguments and options available for any version of the REBOL language, type `usage` at the console prompt.

```
The command line usage is:

    REBOL <options> <script> <arguments>

All fields are optional. Supported options are:

    --cgi (-c)       Check for CGI input
    --do expr        Evaluate expression
    --help (-?)      Display this usage information
    --nowindow (-w)  Do not open a window
    --noinstall (-i) Do not install (View)
    --quiet (-q)     Don't print banners
    --reinstall (+i) Force an install (View)
    --script file    Explicitly specify script
    --secure level   Set security level:
                     (allow ask throw quit)
    --trace (-t)     Enable trace mode
    --uninstall (-u) Uninstall REBOL (View)

Other command line options:

    +q               Force not quiet (View)
    -s               No security
    +s               Full security
    -- args          Provide args without script

Examples:

    REBOL script.r
    REBOL script.r 10:30 test@domain.dom
    REBOL script.r --do "verbose: true"
    REBOL --cgi -s
    REBOL --cgi --secure throw --script cgi.r "debug: true"
    REBOL --secure none

```

Again, the format of the command line is:

```
REBOL options script arguments

```

Where:

|      | **options**   | one or more of the program options. See [Specifying Options](#_Toc487519647) below for more details. |
| ---- | ------------- | ---------------------------------------- |
|      | **script**    | the file name of the script you want to run. If the file name contains spaces, it should be typed in quotes. |
|      | **arguments** | the arguments passed to the script as a string. These arguments can be accessed from within the script. |

All of the above arguments are optional, and any combination is permitted.

**Shortcut Icons**

In some operating systems, like Windows or AmigaOS, you can create icons that supply any of the above options as part of the icon. Using this technique, you can create icons that directly execute REBOL scripts with the correct options.

### 2.6 Script File

Typically, you run REBOL with the file name of the script that you want it to evaluate. Only one script file is allowed. For example:

```
REBOL script.r

```

If the file name contains spaces, it must be provided in double quotes.

### 2.7 Specifying Options

[Program options are identifed with a plus (+) or minus (-) before a character or by a double dash (--) before a word. This is a standard practice for specifying program options on most operating systems.Here are several examples of how options are used.To run a script with an option, such as the `-s` option, which evaluates the script with security turned off, type:`REBOL -s script.r`To obtain usage information about REBOL, type:`REBOL -?REBOL --help`To run REBOL without opening a new window (this is done when you need to redirect output to a file or server), type:`REBOL -wREBOL --nowindow`To prevent the printout of startup information which is useful if you are redirecting the output to a file or server, type:`REBOL -qREBOL --quiet`To evaluate a REBOL expression from the command line, type:`REBOL --do "print 1 + 2"REBOL --do "verbose: true" script.r`This lets you evaluate a remote script with a line such as:`REBOL --do "do http://www.rebol.com/speed.r"`To change the security level of REBOL, type:`REBOL -s script.rREBOL --secure none script.r`]()[To use REBOL scripts for CGI (see the ]()[CGI - Common Gateway Interface Section](rebolcore-13.html#_Toc487519913) of the [Network Protocols Chapter](rebolcore-13.html#_Toc487519750) for more information), type:`REBOL -c cgi-script.rREBOL --cgi`Multiple options are also allowed. Multiple single character options can be included together. Multiple full word options must be separated with spaces.`REBOL -cs cgi-script.rREBOL --cgi --secure none cgi-script.r`The above example runs in CGI mode, with security turned off. The shorthand method is required for various web servers that restrict the number of arguments allowed on the command line (such as the Apache server on Linux).

### 2.8 File Redirection

On most systems, it is possible to redirect standard input and output from and to files. The example:

```
rebol -w script.r > output-file

```

redirects output to a file. Similarly,

```
rebol -w script.r < input-file

```

redirects input from a file.

**When Redirecting File IO...**

Use the `-w` option to prevent the REBOL console window from opening, as it interferes with standard input and output redirection.

### 2.9 Script Arguments

Everything on the command line that follows the script file name is passed to the script as its argument. This allows you to write scripts that accept arguments directly from the command line. For example, if you start REBOL with the line:

```
REBOL script.r 10:30 test@domain.dom

```

There are two ways to obtain the command line arguments. The first method returns the arguments as a block of REBOL values:

```
probe system/options/args
["10:30" "test@domain.dom"]

```

The second method returns the arguments as a string:

```
probe system/script/args
"10:30 test@domain.dom"

```

**Version dependent note:**

Earlier versions of REBOL returned the block of values for the script/args field (similar to options/args). It is advised that you verify that your script receives the correct args datatype as shown above.

### 2.10 Startup Files

When REBOL starts, it attempts to load the `rebol`.`r` and `user`.`r` boot files. These files are optional, but when found, they can be used to set up networking, define common functions, and initialize data used by scripts.

The `rebol`.`r` script file holds special functions or extensions to REBOL that are provided as part of the standard distribution. It is suggested that you do not edit this file as it is overwritten with each new release of REBOL.

The `user`.`r` script file holds user preferences. You can edit this file and add whatever definitions or data you require.

On multi-user systems, there can be a different `user`.`r` for every user. While the `user`.`r` file is not part of the distribution, it is automatically generated if it does not exist.

When REBOL starts, it looks for the `rebol`.`r` and `user`.`r` files first in the home directory and, if not found there, then in the current directory.

To set a HOME directory, you can set an environment variable in the appropriate login or startup script for your system. Note that some systems, such as UNIX or Linux may already do this, so you do not need to.

For example, on Windows NT to set HOME you can add:

```
set HOME=C:\REBOL

```

to your environment by following these steps:

1. Choose Settings Control Panel in the Windows Start Menu,
2. Double-click the System icon, and select the Environment tab.
3. Type HOME in the variable field and C:\REBOL (or the path to where you put the REBOL program) in the value field.

On Unix systems, you can set the path to REBOL by adding a line like the following in your login shell script or profile:

```
set HOME=/usr/bin/rebol

```

For some versions of REBOL, the path is stored in a .`rebol` file that is located in your home directory.

## 3. Quitting REBOL

To exit REBOL at any time, select **Quit** from the **Console** **File** menu or by typing **quit** or **q** at the prompt.

You can also quit the program from within a script:

```
if now/time > 12:00 [quit]

```

The REBOL console may also quit if an error occurs during startup.

**Exit Does Not Quit**

Do not use the word **exit** to quit REBOL. This word is used for exiting functions and it will return an error if typed at the console.

## 4. Using the Console

Whenever you run REBOL/Core, it opens a console to display output and accept input. If you provide a script argument to the program, the script is run, and you see the output from that script. If you do not provide a script file, the console prompts you for input. The input prompt looks like this:

```
>>

```

If you type an expression at the input prompt, it is evaluated and any returned values are displayed following the result indicator:

```
==

```

For example:

```
>> 100 + 20
== 120
>> now - 7-Dec-1944
== 20341

```

**Changing the Prompt**

The prompt characters can be changed. See the [Console Appendix](rebolcore-18.html#_Toc487519750) for more information.

The console also becomes active if a script encounters an error or if the script calls the **halt** function.

### 4.1 Mulitple Line Input

If you begin a block on the command line and don't end it, the block is extended to the next line. This is indicated by a prompt that begins with a bracket and is followed by indentation. The line will be indented four spaces for each open block. For example:

```
loop 10 [
[    print "example"
[    if odd? random 10 [
[        print "here"
[        ]
[    ]

```

This is also true for multilined strings enclosed in braces.

```
Print {This is a long
{    string that has more
{    than one line.}

```

Brackets and braces that appear within quoted strings are ignored. You can escape from input at any time by pressing the ESCAPE key.

### 4.2 Interrupting a Script

A script can be interrupted by pressing the ESCAPE key, which returns immediately to the command prompt.

During some types of operating system or network activity there may be a delay in responding to the ESCAPE interrupt.

### 4.3 History Recall

Each line that is typed into REBOL is stored for later recall. The up and down arrow keys are used to scroll through the list of previous lines. For instance, pressing the up arrow once recalls the prior input line.

History lines can be written to a file by saving the history block. See the [Console Appendix](rebolcore-18.html#_Toc487519750) for more information.

### 4.4 Word Completion

To help speed typing of long words and file names, the REBOL console has word and file name completion. After typing a few letters of a word, press the tab key. If the letters uniquely identify the word, the rest of the word is displayed. For example, typing:

```
>> sq
```

then pressing tab results in:

```
>> square-root

```

If the letters do not uniquely identify the word, you can press tab again to get a list of choices. For example, typing:

```
>> so

```

then pressing tab twice results in:

```
>> sort source

```

so

and you can type the rest of the word or enough of it to be unique.

Completion works for all words, including user-defined words. It also works for files when they are preceded by a percent sign.

```
>> print read %r

```

Pressing tab might produce:

```
>> print read %rebol.r

```

depending on your current directory.

### 4.5 Busy Indicator

When REBOL waits for a network operation to complete, a busy indicator appears to indicate that something is happening. You can change the indicator to your own character pattern. See the [Console Appendix](rebolcore-18.html#_Toc487519750) for more information.

### 4.6 Network Connections

As network connections are initiated, a message appears on the console. For instance, typing:

```
>> read http://www.rebol.com
connecting to: www.rebol.com

```

If necessary, you can disable this output by setting the quiet flag. See the [Console Appendix](rebolcore-18.html#_Toc487519750) for more information.

### 4.7 Virtual Terminal

The console provides `virtual` terminal capability that allows you to perform operations such as cursor movement, cursor addressing, line editing, screen clearing, control key input, and cursor position querying.

The virtual terminal uses the standard ANSI character sequences. This allows you to write platform-independent terminal programs such as text editors, email clients, or telnet emulators.

More information can be found in the [Console Appendix](rebolcore-18.html#_Toc487519750).

## 5. Getting Help

Several sources of information exist: online help built into REBOL, the **source** function, [documents on the REBOL website](http://www.rebol.com/docs.html), the [REBOL script library](http://www.rebol.org), the [REBOL mailing list](http://www.rebol.com//discussion.html), and sending [feedback to REBOL](http://www.rebol.com/feedback.html).

### 5.1 Online Help

The online **help** function provides a quick way to obtain summary information about REBOL words. There are several ways to use help.

Type **help** or **?** at the console prompt to view a summary of help:

```
The help function provides a simple way to get
information about words and values.  To use it
supply a word or value as its argument:

    help insert
    help find

To view all words that match a pattern:

    help "path"
    help to-

To view all words of a specified datatype:

    help native!
    help datatype!

There is also word completion from the command
line.  Type a few chars and press TAB to complete
the word.  If nothing happens, there is more than
one word that matches.  Enough chars are needed
to uniquely identify the word.

Other useful functions:

    about - for general info
    usage - for the command line arguments
    license - for the terms of user license
    source func - print source for given function
    upgrade - updates your copy of REBOL

For more information, see the user guides.

```

If you provide a function word as an argument, **help** prints all of the information that was provided about the function. For instance, if you type:

```
help insert

```

you will see:

```
USAGE:
    INSERT series value /part range /only /dup count

DESCRIPTION:
     Inserts a value into a series and returns the series after the insert.
     INSERT is an action value.

ARGUMENTS:
     series -- Series at point to insert (Type: series port bitset)
     value -- The value to insert (Type: any-type)

REFINEMENTS:
     /part -- Limits to a given length or position.
         range -- (Type: number series port)
     /only -- Inserts a series as a series.
     /dup -- Duplicates the insert a specified number of times.
         count -- (Type: number)

```

The **help** function also finds words that contain a specified string. For instance, to find all of the words that include the string `path`, type:

```
? "path"

```

and the result will be:

```
Found these words:
     clean-path     (function)
     lit-path!      (datatype)
     lit-path?      (action)
     path           (file)
     path!          (datatype)
     path-thru      (function)
     path?          (action)
     set-path!      (datatype)
     set-path?      (action)
     split-path     (function)
     to-lit-path    (function)
     to-path        (function)
     to-set-path    (function)

```

You can also search for all globally defined words that are of a given data type. For example, to list all words that are function! data types, type:

```
? function!

```

and the result would be:

```
Found these words:
     ?              (function)
     ??             (function)
     about          (function)
     alert          (function)
     alter          (function)
     append         (function)
     array          (function)
     ask            (function)
...

```

To obtain a list of all REBOL datatypes, type:

```
? datatype!

Found these words:
     action!        (datatype)
     any-block!     (datatype)
     any-function!  (datatype)
     any-string!    (datatype)
     any-type!      (datatype)
     any-word!      (datatype)
     binary!        (datatype)
     bitset!        (datatype)
     block!         (datatype)
     char!          (datatype)
     datatype!      (datatype)
     date!          (datatype)
     decimal!       (datatype)
     email!         (datatype)
...

```

**No Help for Objects**

[The **help** function does not provide useful information about the objects of the system, for example:]()

```
help system/options/home
system/options/home is a path.

```

Do not attempt to do:

```
help system

```

as it can take several minutes and produce over a megabyte of text output.

### 5.2 Viewing Source Code

Advanced users can learn more about specific REBOL functions by examining their source code. The **source**function displays the code for any REBOL defined function. If you type:

```
source join

```

The source to the **join** function will be returned:

```
join: func [
    "Concatenates values."
    value "Base value"
    rest "Value or block of values"
][
    value: either series? value [copy value] [form value]
    repend value rest
]

```

REBOL defined functions include the **mezzanine** **functions** (built-in functions implemented in REBOL) and user defined functions. **Native** **functions** are built-in functions implemented in machine code, and their source cannot be displayed.

### 5.3 Download Documents

[Check the REBOL Web site ]()[http://www.rebol.com/](http://www.rebol.com/) for a list of the current documentation.

In addition to this manual, there is a *REBOL Dictionary* that covers all the predefined words available in REBOL. If the console help or this guide does not contain sufficient information about a REBOL word, look in the dictionary for a detailed description.

The dictionary is updated with each release of REBOL and is available at [http://www.REBOL.com/docs/dictionary.html](http://www.rebol.com/docs/dictionary.html).

### 5.4 Script Library

The REBOL Web site contains a library with numerous useful debugged scripts that cover a variety of topics. The library is divided into categories to make it easy to find a script specific to a given function. You can also search the library for scripts that contain a specific word.

The script library can be found at [http://www.REBOL.com/library/library.html](http://www.rebol.com/library/library.html).

### 5.5 User Mailing List

You can also obtain help from a community of REBOL users by joining the REBOL email discussion list. To sign up, send an email to rebol-request@rebol.com with the subject line containing the word "subscribe". For example:

```
send rebol-request@rebol.com "subscribe"

```

Be sure that your correct email address has been set up in advance with **set-net**.

### 5.6 Contacting Us

We want to know what you think; please contact us to:

- Report crashes or problems
- Tell us how you are using REBOL
- Make suggestions
- Request more information about our products.

You can reach us through the [Feedback](http://www.rebol.com/feedback.html) page on our website.

## 6. Errors

### 6.1 Error Messages

There are several types of errors within REBOL. When an error occurs a message is displayed that tells you what the error was and approximately where it occurred. For instance if you type:

```
abc
** Script Error: abc has no value.
** Where: abc

```

The type of error is indicated by the first few words of the message. In the above example, the error is a `Script`Error. Script errors are the most common and occur when you use a function of the language in the wrong way or with improper arguments. Other types of errors are described in [Error Types](#30433).

| Error Type         | Description                              |
| ------------------ | ---------------------------------------- |
| `Syntax``errors`   | Occur when the script contains an invalid value or a missing header, quote, bracket, or parenthesis. |
| `Math``errors`     | Occur when dividing a number by zero or there was a math overflow or underflow. |
| `Access``errors`   | Occur when a file, directory, or network operation cannot be accessed or access permissions are restricted. |
| `Throw``errors`    | Occur when a break, exit, or throw is used in an improper manner. |
| `User``errors`     | Defined by the user's script.            |
| `Internal``errors` | Returned when a problem occurs within the REBOL system. If you encounter one of these types of errors, please report it to [Feedback](http://www.rebol.com/feedback.html). |

Most types of errors can be trapped and processed by your script. See [Trying Blocks](rebolcore-4.html#_Toc487519749) for a description of the try function.

The [Errors Appendix](rebolcore-17.html#_Toc487519750) also includes useful information about errors.

### 6.2 Redirecting Errors

When errors are encountered in non-interactive sessions, such as when running in CGI mode (-c or --cgi ) or in no window mode (-w or --nowindow ), the session is automatically terminated.

If a script terminates while running in non-interactive mode, you can use shell redirection to output the error to a file:

```
REBOL -cs my_script.r >> my_script.log

```

This appends the output to the file in most operating systems.

## 7. Upgrading

On initialization, a banner is displayed that identifies the program version. Version numbers have the format:

```
version.revision.update.platform.variation

```

For example, the version number:

```
2.3.0.3.1

```

indicates that you are running version 2, revision 3, update 0, for Windows 95/98/NT (REBOL platform number 3.1). A complete list of all platform numbers is available from [http://www.rebol.com](http://www.rebol.com). This HTML file also contains a hidden REBOL database that can be used for determining the platform.

You can obtain the version number from the REBOL prompt with:

```
print system/version

```

Only the latest release of REBOL is supported by REBOL Technologies. You can verify that you have the latest version and automatically update it if out of date. To do so, be sure that you are connected to the Internet, then from within REBOL type:

```
upgrade

```

REBOL returns one of the following messages about your version:

```
This copy of Windows 95/98/NT iX86 REBOL/core 2.3.0.3.1
is currently up to date.

```

or:

```
This copy of Windows 95/98/NT iX86 REBOL/core 2.1.2.3.1
is not up to date. Current version is: 2.3.0.3.1.
Download current version?

```

To upgrade to the latest version, type `Y` (yes). Otherwise, type `N` (no).