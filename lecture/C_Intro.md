# Introduction to C Programming

## Textbook TIPS

- Pay attention
- Digest and follow

## Objectives

Write simple C programs. 

Use simple input and output statements. 

Use the fundamental data types.

Learn computer memory concepts. 

Use arithmetic operators. 

Learn the precedence of arithmetic operators. 

Write simple decision-making statements. 

Begin focusing on secure C programming practices.

## Introduction

The C language facilitates a structured and disciplined approach to computer-program design. In this chapter we introduce C programming and present several examples that illustrate many important features of C. Each example is analyzed one statement at a time.

We provide the first of many “Secure C Programming” sections.

## A Simple C Program: Printing a Line of Text

```c
// A first program in C.
#include <stdio.h>

// function main begins program execution 
int main(void) {
    printf("Welcome to C!\n");
    return 0;
} // end function main
```

### Comments

```c
// A first program in C.
```

begin with //, indicating that these two lines are comments. You insert comments to document programs and improve program readability. Comments do not cause the computer to perform any action when the program is run—they’re ***ignored*** by the C compiler and do ***not*** cause any machine-language object code to be generated. 

You can also use /\*…\*/ multi-line comments in which everything from /* on the first line to \*/ at the end of the last line is a comment. We prefer // comments because they’re shorter and they eliminate common programming errors that occur with /\*…\*/ comments, especially when the closing */ is omitted.

### #include Preprocess Directive

```c
#include <stdio.h>
```

is a directive to the C preprocessor. Lines beginning with # are processed by the preprocessor before compilation. It tells the preprocessor to include the contents of the standard input/output header (<stdio.h>) in the program. This header contains information used by the compiler when compiling calls to standard input/output library functions such as printf. 

### Blank Lines and White Space

You use blank lines, space characters and tab characters (i.e., “tabs”) to make programs easier to read. Together, these characters are known as white space. White-space characters are normally ignored by the compiler. 

### The main Function

```c
int main(void)
```

is a part of every C program. The parentheses after main indicate that main is a program building block called a function. C programs contain one or more functions, one of which must be main. Every program in C begins executing at the function main. Functions can return information. The keyword int to the left of main indicates that main “returns” an integer (whole-number) value.

Functions also can receive information when they’re called upon to execute. The void in parentheses here means that main does not receive any information.

### An Output Statement



### Escape Sequences



### Return Value



### The Linker and Executables



### Using Multiple printfs

```c
#include <stdio.h>

int main(void) {
    printf("Welcome ");
    printf("to C!\n");
    return 0;
}
```



```c
#include <stdio.h>

int main(void) {
    printf("Welcome\nto\nC!\n");
    return 0;
}
```



## Another Simple C Program: Adding Two Integers



## Memory Concepts



## Arithmetic in C



## Decision Making: Equality and Relational Operators



## Secure C Programming

### Avoid Single-Argument printfs

One such guideline is to avoid using printf with a single string argument. If you need to display a string that terminates with a newline, use the puts function, which displays its string argument followed by a newline character.

```c
printf("Welcome to C!\n");
```

should be written as:

```c
puts("Welcome to C!\n");
```

If you need to display a string without a terminating newline character, use printf with two arguments—a "%s" format control string and the string to display. The %s conversion specifier is for displaying a string. 

```c
printf("Welcome ");
```

should be written as:

```c
printf( "%s", "Welcome " );
```

Although the printfs in this chapter as written are actually not insecure, these changes are responsible coding practices that will eliminate certain security vulnerabilities as we get deeper into C.

### scanf and printf, scanf_s and printf_s

https://stackoverflow.com/questions/21434735/difference-between-scanf-and-scanf-s

C11 standard

scanf_s: secure version of scanf

printf_s: secure version of printf

***tradeoff***

- more secure
- less portability 