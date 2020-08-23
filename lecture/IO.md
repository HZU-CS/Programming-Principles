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

A conversion specification consists of a % and a conversion specifier.

## Printing Integers

Integers are printed with the following conversion specifiers: d or i for optionally signed integers, o for unsigned integers in octal form, u for unsigned integers in decimal form and x or X for unsigned integers in hexadecimal form. The modifier h, l or ll is prefixed to the preceding conversion specifiers to indicate a short, long or long long integer, respectively.

## Printing Floating-Point Numbers

Floating-point values are printed with the following conversion specifiers: e or E for exponential notation, f for regular floating-point notation, and g or G for either e (or E) notation or f notation. When the g (or G) conversion specifier is indicated, the e (or E) conversion specifier is used if the value’s exponent is less than -4 or greater than or equal to the precision with which the value is printed.

The precision for the g and G conversion specifiers indicates the maximum number of significant digits printed.

## Printing Strings and Characters

The conversion specifier c prints a character.

The conversion specifier s prints a string of characters ending in the null character. 

## Other Conversion Specifiers

The conversion specifier p displays an address in an implementation-defined manner (on many systems, hexadecimal notation is used). 

The conversion specifier %% causes a literal % to be output. 

## Printing with Field Widths and Precision

If the field width is larger than the object being printed, the object is right justified by default. 

Field widths can be used with all conversion specifiers.

Precision used with integer conversion specifiers indicates the minimum number of digits printed. Zeros are prefixed to the printed value until the number of digits is equivalent to the precision.

Precision used with floating-point conversion specifiers e, E and f indicates the number of digits that appear after the decimal point. Precision used with floating-point conversion specifiers g and G indicates the number of significant digits to appear. 

Precision used with conversion specifier s indicates the number of characters to be printed. 

The field width and the precision can be combined by placing the field width, followed by a decimal point, followed by the precision between the percent sign and the conversion specifier. 

It’s possible to specify the field width and the precision through integer expressions in the argument list following the format control string. To do so, use an asterisk (*) for the field width or precision. The matching argument in the argument list is used in place of the asterisk. 

## Using Flags in the printf Format Control String

The - flag left justifies its argument in a field.

The + flag prints a plus sign for positive values and a minus sign for negative values. 

The space flag prints a space preceding a positive value that’s not displayed with the + flag.

The # flag prefixes 0 to octal values and 0x or 0X to hexadecimal values and forces the decimal point to be printed for floating-point values printed with e, E, f, g or G.

The 0 flag prints leading zeros for a value that does not occupy its entire field width.

## Printing Literals and Escape Sequences

Most literal characters to be printed in a printf statement can simply be included in the format control string. However, there are several “problem” characters, such as the quotation mark (") that delimits the format control string itself. Various control characters, such as newline and tab, must be represented by escape sequences. An escape sequence is represented by a backslash (\\), followed by a particular escape character. 

## Reading Formatted Input with scanf

Input formatting is accomplished with the scanf library function. 

Integers are input with scanf with the conversion specifiers d and i for optionally signed integers and o, u, x or X for unsigned integers. The modifiers h, l and ll are placed before an integer conversion specifier to input a short, long and long long integer, respectively.

Floating-point values are input with scanf with the conversion specifiers e, E, f, g or G. The modifiers l and L are placed before any of the floating-point conversion specifiers to indicate that the input value is a double or long double value, respectively.

 Characters are input with scanf with the conversion specifier c

Strings are input with scanf with the conversion specifier s

A scanf with a scan set scans the characters in the input, looking only for those characters that match characters contained in the scan set. When a character is matched, it’s stored in a character array. The scan set stops inputting characters when a character not contained in the scan set is encountered. 

To create an inverted scan set, place a caret (^) in the square brackets before the scan characters. This causes characters input with scanf and not appearing in the scan set to be stored until a character contained in the inverted scan set is encountered.

Address values are input with scanf with the conversion specifier p.

Conversion specifier n stores the number of characters input so far in the current scanf. The corresponding argument is a pointer to int.

The assignment suppression character (*) reads data from the input stream and discards the data.

A field width is used in scanf to read a specific number of characters from the input stream.

## Secure C Programming

The C standard lists many cases in which using incorrect library-function arguments can result in undefined behaviors. These can cause security vulnerabilities, so they should be avoided. Such problems can occur when using printf (or any of its variants, such as sprintf, fprintf, printf_s, etc.) with improperly formed conversion specifications. CERT rule FIO00-C discusses these issues and presents a table showing the valid combinations of formatting flags, length modifiers and conversion-specifier characters that can be used to form conversion specifications. The table also shows the proper argument type for each valid conversion specification. In general, as you study any programming language, if the language specification says that doing something can lead to undefined behavior, avoid doing it to prevent security vulnerabilities. 