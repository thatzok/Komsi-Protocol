# KOMSI-Command-Structure

The protocol is unidirectional and ASCII text and line based.

Each non-empty line ends with the ASCII LF (line feed) character (ascii code decimal 10).

Each non-empty line consists of one or more variables.

A variable consists of a command-code and an unsigned integer number.

## The structure in pseudo code

<EOL> = ASCII code decimal 10 (hex 0x0a)

<line> = <variables><EOL>

<variables> = one or more <variable>

<variable> = <code><number>

<code> = one ASCII character out of a...z and A...Z CASE SENSITIVE (so "a" and "A" are different codes)

<numer> = one or more <digit>

<digit> = one ASCII character representing the digits "0" ... "9" ("0" is ASCII code dec 48, "9" is ASCII code dec 57). 

