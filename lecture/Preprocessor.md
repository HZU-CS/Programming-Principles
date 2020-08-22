# C Preprocessor

## Objectives

Use #include to develop large programs. 

Use #define to create macros with and without arguments. 

Use conditional compilation to specify portions of a program that should not always be compiled (such as code that assists you in debugging). 

Display error messages during conditional compilation. 

Use assertions to test whether the values of expressions are correct.

## Introduction

The C preprocessor executes before a program is compiled. Some actions it performs are:

- the inclusion of other files into the file being compiled
- definition of symbolic constants and macros
- conditional compilation of program code and
- conditional execution of preprocessor directives

Preprocessor directives begin with #, and only whitespace characters and comments delimited by /* and */ may appear before a preprocessor directive on a line

C has perhaps the largest installed base of “legacy code” of any modern programming language. It’s been in active use for more than four decades. As a professional C programmer, you’re likely to encounter code written many years ago using older programming techniques. To help you prepare for this, we discuss a number of those techniques in this chapter and recommend some newer techniques that can replace them.

## #include Preprocessor Directive

The #include preprocessor directive has been used throughout this text. It causes a copy of a specified file to be included in place of the directive. The two forms of the #include directive are:

```c
#include <filename>
#include "filename"
```

The difference between these is the location at which the preprocessor begins searches for the file to be included. If the filename is enclosed in angle brackets (< and >)—used for standard library headers—the search is performed in an implementation-dependent manner, normally through predesignated compiler and system directories. If the filename is enclosed in quotes, the preprocessor starts searches in the same directory as the file being compiled for the file to be included. This method is normally used to include programmer-defined headers. If the compiler cannot find the file in the current directory, then it will search through the predesignated compiler and system directories.

The #include directive is used to include standard library headers such as stdio.h and stdlib.h and with programs consisting of multiple source files that are to be compiled together. A header containing declarations common to the separate program files is often created and included in the file. Examples of such declarations are: 

- structure and union declarations, 
- typedefs,
- enumerations and 
- function prototypes.

## #define Preprocessor Directive: Symbolic Constants

The #define directive creates symbolic constants—constants represented as symbols—and macros—operations defined as symbols. The #define directive format is

```c
#define identifier replacement-text
```

When this line appears in a file, all subsequent occurrences of identifier that do not appear in string literals or comments will be replaced by replacement text automatically before the program is compiled. For example, 

```c
#define PI 3.14159
```

replaces all subsequent occurrences of the symbolic constant PI with the numeric constant 3.14159. Symbolic constants enable you to create a name for a constant and use the name throughout the program. 

## #define Preprocessor Directive: Macros

A macro is an identifier defined in a #define preprocessor directive. As with symbolic constants, the macro-identifier is replaced with replacement-text before the program is compiled. Macros may be defined with or without arguments. A macro without arguments is processed like a symbolic constant. In a macro with arguments, the arguments are substituted in the replacement text, then the macro is expanded—the replacement-text replaces the identifier and argument list in the program. A symbolic constant is a type of macro.

### Macro with one Argument

Consider the following one-argument macro definition that calculates the area of a circle:

```c
#define CIRCLE_AREA(x) ((PI) * (x) * (x))
```

#### Expanding a Macro with an Argument

Wherever CIRCLE_AREA(y) appears in the file, the value of y is substituted for x in the replacement-text, the symbolic constant PI is replaced by its value (defined previously) and the macro is expanded in the program. For example, the statement

```c
area = CIRCLE_AREA(4);
```

is expanded to

```c
area = ((3.14159) * (4) * (4));
```

then, at compile time, the value of the expression is evaluated and assigned to variable area. 

#### Importance of Parentheses

The parentheses around each x in the replacement-text force the proper order of evaluation when the macro argument is an expression. For example, the statement

```c
area = CIRCLE_AREA(c + 2);
```

is expanded to

```c
area = ((3.14159) * (c + 2) * (c + 2));
```

which evaluates correctly because the parentheses force the proper order of evaluation. If the parentheses in the macro definition are omitted, the macro expansion is

```c
area = 3.14159 * c + 2 * c + 2;
```

which evaluates incorrectly as

```c
area = (3.14159 * c) + (2 * c) + 2;
```

because of the rules of operator precedence. 

#### Better to Use a Function

Macro CIRCLE_AREA could be defined more safely as a function. Function circleArea

```c
double circleArea(double x)
{
	return 3.14159 * x * x;
}
```

