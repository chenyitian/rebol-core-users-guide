# Network Protocols

## Contents:

- [1. Overview](#section-1)
- [2. REBOL Networking Basics](#section-2)
  - [2.1 Modes of Operation](#section-2.1)
  - [2.2 Specifying Network Resources](#section-2.2)
  - [2.3 Schemes, Handlers, and Protocols](#section-2.3)
  - [2.4 Monitoring Handlers](#section-2.4)
- [3. Initial Setup](#section-3)
  - [3.1 Basic Network Settings](#section-3.1)
  - [3.2 Proxy Settings](#section-3.2)
  - [3.3 Other Settings](#section-3.3)
  - [3.4 Access to Settings](#section-3.4)
- [4. DNS - Domain Name Service](#section-4)
- [5. Whois Protocol](#section-5)
- [6. Finger Protocol](#section-6)
- [7. Daytime - Network Time Protocol](#section-7)
- [8. HTTP - Hyper Text Transfer Protocol](#section-8)
  - [8.1 Reading a Web Page](#section-8.1)
  - [8.2 Scripts on Web Sites](#section-8.2)
  - [8.3 Loading Markup Pages](#section-8.3)
  - [8.4 Other Functions](#section-8.4)
  - [8.5 Acting Like a Browser](#section-8.5)
  - [8.6 Posting CGI Requests](#section-8.6)
- [9. SMTP - Simple Mail Transport Protocol](#section-9)
  - [9.1 Sending Email](#section-9.1)
  - [9.2 Multiple Recipients](#section-9.2)
  - [9.3 Bulk Mail](#section-9.3)
  - [9.4 Subject Line and Headers](#section-9.4)
  - [9.5 Debug Your Scripts](#section-9.5)
- [10. POP - Post Office Protocol](#section-10)
  - [10.1 Reading Email](#section-10.1)
  - [10.2 Removing Email](#section-10.2)
  - [10.3 Handling Email Headers](#section-10.3)
- [11. FTP - File Transfer Protocol](#section-11)
  - [11.1 Using FTP](#section-11.1)
  - [11.2 FTP URLs](#section-11.2)
  - [11.3 Transferring Text Files](#section-11.3)
  - [11.4 Transferring Binary Files](#section-11.4)
  - [11.5 Appending to Files](#section-11.5)
  - [11.6 Reading Directories](#section-11.6)
  - [11.7 File Information](#section-11.7)
  - [11.8 Making Directories](#section-11.8)
  - [11.9 Deleting Files](#section-11.9)
  - [11.10 Renaming Files](#section-11.10)
  - [11.11 About Passwords](#section-11.11)
  - [11.12 Transferring Large Files](#section-11.12)
- [12. NNTP - Network News Transfer Protocol](#section-12)
  - [12.1 Reading the Newsgroup List](#section-12.1)
  - [12.2 Reading All Messages](#section-12.2)
  - [12.3 Reading Single Messages](#section-12.3)
  - [12.4 Handling News Headers](#section-12.4)
  - [12.5 Sending a News Message](#section-12.5)
- [13. CGI - Common Gateway Interface](#section-13)
  - [13.1 CGI Server Setup](#section-13.1)
  - [13.2 CGI Scripts](#section-13.2)
  - [13.3 Generating HTML Content](#section-13.3)
  - [13.4 CGI Environment](#section-13.4)
  - [13.5 CGI Requests](#section-13.5)
  - [13.6 Processing HTML Forms](#section-13.6)
- [14. TCP - Transmission Control Protocol](#section-14)
  - [14.1 Creating Clients](#section-14.1)
  - [14.2 Creating Servers](#section-14.2)
  - [14.3 A Tiny Server](#section-14.3)
  - [14.4 Testing TCP Code](#section-14.4)
- [15. UDP - User Datagram Protocol](#section-15)

## 1. Overview

REBOL includes several of the primary Internet service protocols built-in. These protocols are easy to use within your scripts; they require no extra libraries or include files, and many useful operations can be done with only a single line of source code.

The protocols listed in [Network Protocols](#50687) are supported:

|      | **DNS**     | Domain Name Service: translates computer names into addresses and addresses into names. |
| ---- | ----------- | ---------------------------------------- |
|      | **Finger**  | Obtains information about a user from their profile. |
|      | **Whois**   | Obtains information about domain registration. |
|      | **Daytime** | Network Time Protocol. Gets the time from a server. |
|      | **HTTP**    | Hypertext Transfer Protocol. Used for the Web. |
|      | **SMTP**    | Simple Mail Transfer Protocol. Used for sending email. |
|      | **POP**     | Post Office Protocol. Used for fetching email. |
|      | **FTP**     | File Transfer Protocol. Exchanges files with a server. |
|      | **NNTP**    | Network News Transfer Protocol. Posts or reads Usenet news. |
|      | **TCP**     | Transmission Control Protocol. Basic Internet protocol. |
|      | **UDP**     | User Datagram Protocol. Packet-based protocol. |

In addition, you can create handlers for other Internet protocols or make your own custom protocols.

## 2. REBOL Networking Basics

### 2.1 Modes of Operation

There are two basic modes of network operation: atomic and port-based.

`Atomic` network operations are those that are accomplished in a single function. For instance, you can read an entire Web page with a single call to the read function. There is no need to separately open a connection or set up the read. All of that is done automatically as part of the read. For example, you can type:

```
print read http://www.rebol.com

```

The host is found and opened, its Web page transferred, and the connection closed.

The `port-based` mode of operation is one that uses a more traditional programming approach. It involves opening a port and performing various series operations on the port. For instance, if you want to read your email from a POP server one message at a time, you would use this method. Here is an example that reads and displays all of your email:

```
pop: open pop://user:pass@mail.example.com
forall pop [print first pop]
close pop

```

The atomic method of operation is easier, but it is also more limited. The port-based method allows more types of operations, but also requires a greater understanding of networking.

### 2.2 Specifying Network Resources

REBOL provides two approaches for specifying network resources: URLs and port specifications.

`Uniform` Resource Locators (URL) are used on the Internet to identify a network resource, such as a Web page, FTP site, email address, file, or other resource or service. URLs are integral to the operation of REBOL, and they can be expressed directly in the language.

The standard notation for URLs consists of a `scheme` followed by a specification:

```
scheme:specification

```

The scheme is often the name of a protocol, such as HTTP, FTP, SMTP, and POP; however, that is not a requirement. A scheme can be any name that identifies the method used to access a resource.

The format of a scheme's specification depends on the scheme; however, most schemes share a common format for identifying network hosts, user names, passwords, port numbers, and file paths. Here are a few commonly used formats:

```
scheme://host

scheme://host:port

scheme://user@host

scheme://user:pass@host

scheme://user:pass@host:port

scheme://host/path

scheme://host:port/path

scheme://user@host/path

scheme://user:pass@host/path

scheme://user:pass@host:port/path

```

[Network Resource Specification](#76862) lists the fields used in the above formats.

|      | **scheme** | The name used to identify the type of resource, often the same as the protocol. For example, HTTP, FTP, and POP. |
| ---- | ---------- | ---------------------------------------- |
|      | **host**   | The network name or address for a machine. For example, www.rebol.com, cnn.com, accounting. |
|      | **port**   | Port number on the host machine for the scheme being used. Normally there is a default for this, so it is not required most of the time. Examples: 21, 23, 80, 8000. |
|      | **user**   | A user name to access the resource.      |
|      | **pass**   | A password to verify the user name.      |
|      | **path**   | A file path or some other method for referencing the resource. This is scheme dependent. Some schemes include patterns and script arguments (such as CGI). |

Another way to identify a resource is with a REBOL `port` specification. In fact, when a URL is used, it is automatically converted into a port specification. A port specification can accept many more arguments than a URL, but it requires multiple lines to express.

A port specification is written as an object block definition that provides each of the parameters necessary to access the network resource. For instance, the URL to access a Web site is:

```
read http://www.rebol.com/developer.html

```

but, it can also be written as:

```
read [
    scheme: 'HTTP
    host: "www.rebol.com"
    target: %/developer.html
]

```

The URL for an FTP read can be:

```
read ftp://bill:vbs@ftp.example.com:8000/file.txt

```

but, it can also be written as:

```
read [
    scheme: 'FTP
    host: "ftp.example.com"
    port-id: 8000
    target: %/file.txt
    user: "bill"
    pass: "vbs"
]

```

In addition, there are many other port fields that can be specified, such as timeout, type of access, and security.

### 2.3 Schemes, Handlers, and Protocols

REBOL networking operates by using `schemes` to identify `handlers` that communicate with `protocols`.

In REBOL a `scheme` is used to identify the method of accessing a resource. That method uses a code object that is called a `handler`. Each of the URL schemes that are supported by REBOL (such as HTTP, FTP) has a handler. The list of schemes can be obtained with:

```
probe next first system/schemes
[default Finger Whois Daytime SMTP POP HTTP FTP NNTP]

```

In addition, there are lower level scheme names that are not shown here. For instance, the TCP and UDP schemes are used for direct, lower level communication.

New schemes can be added to this list. For instance, you can define your own scheme, called FTP2, that provides special features for FTP access, such as automatically supplying your username and password so it does not need to be included in every FTP URL.

Most handlers are used to provide an interface to a network protocol. A `protocol` is used to communicate between various devices, including clients and servers.

Although each protocol is quite different in how it communicates, it does have some things in common with other protocols. For instance, most protocols require a network connection to be opened, read, written, and closed. These common operations are performed by a default handler in REBOL. This handler makes protocols like finger, whois, and daytime almost trivial to implement.

Scheme handlers are written as objects. The default handler serves as the root object for all the other handlers. When a handler requires a particular field, such as a timeout value to use for reading data, if the value is not defined in the specific handler, it will be provided by the default handler. Hence, handlers overlay one another with their fields and value. You can also create handlers that use other handlers for default values. For instance, you can create an FTP2 handler that looks for missing fields first in the FTP handler, then in the default handler.

When a port is used to access network resources, it is linked to a specific handler. The handler and the port together form the unit that is used to provide the data, code, and state information to process all protocols.

The source code to handlers can be obtained from the system/scheme object. This can be useful if you want to modify the behavior of a handler or build your own handler. For instance, to view the code for the whois handler, type:

```
probe get in system/schemes 'whois

```

Note that what you are seeing is a composite of the default handler with the whois handler. The actual source code that is used to create the whois handler is only a few lines:

```
make Root-Protocol [
    open-check:  [[any [port/user ""]] none]
    net-utils/net-install Whois make self [] 43
]

```

### 2.4 Monitoring Handlers

For debugging purposes, you can monitor the actions of any handler. Each handler has its own debugging output to indicate what operations are being performed. To enable network debugging, turn network tracing on with the line:

```
trace/net on

```

To turn network debugging off, use:

```
trace/net off

```

Here is an example:

```
read pop://carl:poof@zen.example.com
URL Parse: carl poof zen.example.com none none none
Net-log: ["Opening tcp for" POP]
connecting to: zen.example.com
Net-log: [none "+OK"]
Net-log: {+OK QPOP (version 2.53) at zen.example.com starting.}
Net-log: [["USER" port/user] "+OK"]
Net-log: "+OK Password required for carl."
Net-log: [["PASS" port/pass] "+OK"]
** User Error: Server error: tcp -ERR Password supplied for "carl"
is incorrect.
** Where: read pop://carl:poof@zen.example.com

```

## 3. Initial Setup

REBOL networking is built-in. To create scripts that use the network protocols you do not need any special include files or libraries. The only requirement is that you provide the basic information necessary to enable protocols to connect to servers or through firewalls and proxies. For instance, to send an email, the SMTP protocol needs an SMTP server name and a reply email address.

### 3.1 Basic Network Settings

When you run REBOL the first time, you re prompted for the necessary network settings, which is stored in the `user`.r file. REBOL uses this file to load the required network settings each time it is started. If a `user`.r is not created and REBOL cannot find an existing `user`.r file in its paths, no settings are loaded. See the chapter on [Operation](rebolcore-3.html#_Toc487519750) for more information.

To change the network settings, type **set-user** at the prompt. This runs the same network configuration script that ran when REBOL first started. This script is loaded from the `rebol`.r file. If that file cannot be found, or if you want to edit the setting directly, you can use a text editor on the `user`.r file.

Within the `user`.r file the network settings are found in a block that follows the **set-net** function. At a minimum the block should contain two items:

- Your email address for use in the from and reply fields of email and for anonymous FTP login
- Your default server; this is also your primary email server

In addition, you can specify a few other items:

- A different incoming email server (for POP)
- A proxy server (for connecting to the network)
- A proxy port number
- A proxy type (see [Proxy Settings](#62361) below).

You can also add lines after the **set-net** function to configure other protocol values. For instance you can set the timeout values for protocols, set the FTP passive mode, set the HTTP user-agent identifier, set up separate proxies for different protocols, and more.

An example of **set-net** is:

```
set-net [user@domain.dom mail.server.dom]

```

The first field specifies your email from address, and the second field indicates your default server (notice that it does not need quotes here). For most networks, this is enough and no other settings are necessary (unless you require a proxy). Also your default server is used whenever a specific server is not provided.

In addition, if you use a POP server (for incoming email) that is different from your SMTP server (for outgoing email), you can specify that as well:

```
set-net [
    user@domain.dom
    mail.server.dom
    pop.server.dom
]

```

However, if your SMTP and POP servers are the same, then this is not necessary.

### 3.2 Proxy Settings

If you use a proxy or firewall, you can provide the set-net function with your proxy settings. This can include the proxy server name or address, a proxy port number to access the server, and an optional proxy type. For example:

```
set-net [
    email@addr
    mail.example.com
    pop.example.com
    proxy.example.com
    1080
    socks
]

```

This example would use a proxy called `proxy`.example.com on its TCP port 1080 with the socks proxy method. To use a socks4 proxy server, use the word `socks4` rather than `socks`. To use the generic CERN server, use the word `generic`.

You can also set the proxy to be different machines for different schemes (protocols). Each protocol has its own proxy object where you can set the proxy values for just that scheme. Here is an example of setting a proxy for FTP:

```
system/schemes/ftp/proxy/host: "proxy2.example.com"

system/schemes/ftp/proxy/port-id: 1080

system/schemes/ftp/proxy/type: 'socks

```

In this case, only FTP uses a special proxy server. Notice that the machine name must be a string and the proxy type must be a literal word.

Here are two more examples. The first example sets the proxy for HTTP to be the generic (CERN) proxy method:

```
system/schemes/http/proxy/host: "wp.example.com"

system/schemes/http/proxy/port-id: 8080

system/schemes/http/proxy/type: 'generic

```

In the above example, all HTTP requests go through a generic proxy on `wp`.example.com using TCP port 8080.

If you want to disable the proxy settings for a particular scheme, you can set the proxy fields to false.

```
system/schemes/smtp/proxy/host: false

system/schemes/smtp/proxy/port-id: false

system/schemes/smtp/proxy/type: false

```

In the above example, all outgoing email does not go through a proxy. The `false` value prevents even the default proxy from being used. If you set these fields to `none`, then the default proxy is used if it is configured.

If you want to bypass the proxy settings for particular machines, such as those on your local network, you can provide a bypass list. Here is a bypass list for the default proxy:

```
system/schemes/default/proxy/bypass:
    ["host.example.net" "*.example.com"]

```

Note that the asterisk (*) and question mark (?) characters can be used for pattern matching. The asterisk (*) as used in the example above bypasses any machine that ends with `example`.com.

To set a bypass list for only the HTTP scheme, type:

```
system/schemes/http/proxy/bypass:
    ["host.example.net" "*.example.com"]

```

### 3.3 Other Settings

In addition to proxy settings, you can set network timeout values for all of the schemes (in the default) or for specific schemes. For instance, to increase the timeout for all schemes, you can write:

```
system/schemes/default/timeout: 0:05

```

This sets the network timeout for 5 minutes.

If you want to increase the timeout just for SMTP, you would write:

```
system/schemes/smtp/timeout: 0:10

```

Some schemes have custom fields. For instance, the FTP scheme allows you to set passive mode for all transfers:

```
system/schemes/ftp/passive: on

```

FTP passive mode is useful because FTP servers that are set to passive mode do not attempt to connect back through your firewall.

When making HTTP accesses to Web sites, you may want to use a different user-agent field in the HTTP request to get better results on a few sites that detect the browser type:

```
system/schemes/http/user-agent: "Mozilla/4.0"

```

### 3.4 Access to Settings

Each time REBOL is started, it reads the `user`.r file to find its network settings. These settings are made with the **set-net** function. Scripts have access to these settings through the `system/schemes` object.

```
system/user/email ; used for email from and reply
system/schemes/default/host - your primary server
system/schemes/pop/host - your POP server
system/schemes/default/proxy/host - proxy server
system/schemes/default/proxy/port-id - proxy port
system/schemes/default/proxy/type - proxy type

```

Below is a function that returns a block containing the network settings in the same order as **set-net** accepts them:

```
get-net: func [][
    reduce [
        system/user/email
        system/schemes/default/host
        system/schemes/pop/host
        system/schemes/default/proxy/host
        system/schemes/default/proxy/port-id
        system/schemes/default/proxy/type
    ]
]

probe get-net

```

## 4. DNS - Domain Name Service

DNS is the network service that translates domain names to their associated IP address. In addition, you can use DNS to find a machine and domain name from an IP address.

The DNS protocol can be used in three ways: you can lookup the primary IP address of a machine name, you can lookup the domain name for an IP address, and you can find the name and IP address of your local system.

To lookup the primary IP address of a specific machine within a specific domain, type:

```
print read dns://www.rebol.com
207.69.132.8

```

You can also obtain the domain name that is associated with a particular IP address:

```
print read dns://207.69.132.8
rebol.com

```

Note that it is not unusual for this reverse DNS lookup to return a none. There are machines that do not have host names.

```
print read dns://11.22.33.44
none

```

To find your system's host name, read an empty DNS URL of the form:

```
print read dns://
crackerjack

```

The data returned here depends on the type of machine. It may be the unqualified host name, as shown above, but it can also be the fully-qualified host name, `crackerjack`.example.com. This depends on the operating system and the network configuration in the operating system.

Here's an example that looks up and prints the IP addresses for a number of Web sites:

```
domains: [
    www.rebol.com
    www.rebol.org
    www.mochinet.com
    www.sirius.com
]

foreach domain domains [
    print ["address for" domain "is:"
        read join dns:// domain]
]
address for www.rebol.com is: 207.69.132.8
address for www.rebol.org is: 207.66.107.61
address for www.mochinet.com is: 216.127.92.70
address for www.sirius.com is: 205.134.224.1

```

## 5. Whois Protocol

The whois protocol retrieves information about domain names from a central registry. The whois service is provided by the organizations that run the Internet. Whois is often used to retrieve registration information about an Internet domain or server. It can tell you who owns the domain, how their technical contact can be reached, along with other information.

To obtain information, use the **read** function with a whois URL. This URL should contain the domain name and a whois server name separated by an at sign (@). For example to obtain information about `example`.com from the Internic registry:

```
print read whois://example.com@rs.internic.net
connecting to: rs.internic.net
Whois Server Version 1.1
Domain names in the .com, .net, and .org domains can now be
registered with many different competing registrars. Go to
http://www.internic.net for detailed information.
Domain Name: EXAMPLE.COM
Registrar: NETWORK SOLUTIONS, INC.
Whois Server: whois.networksolutions.com
Referral URL: www.networksolutions.com
Name Server: NS.ISI.EDU
Name Server: VENERA.ISI.EDU
Updated Date: 17-aug-1999
>>> Last update of whois database: Sun, 16 Jul 00 03:16:34 EDT <<<
The Registry database contains ONLY .COM, .NET, .ORG, .EDU domains
and Registrars.

```

*The above code is only an example. The details of the information being returned and the servers that support whois change over time.*

If instead of a domain name you provide a word, all entries that match that word are returned:

```
print read whois://example@rs.internic.net
connecting to: rs.internic.net
Whois Server Version 1.1
Domain names in the .com, .net, and .org domains can now be
registered with many different competing registrars. Go to
http://www.internic.net for detailed information.
EXAMPLE.512BIT.ORG
EXAMPLE.ORG
EXAMPLE.NET
EXAMPLE.EDU
EXAMPLE.COM
To single out one record, look it up with "xxx", where xxx is one
of the of the records displayed above. If the records are the same, look them
up with "=xxx" to receive a full display for each record.
>>> Last update of whois database: Sun, 16 Jul 00 03:16:34 EDT <<<
The Registry database contains ONLY .COM, .NET, .ORG, .EDU domains
and Registrars.

```

*The whois protocol does not accept URLs, such as www.example.com, unless the URL is part of the registrant's company name.*

## 6. Finger Protocol

The finger protocol retrieves user-specific information stored in the user log file.

To request user information from a server it must be running the finger protocol. The information is requested by reading a finger URL that contains a username and a domain name in an email style format:

```
print read finger://username@example.com

```

The above example retrieves information about the user at `username@example`.com. The information returned depends on the information provided by the user and the settings of the finger server. Also, the details of the information being returned are up to each server; the examples below only describe typical servers. Many servers can have non-standard behaviors on their finger ports.

For instance, the following information may be returned:

```
Login: username
Name: Firstname Lastname
Directory: /home/user
Shell: /usr/local/bin/tcsh
Office: City, State +1 555 555 5555
Last login Wed Jul 28 01:10 (PDT) on ttyp0 from some.example.com
No Mail.
No Plan.

```

Notice that finger reports when the user last logged in from a machine, and whether the user has mail waiting. If the user reads email from this account, finger sometimes reports when mail was received and when the user last retrieved email:

```
New mail received Sun Sep 26 11:39 1999 (PDT)
Unread since Tue Sep 21 04:45 1999 (PDT)

```

The finger server can also report the contents of a `plan` file and a `project` file if they exist. Users can include any information they want in a `plan` or `project` file.

It is also possible to retrieve information about users using their real first name or their last name. Some finger servers require that you capitalize the names exactly as they appear in the login file or in the file used by the online finger server, to retrieve user information. Other finger servers are more liberal about capitalization. A finger server will respond to real name queries by returning all listings that match the query criteria. For instance, if there are several users on a host that have the first name `zaphod`, then entering the query

```
print read finger://Zaphod@main.example.com

```

will retrieve all such users whose first or last name is `Zaphod`.

Some finger servers return a listing of users when the user name is omitted. For example,

```
print read finger://main.example.com

```

retrieves a list of all users who are logged onto the machine, if the finger service installed on the hosting machine allows it.

Some host machines limit finger services for security reasons. They may require a valid username and only return information regarding that user. If you finger such a server without providing user information, the server will report that it requires specific user information.

If a system does not support the finger protocol, REBOL reports an access error:

```
print read finger://host.dom
connecting to: host.dom
Access Error: Cannot connect to host.dom.
Where: print read finger://host.dom

```

## 7. Daytime - Network Time Protocol

The daytime protocol retrieves the current day and time. To connect to a daytime server use **read** with a daytime URL. The URL contains the name of the server to read the date from:

```
print read daytime://everest.cclabs.missouri.edu
Fri Jun 30 16:40:46 2000

```

The format of the information returned by servers may vary, depending on the server. Notice that the time zone may not be present.

If the server you choose does not support daytime, REBOL returns an error:

```
print read daytime://www.example.com
connecting to: www.example.com
** Access Error: Cannot connect to www.example.com.
** Where: print read daytime://www.example.com

```

## 8. HTTP - Hyper Text Transfer Protocol

The world wide Web is driven by two fundamental technologies: HTTP and HTML. HTTP is the Hypertext Transfer Protocol that controls how Web servers and Web browsers communicate with each other. HTML is the Hypertext Markup Language that defines the structure and contents of a Web page.

To retrieve a Web page, the browser sends a request to a Web server using HTTP. On receiving the request, the server interprets it, sometimes using a CGI script (see [CGI - Common Gateway Interface](#_Toc487519913)), and sends back data. This data can be just about anything, including HTML, text, images, programs, and sound.

### 8.1 Reading a Web Page

To read a Web page, use the **read** function with an HTTP URL. For example:

```
page: read http://www.rebol.com

```

This returns the Web page for `www`.rebol.com. Note that a string that contains the HTML code for the page is returned by the read. No graphics or other information are fetched. To do so you would need to provide additional reads. The page can be displayed as HTML code using **print**, it can be written to a file with **write**, or it can be sent as email using **send**.

```
print page

write %index.html page

send zaphod@example.com page

```

The page can be processed in a variety of ways by using a variety of REBOL functions, such as **parse**, **find**, and**load**.

For instance, to search a Web page for all occurrences of the word `REBOL`, you can write:

```
parse read http://www.rebol.com [
    any [to "REBOL" copy line to newline (print line)]
]

```

### 8.2 Scripts on Web Sites

A Web server can provide more than just HTML scripts. Web servers are quite useful for supplying REBOL scripts as well.

You can load REBOL scripts directly from a Web server with **load:**

```
data: load http://www.rebol.com/data.r

```

You can also evaluate scripts directly from a server with **do:**

```
data: do http://www.rebol.com/code.r

```

**Warning**

Do this with care. Evaluating arbitrary scripts on open Internet servers is asking for trouble. Evaluate a script only if you completely trust its source, have fully inspected its source, or have kept your REBOL security settings on maximum.

In addition, Web pages that contain HTML can contain embedded REBOL scripts, and they can be run with:

```
data: do http://www.rebol.com/example.html

```

To determine if a script exists on a page before evaluating it, use the **script?** function.

```
if page: script? http://www.rebol.com [do page]

```

The **script?** function reads the page from the Web site and returns the page at its REBOL header position.

### 8.3 Loading Markup Pages

HTML and XML pages can be quickly converted to a REBOL block with the **load/markup** function. This function returns a block that consists of all the tags and strings found within the page. All spacing and line breaks are left intact.

To filter out all of the tags for a Web page and just print its text, type:

```
tag-text: load/markup http://www.rebol.com
text: make string! 2000

foreach item tag-text [
    if string? item [append text item]
]

print text

```

You could then search this text for string patterns. It will contain all of the spaces and line breaks of the original HTML file.

Here's another example that checks all links found on a Web page to make sure that the pages they reference exist:

```
REBOL []

page: http://www.rebol.com/developer.html
set [path target] split-path page
system/options/quiet: true  ; turn off connection msgs
tag-text: load/markup page
links: make block! 100

foreach tag tag-text [  ; find all anchor href tags
    if tag? tag [
        if parse tag [
            "A" thru "HREF="
            [{"} copy link to {"} | copy link to ">"]
            to end
        ][
            append links link
        ]
    ]
]

print links

foreach link unique links [  ; try each link
    if all [
        link/1 <> #"#"
        any [flag: not find link ":"
             find/match link "http:"]
    ][
        link: either flag [path/:link][to-url link]
        prin [link "... "]
        print either error? try [read link]
            ["failed"]["OK"]
    ]
]

```

### 8.4 Other Functions

To check if a Web page exists, use the **exists?** function, which returns `true` if the page exists.

```
if exists? http://www.rebol.com [
    print "page still there"
]

```

*Note: It is usually faster in many cases to just read the page rather than checking first to see if it exists. Otherwise the script must contact the server twice, and that can be time consuming.*

To request the date on which a Web page was last modified, use the **modified?** function:

```
print modified? http://www.rebol.com/developer.html

```

However, note that not all Web servers provide modification date information. Dynamically generated Web pages typically do not return a modification date.

Another way to determine if a Web page has changed is poll it every so often and check it. A handy way to verify that a Web page has changed is by using the **checksum** function. If the previously calculated checksum of a Web page differs from its current value, then the Web page has been modified since it was last checked. Here is an example that uses this technique. It checks a page every eight hours.

```
forever [
    page: read http://www.rebol.com
    page-sum: checksum page
    if any [
        not exists? %page-sum
        page-sum <> (load %page-sum)
    ][
        print ["Page changed" now]
        save %page-sum page-sum
        send luke@rebol.com page
    ]
    wait 8:00
]

```

Whenever the page changes, it is sent to Luke via email.

### 8.5 Acting Like a Browser

Normally, REBOL identifies itself to a server when it reads from a Web site. However, some servers are programmed to respond to particular browsers only. If a request to a server does not produce the correct Web page, you can change the request to make it look like it came from some other type of Web browser. Pretending to be a Web browser is done by many programs to get Web sites to respond correctly. However, this practice does end up defeating the purpose behind the browser identification.

To change HTTP requests to look as though they are being sent by Netscape 4.0, you can modify the user-agent within the HTTP handler:

```
system/options/http/user-agent: "Mozilla/4.0"

```

Setting this variable affects all HTTP requests that follow.

### 8.6 Posting CGI Requests

HTTP CGI requests can be posted in two ways. You can include the CGI request data in the URL or you can provide the request data through an HTTP post operation.

The URL CGI request uses a normal URL. The example below sends the CGI script `test`.r the data value of 10.

```
read http://www.example.com/cgi-bin/test.r?data=10

```

The post CGI request requires that you supply the CGI data as part of a custom refinement to the **read** function. The example below shows how data is posted to CGI:

```
read/custom http://www.example.com/cgi-bin/test.r [
    post "data: 10"
]

```

In this example, the **/custom** refinement is used to provide additional information to the read. The second argument is a block that begins with the word **post** and is followed by the string to send.

The post method is useful for easily sending REBOL code and data to a web server that runs CGI. The following example illustrates this:

```
data: [sell 10 shares of "ACME" at $123.45]

read/custom http://www.example.com/cgi-bin/test.r reduce [
    `post mold data
]

```

The mold function will produce the proper REBOL string to be sent to the server.

## 9. SMTP - Simple Mail Transport Protocol

The Simple Mail Transport Protocol (SMTP) controls the transfer of email messages on the Internet. SMTP defines the interaction between Internet hosts that participate in forwarding email from a sender to its destination.

### 9.1 Sending Email

Email is sent through SMTP by using the **send** function. This function can send an email message to one or more email addresses.

For **send** to operate correctly, your networking must be set up. The **send** function requires that you specify your email From address and your default email server. See [Initial Setup](#_Toc487519877) above.

The **send** function takes two arguments: an email address and a message. For example:

```
send user@example.com "Hi from REBOL"

```

The first argument must be an email or block data type. The second argument can be any data type.

```
send luke@rebol.com $1000.00

send luke@rebol.com 10:30:40

send luke@rebol.com bill@ms.dom

send luke@rebol.com [Today 9-Apr-99 10:30]

```

Each of these simple email messages can be interpreted on the receiver's side (with REBOL) or viewed with a normal email program.

You can send an entire file by reading the file and passing it as the second argument to the send function:

```
send luke@rebol.com read %task.txt

```

Binary data, such as an image or executable file, can also be sent:

```
send luke@rebol.com read/binary %rebol

```

The binary data is encoded to allow it to be transferred as text.

To send a self-extracting binary message you can write:

```
send luke@rebol.com join "REBOL for the job" [
    newline "REBOL []" newline
    "write/binary %rebol decompress "
    compress read/binary %rebol
]

```

When the message is received, the file can be extracted by using the **do** function.

### 9.2 Multiple Recipients

To send to multiple recipients, you can provide a block of email names:

```
send [luke@rebol.com ben@example.com] message

```

In this case, each message is individually addressed with only the recipient's email name appearing in the `To` field (similar to BCC addressing).

The block of email addresses can be any size or even a file that you load. Just be sure that they are valid addresses, not strings. Strings are ignored.

```
friends: [
    bob@cnn.dom
    betty@cnet.dom
    kirby@hooya.dom
    belle@apple.dom
    ...
]

send friends read %newsletter.txt

```

### 9.3 Bulk Mail

If you are sending email to a large group, you can reduce the load on your server by delivering everyone in the group a single message. This is the purpose of the **/only** refinement. It uses a feature of SMTP to send only one message to multiple email addresses. Using the friends list from the previous example:

```
send/only friends message

```

The messages are not individually addressed. You may have seen this mode in some of the bulk email that you receive. When you receive bulk email, your address does not appear in the `To` field.

The bulk email mode of SMTP should be used for email lists and not for sending spam. Spam email is not proper network etiquette, it is illegal in some countries and states, and spam will get you banned from your ISP and from other sites.

### 9.4 Subject Line and Headers

By default the **send** function uses the first line of a message as the subject line. To provide your own subject line, you need to supply an email header to the **send** function. In addition to a subject line, you can provide an organization, date, CC, and even your own custom fields.

To include a header, use the **/header** refinement of the **send** function and include a header object. The header object must be made from the `system/standard/email` object. For example:

```
header: make system/standard/email [
    Subject: "Seen REBOL yet?"
    Organization: "Freedom Fighters"
]

```

Notice that the standard fields, such as the `From` address, are not required and are supplied automatically by the **send** function.

The header is then provided as an argument to **send/header:**

```
send/header friends message header

```

The email above is sent using the custom header for each message.

### 9.5 Debug Your Scripts

When testing email scripts, it is advised that you send email to yourself first, before sending it to others. Examine your test email carefully to make sure that it is what you want. It is common to have errors such as sending a file name rather than the file contents. For instance, you might write:

```
send person %the-data-file.txt

```

This sends the name of the file, not the file itself.

## 10. POP - Post Office Protocol

The Post Office Protocol (POP) allows you to fetch email that is waiting in a mail server mailbox. POP defines a number of operations for how to access and store email on your server.

### 10.1 Reading Email

You can read all of your email in a single line without removing it from the email server: This is done by reading from a POP URL in which you provided your username, password, and email host.

```
mail: read pop://user:pass@mail.example.com

```

The messages are returned as a block of strings which you can handle one message at a time using code such as:

```
foreach message mail [print message]

```

To read individual email messages from the server, you need to open a port connection to the server and handle each message one at a time. To open the POP port:

```
mailbox: open pop://user:pass@mail.example.com

```

In the example, `mailbox` can be accessed as a series. It responds to many of the standard series functions, such as **length?**, **first**, **second**, **third**, **pick**, **next**, **back**, **head**, **tail**, **head?**, **tail?**, **remove**, and **clear**.

To determine the number of mail messages residing on the server, use the **length?** function.

```
print length? mailbox
37

```

In addition, you can find out the total size of all messages and the individual sizes of messages with:

```
print mailbox/locals/total-size

print mailbox/locals/sizes

```

To display the first, second, and last messages, you can write:

```
print first mailbox

print second mailbox

print last mailbox

```

You can also use **pick** to fetch a specific message:

```
print pick mailbox 27

```

You can fetch and display each message from the oldest to the newest using a loop that is identical to that used for other types of series:

```
while [not tail? mailbox] [
    print first mailbox
    mailbox: next mailbox
]

```

You can also read your email from newest to oldest with a loop such as:

```
mailbox: tail mailbox

while [not head? mailbox] [
    mailbox: back mailbox
    print first mailbox
]

```

When you are done, be sure to **close** the mailbox. This can be done with a line such as:

```
close mailbox

```

### 10.2 Removing Email

As with series, the **remove** function can be used to delete a single message, and the **clear** function can be used to delete all of the messages from the current position to the end of the mailbox.

For example, to read a message, save it to a file, and remove it from the server:

```
mailbox: open pop://user:pass@mail.example.com
write %mail.txt first mailbox
remove mailbox
close mailbox

```

The message is removed from the server when the **close** is done.

To remove the 22nd email message from the server, you can write:

```
user:pass@mail.example.com
remove at mailbox 22
close mailbox

```

You can remove a number of messages by using the **/part** refinement with the remove function:

```
remove/part mailbox 5

```

To remove all of the messages in your mailbox, use the **clear** function:

```
mailbox: open pop://user:pass@example.com
clear mailbox
close mailbox

```

The **clear** function can also be used at different positions within the mailbox to remove messages to the end of the mailbox.

### 10.3 Handling Email Headers

Email messages always include a header. The header holds information such as the sender, recipient, subject, date, and other fields.

In REBOL email headers are handled as objects that contain all of the necessary fields. To convert email message to a header object you can use the **import-email** function. For example:

```
msg: import-email first mailbox

print first msg/from  ; the email address
print msg/date
print msg/subject
print msg/content

```

You can easily write a filter that scans your email for messages that begin with a particular subject line:

```
mailbox: open pop://user:pass@example.com

while [not tail? mailbox] [
    msg: import-email first mailbox
    if find/match msg/subject "[REBOL]" [
        print msg/subject
    ]
    mailbox: next mailbox
]

close mailbox

```

Here is another example that informs you when email is received from a group of friends:

```
friends: [orson@rebol.com hans@rebol.com]

messages: read pop://user:pass@example.com

foreach message messages [
    msg: import-email message
    if find friends first msg/from [
        print [msg/from newline msg/content]
        send first msg/from "Got your email!"
    ]
]

```

This spam filter removes all messages from the server that do not contain your email name anywhere within the message:

```
mailbox: open pop://user:pass@example.com

while [not tail? mailbox] [
    mailbox: either find first mailbox user@example.com
        [next mailbox][remove mailbox]
]

close mailbox

```

Here is a simple email list server that receives messages and sends them to a group. The server only accepts email from people in the group.

```
group: [orson@rebol.com hans@rebol.com]

mailbox: open pop://user:pass@example.com

while [not tail? mailbox] [
    message: import-email first mailbox
    mailbox: either find group first message/from [
        send/only group first mailbox
        remove mailbox
    ][next mailbox]
]

close mailbox

```

## 11. FTP - File Transfer Protocol

The File Transfer Protocol (FTP) is used widely on the Internet for transferring files to and from a remote host. FTP is commonly used for uploading pages to a Web site and for providing online file archives.

### 11.1 Using FTP

In REBOL FTP file operations are handled in much the same way as local file operations. Functions such as **read**, **write**, **load**, **save**, **do**, **open**, **close**, **exists?**, **size?**, **modified?**, and others are used with FTP. REBOL distinguishes between local files and files accessible by FTP through the use of an FTP URL.

Access to FTP servers can be open or closed. Open access allows anyone to login to the site and download files. This is called anonymous access and it is used frequently for public file archives. Closed access requires that you provide a username and password to download and upload files. This is the mode of operation for uploading Web pages to a Web site.

Although FTP does not require your REBOL networking to be configured, if you wish to use anonymous access, an email address is required. This address is found in the `system/user/email` object. Normally, when you boot REBOL, this field is set from your `user`.r file. See [Initial Setup](#_Toc487519877) for more detail.

If you are using FTP through a proxy server or firewall, FTP may need to operate in passive mode. Passive mode does not require reverse connections from the FTP server to the client for data transfers. This mode only makes outgoing connections from your machine and allows a greater level of security. To enable passive mode you need to set a flag in the FTP protocol handler:

```
system/schemes/ftp/passive: true

```

If you do not know if it is necessary, try FTP first without it. If that does not work, try setting the passive flag.

### 11.2 FTP URLs

An FTP URL has the basic form:

```
ftp://user:pass@host/directory/file

```

For anonymous access the username and password can be left out:

```
ftp://host/directory/file

```

Most of the examples in this section use this form for simplicity; however, they also work with a username and password.

To access a remote directory, end the URL with a slash, such as:

```
ftp://user:pass@host/directory/

ftp://host/directory/

ftp://host/

```

More about directory access is shown below.

It is convenient to put the URL in a variable and use paths to provide the file names. This allows you to refer to the URL with just a word. For example:

```
site: ftp://ftp.rebol.com/pub/

read site/readme.txt

```

This technique is used in some of the sections that follow.

### 11.3 Transferring Text Files

FTP distinguishes between text files and binary files. When transferring text files, FTP converts the line break characters. This is not desirable for binary files.

To read a text file, supply the **read** function with an FTP URL:

```
file: read ftp://ftp.site.com/file.r

```

This puts the contents of the file into a string. To write the file locally, use this line:

```
write %file.r read ftp://ftp.site.com/file.r

```

Many of the refinements of **read** can also be used. For instance, you can use **read/lines** with:

```
data: read/lines ftp://ftp.site.com/file.r

```

This example returns a block of lines for the file. See the [Files](rebolcore-12.html#_Toc487519750) chapter for more information about the refinements to the **read** function.

To write a text file to the server, use the **write** function:

```
write ftp://ftp.site.com/file.r read %file.r

```

The **write** function can also include refinements. See the [Files](rebolcore-12.html#_Toc487519750) chapter.

As with normal text file transfers, all line termination will be properly converted during FTP transfers.

Here is a simple script that updates files to your Web site:

```
site: ftp://wwwuser:secret@www.site.dom/pages

files: [%index.html %home.html %info.html]

foreach file files [write site/:file read file]

```

This should not be used for transferring graphics or sound files, as they are binary. Use the technique shown in [Transferring Binary Files](#28819).

In addition to the **read** and **write** functions, you can use the **load**, **save**, and **do** functions with FTP.

```
data: load ftp://ftp.site.com/database.r

save ftp://ftp.site.com/data.r data-block

do ftp://ftp.site.com/scripts/test.r

```

### 11.4 Transferring Binary Files

To avoid the line termination conversion when transferring binary files (images, archives, executable files), use the **/binary** refinement. For instance, to read a binary file from an FTP server:

```
data: read/binary ftp://ftp.site.com/file

```

To make a local copy of the file:

```
write/binary %file read/binary ftp://ftp.site.com/file

```

To write a binary file to a server:

```
write/binary ftp://ftp.site.com/file read/binary %file

```

No line termination conversions are performed.

To transfer a set of graphics files to a Web site, use this script:

```
site: ftp://user:pass@ftp.site.com/www/graphics

files: [%icon.gif %logo.gif %photo.jpg]

foreach file files [
    write/binary site/:file read/binary file
]

```

### 11.5 Appending to Files

FTP also allows you to append text and data to an existing file. To do so, use the **write/append** refinement as described in the [Files](rebolcore-12.html#_Toc487519750) chapter.

```
write/append ftp://ftp.site.com/pub/log.txt reform
    ["Log entry date:" now newline]

```

This can also be used with binary files.

```
write/binary/append ftp://ftp.site.com/pub/log.txt
    read/binary %datafile

```

### 11.6 Reading Directories

To read the file names of an FTP directory, follow the directory name with a forward slash:

```
print read ftp://ftp.site.com/

pub-files: read ftp://ftp.site.com/pub/

```

The ending forward slash (/) indicates that this is a directory access not a file access. The forward slash is not always required, but it is recommended when you know you are accessing a directory.

The block of files that is returned includes all of the files in the directory. Within that block, directory names are indicated with a forward slash following their names. For example:

```
foreach file read ftp://ftp.site.com/pub/ [
    print file
]
readme.txt
rebol.r
rebol.exe
library/docs/

```

You can also use the **dir?** function on a file to determine if it is a directory.

### 11.7 File Information

The same functions that provide information about files also provide information about FTP files. This includes the**modified?**, **size?**, **exists?**, **dir?**, and **info?** functions.

You can use the **exists?** function to determine if a file exists:

```
if exists? ftp://ftp.site.com/pub/log.txt [
    print "Log file is there"
]

```

This works for directories too, but include the forward slash at the end of the directory name:

```
if exists? ftp://ftp.site.com/pub/rebol/ [
    print read ftp://ftp.site.com/pub/rebol/
]

```

To get the size or modification date for a file:

```
print size? ftp://ftp.site.com/pub/log.txt

print modified? ftp://ftp.site.com/pub/log.txt

```

To determine if the file is actually a directory:

```
if dir? ftp://ftp.site.com/pub/text [
    print "It's a directory"
]

```

You can obtain all this information in a single access by using the **info?** function:

```
file-info: info? ftp://ftp.site.com/pub/log.txt

probe file-info

print file-info/size

```

To perform the same operation on a directory:

```
probe info? ftp://ftp.site.com/pub/

```

To print a directory listing:

```
files: open ftp://ftp.site.com/pub/

forall files [
    file: first files
    info: info? file
    print [file info/date info/size info/type]
]

```

### 11.8 Making Directories

New FTP directories can be created with the **make-dir** function:

```
make-dir ftp://user:pass@ftp.site.com/newdir/

```

### 11.9 Deleting Files

With appropriate permission settings, files can be deleted from a remote FTP server by using the **delete** function:

```
delete ftp://user:pass@ftp.site.com/upload.txt

```

You can also delete directories:

```
delete ftp://user:pass@ftp.site.com/newdir/

```

Note that a directory must be empty for this to succeed.

### 11.10 Renaming Files

You can **rename** a file with the line:

```
rename ftp://user:pass@ftp.site.com/foo.r %bar.r

```

The new name for the file will be `bar`.r.

FTP also allows you to move a file to a different directory with:

```
rename ftp://user:pass@ftp.site.com/foo.r %pub/bar.r

```

To rename a directory on an FTP site be sure to follow the directory name with a slash:

```
rename ftp://user:pass@ftp.site.com/rebol/ rebol-old/

```

### 11.11 About Passwords

The above examples include the password within their URLs, but if you plan on sharing your script, you probably don't want that information to be known. Here's a simple way to prompt for a password and build the correct URL:

```
pass: ask "Password? "

data: read join ftp://user: [pass "@ftp.site.com/file"]

```

Or, you can ask for both the username and password:

```
user: ask "Username? "
pass: ask "Password? "
data: read join ftp:// [
    user ":" pass "@ftp.site.com/file"
]

```

You can also open FTP connections by using a port specification rather than a URL. This allows you to use any password, even ones containing special characters that are not easily written in URLs. An example of a port specification to open an FTP connection is:

```
ftp-port: open [
    scheme: `ftp
    host: "ftp.site.com"
    user: ask "Username? "
    pass: ask "Password? "
]

```

See [Specifying Network Resources](#40832) above for more detail.

### 11.12 Transferring Large Files

Transferring large files requires special considerations. You may want to transfer the file in chunks to reduce the memory required by your computer and to provide user feedback while the transfer is happening.

Here is an example that downloads a very large binary file in chunks.

```
inp: open/binary/direct ftp://ftp.site.com/big-file.bmp
out: open/binary/new/direct %big-file.bmp
buf-size: 200000
buffer: make binary! buf-size + 2

while [not zero? size: read-io inp buffer buf-size][
    write-io out buffer size
    total: total + size
    print ["transferred:" total]
]

```

Be sure to use the **/direct** refinement, otherwise the entire file will be buffered internally by REBOL. The **read-io** and **write-io** functions allow reuse of the buffer memory that has already allocated. Other functions such as **copy** would allocate additional memory.

If the transfer fails, you can restart FTP from where it left off. To do so, examine the output file or the size variable to determine where to restart the transfer. Open the file again with a custom refinement that specifies **restart** and the location from which to start the read. Here is an example of the **open** function to use when the `total` variable indicates the length already read:

```
inp: open/binary/direct/custom
    ftp://ftp.site.com/big-file.bmp
    reduce ['restart total]

```

You should note that restart only works for binary transfers. It cannot be used with text transfers because the line terminator conversion that takes place will cause incorrect offsets.

## 12. NNTP - Network News Transfer Protocol

The Network News Transfer Protocol (NNTP) is the basis for tens of thousands of newsgroups that provide a public forum for millions of Internet users. REBOL includes two levels of support for NNTP.

The built-in support for NNTP that provides very limited functionality and access. This is the NTTP scheme.

An extended level of functionality that is provided by the news scheme that is implemented in the file distributed as `nntp`.r.

### 12.1 Reading the Newsgroup List

NNTP consists of two components: a list of newsgroups supported by a specific newsgroup server (newsgroups are typically selected by an Internet service provider); and, a database of messages that are currently available for any particular newsgroup.

To retrieve the list of all newsgroups from a specific news server, use the **read** function with an NNTP URL such as:

```
groups: read nntp://news.example.com

```

This may take a while, depending on your connection; there are thousands of newsgroups.

### 12.2 Reading All Messages

If you are using a fast connection, you can read all of the pending messages for a newsgroup with:

```
messages: read nntp://news.example.com/alt.test

```

However, caution is advised. Some newsgroups can have thousands of messages. It can take a long time to download all the messages, and you may run out of memory to hold them.

### 12.3 Reading Single Messages

To read single messages, open NNTP as a port and use series functions to access messages. This is similar to how you read email from a POP port. For example:

```
group: open nntp://news.example.com/alt.test

```

You can use the **length?** function to determine the number of messages that are available in the newsgroup:

```
print length? group

```

To read the first message available in the newsgroup, use **first:**

```
message: first group

```

To select a specific message in the group by index, use **pick:**

```
message: pick group 37

```

To create a simple loop that scans all messages for a keyword, use:

```
forall group [
    if find msg: first first group "REBOL" [
        print msg
    ]
]

```

Remember that when the loop returns, the group series is positioned to the tail. If you need to return to the head of the group:

```
group: head group

```

Be sure to **close** a port once you are done using it:

```
close group

```

### 12.4 Handling News Headers

News messages always include a header. The header holds information such as the sender, summary, keywords, subject, date, and other fields.

Headers are handled as objects. To convert a news message to a news header object you can use the **import-email** function. For example:

```
message: first first group
header: import-email message

```

You can now access the fields of the news message:

```
print [header/from header/subject header/date]

```

Different newsgroups and newsgroup clients use different fields in their header. To view the fields available for a specific message display the first item of the header object:

```
print first header

```

### 12.5 Sending a News Message

Before you can send a news message, you need to create a header for it. Here is a generic header that can be used for news:

```
news-header: make object! [
    Path: "not-for-mail"
    Sender: Reply-to: From: system/user/email
    Subject: "Test message"
    Newsgroups: "alt.test"
    Message-ID: none
    Organization: "Docs For All"
    Keywords: "Test"
    Summary: "A test message"
]

```

Before you can send it, you need to create a unique global identification number for it. Here is a function that does that:

```
make-id: does [
    rejoin [
        "<"
        system/user/email/user
        "."
        checksum form now
        "."
        random 999999
        "@"
        read dns://
        ">"
    ]
]

print news-header/message-id: make-id
<carl.4959961.534798@fred.example.com>

```

Now you can combine the header with the message. They must be separated by at least one blank line. The content of the message is read from a file.

```
write nntp://news.example.net/alt.test rejoin [
    net-utils/export news-header
    newline newline
    read %message.txt
    newline
]

```

## 13. CGI - Common Gateway Interface

The common gateway interface is used with many Web servers to provide processing beyond the normal HTTP Web interface. CGI requests are submitted from Web browsers to Web servers. When a server receives a CGI request, it typically executes a script to process the request and return a result to the browser. These CGI scripts can be written in a variety of languages, and REBOL provides one of the easier ways of handling CGI.

### 13.1 CGI Server Setup

Setting up CGI access is different for every Web server. See the instructions provided with your server.

Typically a server has an option for enabling CGI operation. You need to enable this option and provide a path to the directory where your CGI scripts reside. A common directory for CGI scripts is in `cgi-bin`.

On Apache servers, the `ExecCGI` option enables CGI scripts, and you can provide a directory (`cgi-bin` ) for your scripts. This is normally set up by default installation of Apache.

To configure CGI for Microsoft IIS, go to the `properties` for cgi-bin and click on the `configuration` button. On the configuration panel click `add` and enter the path to your `rebol`.exe file. The format for this is:

```
C:\rebol\rebol.exe -cs %s %s

```

The two `%s` symbols are required for correctly passing the script and command line arguments to REBOL. Add the extension for REBOL files (``.r ) and set the last field to `PUT`, `DELETE`. The script engine does not need to be selected.

The -`cs` option that is provided to REBOL enables CGI operation and allows the script to access all files. (!!See notes below on how scripts can limit file access to selected directories).

With Web servers other than those described above, the server requires configuration to execute the REBOL executable for ``.r extension files and run REBOL with the required option `-cs`.

### 13.2 CGI Scripts

Before a script can be executed on most CGI servers, it needs to have the correct file permissions. On UNIX-type systems or those that use the Apache server you need to change the permissions to enable the script to be readable and executable by all users. This can be done with the **chmod** function. If you are new to this concept, you should read your operating system manual or talk with your system administrator before changing file permissions.

For Apache and various other Web servers to run REBOL scripts, you need to provide the correct header at the top of each script file. The header specifies the path to the REBOL executable file and the `-cs` option. This can be followed by the normal REBOL script header. Here is a simple CGI script that prints the string, `hello!`.

```
#!/path/to/rebol -cs

REBOL [Title: "CGI Test Script"]

print "Content-Type: text/plain"

print ""  ; required

print "Hello!"

```

There are many things that prevent a CGI script from running correctly. Get this simple script working first before you try more complex scripts. If your script does not work, here are a few items to check:

- You have CGI enabled on your Web server.
- The first line begins with a #! and the correct path to REBOL.
- The -cs option is supplied to REBOL.
- The script begins with "Content-Type:" being printed. (!!see below)
- The script is in the correct directory. (normally the cgi-bin directory)
- The script has the correct file permissions (readable and executable by all).
- The script contains the correct line break characters. Some servers do not run scripts that contain the CR character for line breaks. You may need to convert the file. (Use REBOL to do this in one line: write file, read file).
- The script does not contain errors. Test it without CGI to make sure that the script loads (does not have syntax errors) and functions properly. Provide some sample data and test it.
- All files that are accessed by the script have the correct file permissions.

Often one or more of the above items is wrong and prevent your script from running. You may see an error when viewing the Web page. If it says "Server Error" or "CGI Error" then it is typically something to do with the permissions or setup of the script. If it shows a REBOL error message, then the script is running, but you have an error within the script.

In the example script shown above, the `Content-Type` line is critical. It is part of the HTTP header that is returned to the browser, and it tells the browser the type of content being delivered. This is followed by a blank line to separate it from the actual content.

Many different types of content can be delivered. The previous example was plain text, but you can also deliver HTML as is shown in the next example. (See your Web server manual for more information about content types.)

The content type and blank line can be combined into a single line. The caret forward slash `(^/`) symbol provides an additional line break to separate it from the content.

```
print "Content-Type: text/plain^/"

```

It is a good practice to always print this line immediately from your script. This allows error messages to be seen by the browser if your script encounters an error.

Here is a simple CGI script that prints the time:

```
#!/path/to/rebol -cs

REBOL [Title: "Time Script"]

print "Content-Type: text/plain^/"

print ["The time is now" now/time]

```

### 13.3 Generating HTML Content

There are as many ways to create HTML content as there are ways to create strings. This page creates a page that displays a page hit counter:

```
#!/path/to/rebol -cs

REBOL [Title: "HTML Example"]

print "Content-Type: text/html^/"

count: either exists? %counter [load %counter][0]
save %counter count: count + 1

print [
    {<HTML><BODY><H2>Web Counter Page</H2>
    You are visitor} count {to this page!<P>
    </BODY></HTML>}
]

```

The script in the example above loads and saves to a counter text file. For this file to be accessible, it will require the appropriate permissions be set to allow access by all users.

### 13.4 CGI Environment

When a CGI script is run the server provides information to REBOL about the CGI request and its arguments. All of this information is provided as an object within the `system/options` object. To view the fields of the object, type:

```
probe system/options/cgi
make object! [
    server-software: none
    server-name: none
    gateway-interface: none
    server-protocol: none
    server-port: none
    request-method: none
    path-info: none
    path-translated: none
    script-name: none
    query-string: none
    remote-host: none
    remote-addr: none
    auth-type: none
    remote-user: none
    remote-ident: none
    Content-Type: none
    content-length: none
    other-headers: []
]

```

Of course, your script will ignore most of this information, but some of it could be of use. For instance, you may want to create a log file that records the network address of the system that made the request, or check the type of browser being used.

To generate a CGI page that displays this content in your browser:

```
#!/path/to/rebol -cs

REBOL [Title: "Dump CGI Server Variables"]

print "Content-Type: text/plain^/"

print "Server Variables:"

probe system/options/cgi

```

If you want to use this information in a log, you can write it to a file. For example, to log the addresses of visitors to your CGI page you could write:

```
write/append/lines %cgi.log
    system/options/cgi/remote-addr

```

The **/append** and **/lines** refinements causes the write to be at the tail of the file and include a line-break. Here's another approach that puts multiple items on the same line:

```
write/append %cgi.log reform [
    system/options/cgi/remote-addr
    system/options/cgi/remote-ident
    system/options/cgi/content-type
    newline
]

```

### 13.5 CGI Requests

There are two methods for CGI to provide request data to your scripts: GET and POST.

The GET method encodes CGI data into the URL. This is used to provide information to the server. You may have noticed before that some URLs look like this:

```
http://www.example.com/cgi-bin/test.r?&data=test

```

The string that follows the question mark (?) provides the arguments to CGI. At times they can be quite long. This string is provided to your script when it is run. It can be obtained from the `cgi/query-string` field. For instance, to print the string from a script:

```
print system/options/cgi/query-string

```

The data within the string can include whatever data you require. However, because the string is part of a URL, data must be encoded. There are restrictions on the characters that are allowed.

In addition, when the data is created by HTML forms, it is encoded in a standard way. This data can be decoded and placed within an object with the code:

```
cgi: make object! decode-cgi-query
    system/options/cgi/query-string

```

The `decode-cgi-query` function returns a block that contains variable names and their values. See the HTML form example in the next section.

The POST method provides the CGI data as a string. The data does not need to be encoded. It can be in any format you desire and can even be binary. Post data is read from the standard input device. You will need to read it from the input with a line such as:

```
data: make string! 2002
read-io system/ports/input data 2000

```

This would read up to the first 2000 bytes of POST data and put it in a string.

A good format for POST data is to use a REBOL dialect and create a simple parser. The POST data can be loaded and parsed as a block. See the [Parsing](rebolcore-15.html#_Toc487519750) chapter.

**Warning About Blocks**

It is not a good idea to pass REBOL blocks to be directly evaluated because this can present a security risk. For instance, someone could POST a block that reads or deletes files on the server. However, it is safe to pass blocks that are interpreted by your script (a dialect).

Here is an example script that displays the post data in your browser:

```
#!/path/to/rebol -cs

REBOL [Title: "Show POST data"]

print "Content-Type: text/html^/"
data: make string! 10000
foreach line copy system/ports/input [
    repend data [line newline]
]

print [
    <HTML><BODY>
    {Here is the posted data.}
    <HR><PRE>data</PRE>
    </BODY></HTML>
]

```

### 13.6 Processing HTML Forms

CGI is often used for processing HTML forms. The forms accept input from various fields and submit them to the Web server as an HTML get or post method.

Here is an example that uses the CGI get to process a form and send an email as the result. There are two parts to this: the HTML page and the CGI script.

Here is an HTML page that includes a form:

```
<HTML><BODY>

<FORM ACTION="http://example.com/cgi-bin/send.r" METHOD="GET">

<H1>CGI Emailer</H1><HR>

Enter your email address:<P>

<INPUT TYPE="TEXT" NAME="email" SIZE="30"><P>

<TEXTAREA NAME="message" ROWS="7" COLS="35">
Enter message here.
</TEXTAREA><P>

<INPUT TYPE="SUBMIT" VALUE="Submit">

</FORM>
</BODY></HTML>

```

When the above script is submitted, it needs a CGI script to handle its results. Here is an example of such a script. This example script decodes the form data and sends the email. It returns a confirmation page.

```
#!/path/to/rebol -cs

REBOL [Title: "Send CGI Email"]

print "Content-Type: text/html^/"

cgi: make object! decode-cgi-query
    system/options/cgi/query-string

print {<HTML><BODY><H1>Email Status</H1><HR><P>}

failed: error? try [send to-email cgi/email cgi/message]

print either failed [
    {The email could not be sent.}
][
    [{The email to} cgi/email {was sent.}]
]

print {</BODY><HTML>}

```

This script should be named `send`.r and stored in the `cgi-bin` directory. It's permissions must be set to being readable and executable by all.

When the form has been submitted by a browser, this script will run. It decodes the CGI query string into a cgi object. The object now has email and message variables that are used for the **send** function. Before **send** is done, the email field is converted from a string to an `email` datatype.

The **send** function is placed within a try block to catch errors if they occur while sending the email. The failed variable is set to true if an error occurred, and the appropriate message is generated.

Other CGI examples can be found in the REBOL Script Library at ``[http://www.rebol.com/library/library.html](http://www.rebol.com/library/library.html).

## 14. TCP - Transmission Control Protocol

In addition to those protocols previously described, you can create your own network servers and clients with the transmission control protocol, TCP.

### 14.1 Creating Clients

TCP ports can be opened in the same way as other REBOL protocols, using the TCP URL. To open a TCP connection to an HTTP (Web) server on TCP port number 80:

```
http-port: open tcp://www.example.com:80

```

Another way of opening a TCP connection is to provide the port specification directly. This is a substitute for using a URL and is often quite useful:

```
http-port: open [
    scheme: 'tcp
    host: "www.example.com"
    port-id: 80
]

```

Since ports are series, you can use the same series functions for sending and receiving data. The example below queries the HTTP server opened in the previous example. It uses the **insert** function to put data into the port series which sends it to the server:

```
insert http-port "GET / HTTP/1.0^/^/"

```

The two newline characters are used to tell the server that the header has been sent.

*The newline characters are automatically converted to CR LF sequences because the port was opened in text mode.*

The**** server processes the HTTP request and returns a result to the port series. To read the result, use the **copy**function:

```
while [data: copy http-port] [prin data]

```

This loop will continue to fetch data until a `none` is returned from copy. This behavior differs between protocols. A none is returned because the server closes the connection. Other protocols may send a special character to indicate the end of the transfer.

Now that all the data has been received, HTTP port should be closed:

```
close http-port

```

Here is another example that connects to a POP port on a server:

```
pop: open/lines tcp://fred.example.com:110

```

This example uses the **/lines** refinement. The connection will now be line oriented. Data will be written and read as lines. To read the first line from the server:

```
print first pop
+OK QPOP (version 2.53) at fred.example.com starting.

```

To send the server a username for POP login:

```
insert pop "user carl"

```

Because the port is operating in line mode, a line terminator is sent after the insert. The server response can be read with with:

```
print first pop
+OK Password required for carl.

```

And the rest of the communication would proceed as:

```
insert pop "pass secret"

print first pop
+OK carl has 0 messages (0 octets).
insert pop "quit"

first pop
+OK Pop server at fred.example.com signing off.

```

The connection should now be closed:

```
close pop

```

### 14.2 Creating Servers

To create a server you need to wait for connections and respond to them as they occur. To set up a port on your machine that can be used to wait for incoming connections:

```
listen: open tcp://:8001

```

Notice that you do not supply a host name, only a port number. This type of port is called a `listen` port. The system now accepts connections on port number 8001.

To wait for a connection from another machine, you **wait** on the listen port.

```
wait listen

```

This function does not return until a connection has been made.

*NOTE: There are other options available for \**wait** . For instance, you can wait on multiple ports or for a timeout as well.*

You can now open the connection port from the machine that has contacted your system:

```
connection: first listen

```

This returns the connection that has been made to the listen port. It is a port like all others and can now be used to receive and send data using the **insert**, **copy**, **first**, and other series functions:

```
insert connection "you are connected^/"

while [newline <> char: first connection] [
    print char
]

```

When the communications is complete, the connection should be closed:

```
close connection

```

You are now ready for the next connection on the listen port. You can **wait** again and use **first** again to get the connection.

When you are done with serving, you can close the listen port with:

```
close listen

```

### 14.3 A Tiny Server

Here is a useful REBOL server that only requires a few lines of code. This server evaluates whatever REBOL code is sent to it. Lines of REBOL are read from the client until an error occurs. Each line must be a complete REBOL expression. They can be of any length but must be a single line.

```
server-port: open/lines tcp://:4321

forever [
    connection-port: first server-port
    until [
        wait connection-port
        error? try [do first connection-port]
    ]
    close connection-port
]
close server-port

```

If an error occurs, the connection is closed and the server waits for the next connection.

Here is an example of a client script that allows you to enter REBOL command lines remotely:

```
server: open/lines tcp://localhost:4321
until [error? try [insert server ask "R> "]]
close server

```

Here the query is used to determine if the connection was been closed due to an error.

### 14.4 Testing TCP Code

To test your server code, connect from your own machine, rather than requiring both a server and a client. This can be done from two separate REBOL processes or even from the same process.

To connect to your local machine, you can use a line such as:

```
port: open tcp://localhost:8001

```

Here is an example that makes two ports connect to each other in line mode. This is a sort of `echo` port since you're sending data to yourself. It provides a good test of your code and networking:

```
listen: open/lines tcp://:8001
remote: open/lines tcp://localhost:8001
local: first listen
insert local "How are you?"
print first remote  ; response
close local
close remote
close listen

```

## 15. UDP - User Datagram Protocol

The User Datagram Protocol is another transport layer protocol that provides a connectionless method of communicating between machines. It allows you to send datagrams, packets, between machines.

The operation of UDP is much different than TCP. UDP is simpler, but it is essentially unreliable. There is no guarantee that a packet will ever reach its destination. In addition, UDP has no flow control. If you send messages too quickly, packets may be lost.

Like TCP, the **wait** function can be used to wait for the next packet to arrive and the **copy** function is used to return the data. If there is no data, **copy** waits until there is. Note, however, that **insert** never waits.

Here is an example of a simple UDP server script:

```
udp: open udp://:9999
wait udp
print copy udp
insert udp "response"
close udp

```

The messages inserted here by the server are sent to the client the server last received a message from. This allows responses to be sent for incoming messages. However, unlike TCP you do not have a continuous connection between the machines. Each packet transfer is a separate exchange.

The client script to communicate with the above server would be:

```
udp: open udp://localhost:9999
insert udp "Test"
wait udp
print copy udp
close udp

```

You should know that the maximum UDP packet size depends on the operating system. 32 KB and 64 KB are common values. In order to send larger amounts of data, you will need to buffer the data, chopping it into smaller pieces. However, careful programming is required to make sure that each piece of the data is received. Remember that with UDP, there are no guarantees.