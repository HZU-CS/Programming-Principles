# C Formatted Input/Output

## Objectives

Use input and output streams. 

Use print formatting capabilities. 

Use input formatting capabilities. 

Print integers, floating-point numbers, strings and characters. 

Print with field widths and precisions. 

Use formatting flags in the printf format control string. 

Output literals and escape sequences.

Read formatted input using scanf.

## Streams

All input and output is performed with streams —which are sequences of bytes. 

Normally, the standard input stream is connected to the keyboard, and the standard output and error streams are connected to the computer screen.

Operating systems often allow the standard input and standard output streams to be redirected to other devices.

## Formatting Output with printf

A format control string describes the formats in which the output values appear. The format control string consists of conversion specifiers, flags, field widths, precisions and literal characters.

A conversion specification consists of a % (p. 411) and a conversion specifier.

## Printing Integers

Integers are printed with the following conversion specifiers: d or i for optionally signed integers, o for unsigned integers in octal form, u for unsigned integers in decimal form and x or X for unsigned integers in hexadecimal form. The modifier h, l or ll is prefixed to the preceding conversion specifiers to indicate a short, long or long long integer, respectively.

## Printing Floating-Point Numbers

Floating-point values are printed with the following conversion specifiers: e or E for exponential notation, f for regular floating-point notation, and g or G for either e (or E) notation or f notation. When the g (or G) conversion specifier is indicated, the e (or E) conversion specifier is used if the value’s exponent is less than -4 or greater than or equal to the precision with which the value is printed.

The precision for the g and G conversion specifiers indicates the maximum number of significant digits printed.