performs the same calculation as macro CIRCLE_AREA, but the function’s argument is evaluated only once when the function is called. Also, the compiler performs type checking on functions—the preprocessor does not support type checking. 

### Macro with Two Arguments

The following two-argument macro calculates the area of a rectangle:

```c
#define RECTANGLE_AREA(x, y) ((x) * (y))
```

Wherever RECTANGLE_AREA(x, y) appears in the program, the values of x and y are substituted in the macro replacement-text and the macro is expanded in place of the macro name. For example, the statement

```c
rectArea = RECTANGLE_AREA(a + 4, b + 7);
```

is expanded to

```c
rectArea = ((a + 4) * (b + 7));
```

The value of the expression is evaluated at runtime and assigned to variable rectArea. 

### Macro Continuation Character

The replacement-text for a macro or symbolic constant is normally any text on the line after the identifier in the #define directive. If the replacement-text for a macro or symbolic constant is longer than the remainder of the line, a backslash (\) continuation character must be placed at the end of the line, indicating that the replacement-text continues on the next line.

### #undef Preprocessor Directive

Symbolic constants and macros can be discarded by using the #undef preprocessor directive. Directive #undef “undefines” a symbolic constant or macro name. The scope of a symbolic constant or macro is from its definition until it’s undefined with #undef, or until the end of the file. Once undefined, a name can be redefined with #define.

### Standard Library Functions and Macros

Functions in the standard library sometimes are defined as macros based on other library functions. A macro commonly defined in the  header is

```c
#define getchar() getc(stdin)
```

The macro definition of getchar uses function getc to get one character from the standard input stream. Function putchar of the  header and the character-handling functions of the  header often are implemented as macros as well. 

### Do Not Place Expressions with Side Effects in Macros

Expressions with side effects (e.g., variable values are modified) should not be passed to a macro because macro arguments may be evaluated more than once. 

## Conditional Compilation

Conditional compilation enables you to control the execution of preprocessor directives and the compilation of program code. Each conditional preprocessor directive evaluates a constant integer expression. Cast expressions, sizeof expressions and enumeration constants cannot be evaluated in preprocessor directives. 

## #if...#endif Preprocessor Directive

The conditional preprocessor construct is much like the if selection statement. Consider the following preprocessor code:

```c
#if !defined(MY_CONSTANT)
	#define MY_CONSTANT 0
#endif
```

which determines whether MY_CONSTANT is defined—that is, whether MY_CONSTANT has already appeared in an earlier #define directive. The expression defined(MY_CONSTANT) evaluates to 1 if MY_CONSTANT is defined and 0 otherwise. If the result is 0, !defined(MY_CONSTANT) evaluates to 1 and MY_CONSTANT is defined. Otherwise, the #define directive is skipped. Every #if construct ends with #endif. Directives #ifdef and #ifndef are shorthand for #if defined(name) and #if !defined(name). A multiple-part conditional preprocessor construct may be tested by using the #elif (the equivalent of else if in an if statement) and the #else (the equivalent of else in an if statement) directives. These directives are frequently used to prevent header files from being included multiple times in the same source file—we use this technique extensively in the C++ part of this book. These directives also are frequently used to enable and disable code that makes software compatible with a range of platforms. 

### Commenting Out Blocks of Code with #if...#endif

During program development, it’s often helpful to “comment out” portions of code to prevent them from being compiled. If the code contains multiline comments, /* and */ cannot be used to accomplish this task, because such comments cannot be nested. Instead, you can use the following preprocessor construct:

```c
#if 0
	code prevented from compiling
#endif
```

### Conditionally Compiling Debugging Code

Conditional compilation is sometimes used as a debugging aid. Debuggers provide much more powerful features than conditional compilation, but if a debugger is not available, printf statements can be used to print variable values and to confirm the flow of control. These printf statements can be enclosed in conditional preprocessor directives so the statements are compiled only while the debugging process is not completed. For example, 

```c
#ifdef DEBUG
	printf("Variable x = %d\n", x);
#endif
```

