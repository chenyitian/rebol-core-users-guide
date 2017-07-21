# Introduction

## Contents:

- [1. About REBOL](#1-about-rebol)
- [2. About this Guide](#2-about-this-guide)
  - [2.1 Suggestion for New Programmers](#21-suggestion-for-new-programmers)
  - [2.2 Suggestion for Experienced Programmers](#22-suggestion-for-experienced-programmers)
- [3. Document Conventions](#3-document-conventions)
- [4. Technical Support](#4-technical-support)
  - [4.1 Developer News and Information](#41-developer-news-and-information)
  - [4.2 Discussions and Forums](#42-discussions-and-forums)
  - [4.3 Bug Reports and Enhancement Requests](#43-bug-reports-and-enhancement-requests)
  - [4.4 REBOL.org Script Library](#44-rebolorg-script-library)
  - [4.5 New Alpha and Beta Releases](#45-new-alpha-and-beta-releases)
- [5. Comments are Welcome](#5-comments-are-welcome)

## 1. About REBOL

Here are a few quick facts about REBOL:

- **REBOL stands for Relative Expression-Based Object Language.**
- **REBOL is pronounced "reb-ol"** as in "rebel with a cause".
- **REBOL is a messaging language.** Its main purpose is to provide a better approach to distributed computing and communication.
- **REBOL was designed by Carl Sassenrath**, the operating system architect responsible for the Amiga OS, the world's first multitasking operating system for personal computers.
- **REBOL is more than just a programming language.** It is also a language for representing data and metadata. It provides a single method for the computation, storage, and exchange of information.
- **REBOL code and data span more than 40 system platforms.** A script written on Windows runs equally well on Linux, UNIX, and many other platforms... with no changes necessary.
- **REBOL introduces the concept of dialecting** - small, efficient, domain-specific sublanguages for code, data, and metadata.
- **REBOL implementations are intentionally kept very small** even though they include hundreds of functions, dozens of datatypes, built-in help, multiple Internet protocols, compression, error handling, a debugging console, encryption, and much more.
- **REBOL programs are easy to write**. All you need is a text editor. A program can be a single line or an entire application consisting of dozens of files.
- **REBOL/Core serves as the foundation for all REBOL technology.** While designed to be simple and productive for novices, the language extends new dimensions of power to professionals.

The graphical version of REBOL, called REBOL/View, builds on top of REBOL/Core. It can be found on the REBOL website.

## 2. About this Guide

This guide provides the basic information necessary for using REBOL/Core. It assumes that the reader is already familiar with general programming and operating system terminology and concepts.

### 2.1 Suggestion for New Programmers

If you are new to programming, REBOL provides an excellent way to get started.

There are a few general concepts that REBOL uses everywhere. For example, REBOL's concept of a *series* is used in everything from data structures to code blocks. Once you learn the concepts and methods of series, they can be applied throughout your programs. You should learn these concepts well. It will pay off later. The chapters in this users guide are ordered to best help you get started.

If you experience trouble using REBOL, do not get frustrated. There are many people who can help you. The REBOL Mail List (see support section below) is monitored by hundreds of people who enjoy helping beginners get started. Feel free to visit that forum for any reason.

### 2.2 Suggestion for Experienced Programmers

If you are already familiar with other programming languages like C, C++, Java, Pascal, Python, PERL, BASIC, etc. we should warn you: **REBOL is quite different**.

You should know that REBOL was not designed just to be different, but rather to give programmers more expressive power. Programmers who have mastered REBOL suggest that the best approach is to forget what you already know about other languages. That's because you don't create REBOL programs in the same way. Sure, you can create REBOL programs that look similar to C, but if you do that, you will lose a lot of the advantages that REBOL offers.

In technical terms, REBOL is a highly reflective, functional, symbolic language with definitional scoping rules. If you don't know what this means, don't worry. REBOL takes advantage of advances in computer science, but you don't need to be a computer scientist to use it.

As an experienced programmer, you may be tempted to skip most of the chapters of this guide. For the most part, that is fine. However, concepts like *series* are critical to understanding REBOL. If you don't take the time to master such concepts, you will find it difficult to become truly fluent in the REBOL language.

## 3. Document Conventions

The following table describes the typographical conventions used in this guide.

| Item                                     | Convention             | Example                      |
| ---------------------------------------- | ---------------------- | ---------------------------- |
| Words that are part of the REBOL language (as function names, special variables, system objects). | Bold, green, monospace | **Append** **at** **change** |
| Non-REBOL words and values such as file names, directory names, program names, and variable names. | Green, monospace       | `myfile` `window-color`      |
| Code examples.                           | Boxed bold monospace   | `do %feedback.r`             |
| Results printed at the REBOL console.    | Boxed blue monospace   | `true`                       |

## 4. Technical Support

For general questions or feedback regarding REBOL products or our website please visit our[feedback page](http://www.rebol.com/feedback.html). We usually answer messages within 24 to 48 hours. Be sure to include your email address if you want a reply.

### 4.1 Developer News and Information

The [**REBOL Developer Network (www.REBOL.net)**

This site is also home to [Carl's REBOL Blog](http://www.rebol.net/cgi-bin/blog.r), an informative archive of insights, ideas, and queries by REBOL's inventor and founder, Carl Sassenrath.

### 4.2 Discussions and Forums

- **REBOL Mailing List**
  The REBOL email discussion list is a forum for questions and answers about all topics related to REBOL. You can view prior messages at the [mail list archive](http://www.rebol.org/cgi-bin/cgiwrap/rebol/ml-date-index.r) on REBOL.org.
- **REBOL Talk Forum**
  This is an independent web-based forum for open discussions about REBOL.
- **REBOL Google Group**
  This new web/email discussion group has recently been started on Google Groups. This is still in the experimental stages of use.
- **Other Discussions**
  REBOL Technologies also hosts a variety of private discussion groups using our IOS technology and the AltME IM system from Safeworlds Inc. Look for opening announcements and member requests on www.REBOL.net.

### 4.3 Bug Reports and Enhancement Requests

REBOL customers, developers, and user can now directly search for information related to known problems, report new problems, or request enhancements using our **RAMBO** database.

### 4.4 REBOL.org Script Library

The site **www.REBOL.org** is a community-operated website that provides an extensive library of REBOL examples. It also includes a variety of tutorials as well as an archive of REBOL Mailing List messages.

### 4.5 New Alpha and Beta Releases

We [publish interim builds](http://www.rebol.net/builds/) for our products on a regular basis. This service is intended for customers and experienced developers only. These pages hold raw builds not distribution packages.

## 5. Comments are Welcome

To help us with future releases of this documentation we would like to know what corrections or clarifications you would find useful. Send them to the [Feedback](http://www.rebol.com/feedback.html) page on our website. Please include the title, version, and chapter of the guide.