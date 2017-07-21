# Appendix 3 - Console

**REBOL/Core Users GuideMain Table of ContentsSend Us Feedback**

## Contents:

[1. Command Prompt](#section-1)
[2. Result Indicator](#section-2)
[3. History Recall](#section-3)
[4. Busy Indicator](#section-4)
[5. Advanced Console Operations](#section-5)
  [5.1 Keyboard Input Sequences](#section-5.1)
  [5.2 Terminal Output Sequences](#section-5.2)

## 1. Command Prompt

The default command line prompt is ">>". You can change the prompt with code such as:

```
system/console/prompt: "Input: "

```

The prompt then becomes:

```
Input:

```

The prompt can be a block that is evaluated each time. This line prints the current time:

```
system/console/prompt: [reform [now/time " >> "]]

```

This would result in a prompt of:

```
10:30 >>

```

## 2. Result Indicator

The default result indicator is "==" and can be modified with a line such as:

```
system/console/result: "Result: "

```

These settings can be placed in the `user`.`r` file to make them permanent.

## 3. History Recall

Each line typed into REBOL at the prompt is stored in a history block, and it can be recalled later using the up and down arrow keys. For instance, pressing the up arrow once recalls the prior input line.

The history block containing all input lines is accessed from the system console object:

```
probe system/console/history

```

You can save the history block as a file:

```
save %history.r system/console/history

```

and it can be reloaded later with:

```
system/console/history: load %history.r

```

These lines can be put in the `user`.`r` file to save and reload your history between REBOL sessions.

## 4. Busy Indicator

When REBOL waits for a network operation to complete, a busy indicator appears on screen to indicate that something is happening. You can change the indicator with a line like:

```
system/console/busy: "123456789-"

```

Whe REBOL is running in quiet mode, te busy indicator will not be displayed.

## 5. Advanced Console Operations

The console provides "virtual terminal" capability that allows you to perform operations such as cursor movement, cursor addressing, line editing, screen clearing, control key input, and cursor position querying.

The console control sequences follow the ANSI standard. These features provide you with the capability to write your own platform-independent terminal programs such as text editors, email clients, or telnet emulators.

The console features apply to both input and output. On input, function keys will be converted to multiple-character escape sequences. On output, multiple-character escape sequences can be used to control the display of text in the console window. Both the input and output sequences begin with the ANSI escape character, 27 decimal (1B hex). The next character in the sequence indicates the control keys on input or the terminal control operation on output.

*The ANSI control characters are case-sensitive and normally require an upper case character.*

### 5.1 Keyboard Input Sequences

The input sequences for function keys are listed in the table below (on systems and shells that support them, such as Linux, BSD, etc.)

To receive these sequences as a stream of unprocessed characters, disable the input port line handling mode:

```
set-modes system/ports/input [lines: false]

```

Now you can get input from the port (with COPY or READ-IO) or use a function like INPUT to get each character:

```
while [
    code: input
    code <> 13  ; ENTER
][
    probe code
]

```

Here are a few of the common ANSI input function codes:

| Function Key | As Escape Code | As REBOL Block    |
| ------------ | -------------- | ----------------- |
| F1           | ESC O P        | [27 79 80]        |
| F2           | ESC O Q        | [27 79 81]        |
| F3           | ESC O R        | [27 79 82]        |
| F4           | ESC O S        | [27 79 83]        |
| F5           | ESC [ 1 5 ~    | [27 91 49 53 126] |
| F6           | ESC [ 1 7 ~    | [27 91 49 55 126] |
| F7           | ESC [ 1 8 ~    | [27 91 49 56 126] |
| F8           | ESC [ 1 9 ~    | [27 91 49 57 126] |
| F9           | ESC [ 2 0 ~    | [27 91 50 48 126] |
| F10          | ESC [ 2 1 ~    | [27 91 50 49 126] |
| F11          | ESC [ 2 2 ~    | [27 91 50 50 126] |
| F12          | ESC [ 2 3 ~    | [27 91 50 51 126] |
| Home         | ESC [ 1 ~      | [27 91 49 126]    |
| End          | ESC [ 4 ~      | [27 91 52 126]    |
| Page-up      | ESC [ 5 ~      | [27 91 53 126]    |
| Page-down    | ESC [ 6 ~      | [27 91 54 126]    |
| Insert       | ESC [ 2 ~      | [27 91 50 126]    |
| Up           | ESC [ A        | [27 91 65]        |
| Down         | ESC [ B        | [27 91 66]        |
| Left         | ESC [ D        | [27 91 68]        |
| Right        | ESC [ C        | [27 91 67]        |

### 5.2 Terminal Output Sequences

There are several variations in the terminal control output character sequences. Some command codes are preceded by a number (sent in ASCII) indicating that the operation is to be performed the specified number of times. For example the cursor motion command may be preceded by two numbers separated by a semicolon to indicate the row and column position to move to. The cursor command characters (upper case required) are included in the following table:

| Output Sequence | Description                              |
| --------------- | ---------------------------------------- |
| (1B)            | Use this escape code prior to the following codes |
| D               | Moves cursor one space left              |
| C               | Moves cursor one space right             |
| A               | Moves cursor one space up                |
| B               | Moves cursor one space down              |
| n D             | Moves cursor n spaces left               |
| n C             | Moves cursor n spaces right              |
| n A             | Moves cursor n spaces up                 |
| n B             | Moves cursor n spaces down               |
| r ; c H         | Moves cursor to row r, column c*         |
| H               | Moves cursor to top left corner (home)*  |
| P               | Deletes one character to the right at current location |
| n P             | Deletes n characters to the right at current location |
| @               | Inserts one blank space at current location |
| n @             | Inserts n blank spaces at current location |
| J               | Clears screen and moves cursor to top left corner (home)* |
| K               | Clears from current position to end of current line |
| 6n              | Places the current cursor position in the input buffer |
| 7n              | Places screen dimensions in the input buffer |

The top left corner is defined as row 1, column 1

The following example moves the cursor to the right ten spaces:

```
print "^(1B)[10CHi!"
Hi
```

This example moves the cursor to the left seven spaces and clears the remainder of the line:

```
cursor: func [parm [string!]][join "^(1B)[" parm]
print ["How are you" cursor "7D" cursor "K"]
How a

```

To find the current console window size, you can use this example:

```
cons: open/binary [scheme: 'console]

print cursor "7n"
screen-dimensions: next next to-string copy cons
33;105R
close cons

```

The above example opens the console, sends a control character to the input buffer and copies the return value. It reads the value (screen dimensions) that is returned after the control character and closes the console. The return value is the height and width separated by a semicolon (;) and followed by an R. In the above example, the screen is 33 high by 105 wide.

**Autoscroll**

Printing a character to the bottom-right corner of some terminals will cause a new line, which will scroll the screen. Others will not. This inconsistency between console terminal types must be considered when writing REBOL scripts intended to be cross-platform.