compiles the printf statement if the symbolic constant DEBUG is defined (#define DEBUG) before #ifdef DEBUG. When debugging is completed, you remove or comment out the #define directive from the source file and the printf statements inserted for debugging purposes are ignored during compilation. In larger programs, it may be desirable to define several symbolic constants that control the conditional compilation in separate sections of the source file. Many compilers allow you to define and undefine symbolic constants like DEBUG with a compiler flag that you supply each time you compile the code so that you do not need to change the code. 

## #error and #pragma Preprocessor Directives

The #error directive 

```c
#error tokens
```

prints an implementation-dependent message including the tokens specified in the directive. The tokens are sequences of characters separated by spaces. For example, 

```c
#error 1 - Out of range error
```

contains 6 tokens. When a #error directive is processed on some systems, the tokens in the directive are displayed as an error message, preprocessing stops and the program does not compile.

The #pragma directive

```c
#pragma tokens
```

causes an implementation-defined action. A pragma not recognized by the implementation is ignored. For more information on #error and #pragma, see the documentation for your C implementation.

## # and ## Operators

The # operator causes a replacement-text token to be converted to a string surrounded by quotes. Consider the following macro definition:

```c
#define HELLO(x) puts("Hello, " #x);
```

When HELLO(John) appears in a program file, it’s expanded to 

```c
puts("Hello, " "John");
```

The string "John" replaces #x in the replacement-text. Strings separated by whitespace are concatenated during preprocessing, so the preceding statement is equivalent to

```c
puts("Hello, John");
```

The # operator must be used in a macro with arguments because the operand of # refers to an argument of the macro.

The ## operator concatenates two tokens. Consider the following macro definition:

```c
#define TOKENCONCAT(x, y) x ## y
```

When TOKENCONCAT appears in the program, its arguments are concatenated and used to replace the macro. For example, TOKENCONCAT(O, K) is replaced by OK in the program. The ## operator must have two operands.

## Line Numbers

The #line preprocessor directive causes the subsequent source-code lines to be renumbered starting with the specified constant integer value. The directive 

```c
#line 100
```

starts line numbering from 100 beginning with the next source-code line. A filename can be included in the #line directive. The directive

```c
#line 100 "file1.c"
```

indicates that lines are numbered from 100 beginning with the next source-code line and that the name of the file for the purpose of any compiler messages is "file1.c". The directive normally is used to help make the messages produced by syntax errors and compiler warnings more meaningful. The line numbers do not appear in the source file.

## Predefined Symbolic Constants

Standard C provides predefined symbolic constants. These identifiers begin and end with two underscores and often are useful to include additional information in error messages. These identifiers and the defined identifier cannot be used in #define or #undef directives. 

| Symbolic constant | Explanation                                                  |
| ----------------- | ------------------------------------------------------------ |
| \__LINE__         | The line number of the current source-code line (an integer constant). |
| \__FILE__         | The name of the source file (a string).                      |
| \__DATE__         | The date the source file was compiled (a string of the form "Mmm dd yyyy" such as "Jan 19 2002"). |
| \__TIME__         | The time the source file was compiled (a string literal of the form "hh:mm:ss"). |
| \__STDC__         | The value 1 if the compiler supports Standard C; 0 otherwise. Requires the compiler flag /Za in Visual C++. |

## Assertions

The assert macro—defined in —tests the value of an expression at execution time. If the value is false (0), assert prints an error message and calls function abort (of the general utilities library—) to terminate program execution. This is a useful debugging tool for testing whether a variable has a correct value. For example, suppose variable x should never be larger than 10 in a program. An assertion may be used to test the value of x and print an error message if the value of x is greater than 10. The statement would be

```c
assert(x <= 10);
```

If x is greater than 10 when the preceding statement executes, the program displays an error message containing the line number and filename where the assert statement appears, then terminates. You then concentrate on this area of the code to find the error. 

If the symbolic constant NDEBUG is defined, subsequent assertions will be ignored. Thus, when assertions are no longer needed, you can insert the line

```c
#define NDEBUG
```

in the code file rather than delete each assertion manually. Many compilers have debug and release modes that automatically define and undefine NDEBUG, respectively. 

## Secure C Programming

```c
#define CIRCLE_AREA(x) ((PI) * (x) * (x))
```

is considered to be an unsafe macro because it evaluates its argument x more than once. This can cause subtle errors. If the macro argument contains side effects—such as incrementing a variable or calling a function that modifies a variable’s value—those side effects would be performed multiple times. 

For example, if we call CIRCLE_AREA as follows:

```c
result = CIRCLE_AREA(++radius);
```

the call to the macro CIRCLE_AREA is expanded to:

```c
result = ((3.14159) * (++radius) * (++radius));
```

which increments radius twice in the statement. In addition, the result of the preceding statement is undefined because C allows a variable to be modified only once in a statement. In a function call, the argument is evaluated only once before it’s passed to the function. So, functions are always preferred to unsafe macros. 