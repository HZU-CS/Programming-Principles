# C Characters and Strings

## Objectives

Use the functions of the character-handling library (<ctype.h>). 

Use the string-conversion functions of the general utilities library (<stdlib.h>). 

Use the string and character input/output functions of the standard input/output library (<stdio.h>).

Use the string-processing functions of the stringhandling library (<string.h>). 

Use the memory-processing functions of the stringhandling library (<string.h>).

## Fundamentals of Strings and Characters

Characters are the fundamental building blocks of source programs. Every program is composed of a sequence of characters that—when grouped together meaningfully—is interpreted by the computer as a series of instructions used to accomplish a task. 

A character constant is an int value represented as a character in single quotes. The value of a character constant is the character’s integer value in the machine’s character set

A string is a series of characters treated as a single unit. A string may include letters, digits and various special characters such as +, -, *, / and $. String literals, or string constants, in C are written in double quotation marks.

A string in C is an array of characters ending in the null character('\0')

A string is accessed via a pointer to its first character. The value of a string is the address of its first character. 

A character array or a variable of type char * can be initialized with a string in a definition. 

When defining a character array to contain a string, the array must be large enough to store the string and its terminating null character. 

A string can be stored in an array using scanf. Function scanf will read characters until a space, tab, newline or end-of-file indicator is encountered. 

For a character array to be printed as a string, the array must contain a terminating null character. 

## Character-Handling Library

isdigit

isalpha

isalnum

isxdigit

islower

isupper

toupper

tolower

isspace

iscntrl

ispunct

isprint

isgraph

## String-Conversion Functions

strtod

strtol

strtoul

## Standard Input/Output Library Functions

fgets

putchar

getchar

puts

sprintf

sscanf

## String-Manipulation Functions of the String-Handling Library

strcpy

strncpy

strcat

strncat

## Comparison Functions of the String-Handling Library

strcmp

strncmp

## Search Functions of the String-Handling Library

strchr

strcspn

strpbrk

strrchr

strstr

strtok

## Memory Functions of the String-Handling Library

memcpy

memmove

memcmp

memchr

memset

## Other Functions of the String-Handling Library

strerror

strlen

