# Other C Topics

## Objectives

Redirect program input to come from a file. 

Redirect program output to be placed in a file. 

Write functions that use variable-length argument lists. 

Process command-line arguments. 

Compile multiple-source-file programs. 

Assign specific types to numeric constants. 

Terminate programs with exit and at exit . 

Process external asynchronous events in a program. 

Dynamically allocate arrays and resize memory that was dynamically allocated previously

## Introduction

This chapter presents additional topics not ordinarily covered in introductory courses. Many of the capabilities discussed here are specific to particular operating systems, especially Linux/UNIX and Windows.

## Redirecting I/O

In command-line applications, normally the input is received from the keyboard (standard input), and the output is displayed on the screen (standard output). On most computer systems—Linux/UNIX, Mac OS X and Windows systems in particular—it’s possible to redirect inputs to come from a file rather than the keyboard and redirect outputs to be placed in a file rather than on the screen. Both forms of redirection can be accomplished without using the file-processing capabilities of the standard library (e.g., by changing your code to use fprintf rather than printf, etc.). Students often find it difficult to understand that redirection is an operating-system function, not another C feature.

### Redirecting Input with <

There are several ways to redirect input and output from the command line—that is, a Command Prompt window in Windows, a shell in Linux or a Terminal window in Mac OS X. Consider the executable file sum (on Linux/UNIX systems) that inputs integers one at a time and keeps a running total of the values until the end-of-file indicator is set, then prints the result. Normally the user inputs integers from the keyboard and enters the endof-file key combination to indicate that no further values will be input. With input redirection, the input can be read from a file. For example, if the data is stored in file input, the command line

```shell
sum < input
```

executes the program sum; the redirect input symbol (<) indicates that the data in file input is to be used as the program’s input. Redirecting input on a Windows system or in a Terminal window on OS X is performed identically. The character $ shown in the line above is a typical Linux/UNIX command-line prompt (some systems use a % prompt or other symbol).

### Redirecting Input with |

The second method of redirecting input is piping. A pipe (|) causes the output of one program to be redirected as the input to another. Suppose program random outputs a series of random integers; the output of random can be “piped” directly to program sum using the command line 

```shell
random | sum
```

This causes the sum of the integers produced by random to be calculated. Piping is performed identically in Linux/UNIX, Windows and OS X.

### Redirecting Output

The standard output stream can be redirected to a file by using the redirect output symbol (>). For example, to redirect the output of program random to file out, use 

```shell
random > out
```

Finally, program output can be appended to the end of an existing file by using the append output symbol (>>). For example, to append the output from program random to file out created in the preceding command line, use the command line

```shell
random >> out
```

## Variable-Length Argument Lists

It’s possible to create functions that receive an unspecified number of arguments. Most programs in the text have used the standard library function printf, which, as you know, takes a variable number of arguments. As a minimum, printf must receive a string as its first argument, but printf can receive any number of additional arguments. The function prototype for printf is

```c
int printf(const char *format, ...);
```

The ellipsis (…) in the function prototype indicates that the function receives a variable number of arguments of any type. The ellipsis must always be placed at the end of the parameter list.

The macros and definitions of the variable arguments headers provide the capabilities necessary to build functions with variable-length argument lists.

| Identifier | Explanation                                                  |
| ---------- | ------------------------------------------------------------ |
| va_list    | A type suitable for holding information needed by macros va_start, va_arg and va_end. To access the arguments in a variable-length argument list, an object of type va_list must be defined. |
| va_start   | A macro that’s invoked before the arguments of a variable-length argument list can be accessed. The macro initializes the object declared with va_list for use by the va_arg and va_end macros. |
| va_arg     | A macro that expands to the value of the next argument in the variablelength argument list—the value has the type specified as the macro’s second argument. Each invocation of va_arg modifies the object declared with va_list so that it points to the next argument in the list. |
| va_end     | A macro that facilitates a normal return from a function whose variablelength argument list was referred to by the va_start macro. |

You might wonder how functions with variable-length argument lists like printf and function scanf know what type to use in each va_arg macro. The answer is that, as the program executes, they scan the format conversion specifiers in the format control string to determine the type of the next argument to be processed.

## Using Command-Line Arguments

On many systems, it’s possible to pass arguments to main from a command line by including parameters int argc and char *argv[] in the parameter list of main. Parameter argc receives the number of command-line arguments that the user has entered. Parameter argv is an array of strings in which the actual command-line arguments are stored. Common uses of command-line arguments include passing options to a program and passing filenames to a program. 

## Compiling Multiple-Source-File Programs

It’s possible to build programs that consist of multiple source files. There are several considerations when creating programs in multiple files. For example, the definition of a function must be entirely contained in one file—it cannot span two or more files.

### extern Declarations for Global Variables in Other Files

We learned that variables declared outside any function definition are referred to as global variables. Global variables are accessible to any function defined in the same file after the variable is declared. Global variables also are accessible to functions in other files. However, the global variables must be declared in each file in which they’re used. For example, to refer to global integer variable flag in another file, you can use the declaration 

```c
extern int flag;
```

This declaration uses the storage-class specifier extern to indicate that variable flag is defined either later in the same file or in a different file. The compiler informs the linker that unresolved references to variable flag appear in the file. If the linker finds a proper global definition, the linker resolves the references by indicating where flag is located. If the linker cannot locate a definition of flag, it issues an error message and does not produce an executable file. Any identifier that’s declared at file scope is extern by default. 

### Function Prototypes

Just as extern declarations can be used to declare global variables to other program files, function prototypes can extend the scope of a function beyond the file in which it’s defined (the extern specifier is not required in a function prototype). Simply include the function prototype in each file in which the function is invoked and compile the files together. Function prototypes indicate to the compiler that the specified function is defined either later in the same file or in a different file. Again, the compiler does not attempt to resolve references to such a function—that task is left to the linker. If the linker cannot locate a proper function definition, the linker issues an error message. 

As an example of using function prototypes to extend the scope of a function, consider any program containing the preprocessor directive #include , which includes a file containing the function prototypes for functions such as printf and scanf. Other functions in the file can use printf and scanf to accomplish their tasks. The printf and scanf functions are defined in other files. We do not need to know where they’re defined. We’re simply reusing their code in our programs. The linker resolves our references to these functions automatically. This process enables us to use the functions in the standard library.

### Restricting Scope with static

It’s possible to restrict the scope of a global variable or a function to the file in which it’s defined. The storage-class specifier static, when applied to a global variable or a function, prevents it from being used by any function that’s not defined in the same file. This is referred to as internal linkage. Global variables and functions that are not preceded by static in their definitions have external linkage—they can be accessed in other files if those files contain proper declarations and/or function prototypes. 

The global variable declaration 

```c
static const double PI = 3.14159;
```

creates constant variable PI of type double, initializes it to 3.14159 and indicates that PI is known only to functions in the file in which it’s defined. 

The static specifier is commonly used with utility functions that are called only by functions in a particular file. If a function is not required outside a particular file, the principle of least privilege should be enforced by applying static to both the function’s definition and prototype.

### Makefiles

When building large programs in multiple source files, compiling the program becomes tedious if small changes are made to one file and the entire program is needlessly recompiled. Many systems provide special utilities that recompile only the modified program files. On Linux/UNIX systems the utility is called make. Utility make reads a file called makefile that contains instructions for compiling and linking the program. Products such as Eclipse™ and Microsoft® Visual C++® provide similar utilities. 

## Program Termination with exit and atexit

The general utilities library () provides methods of terminating program execution by means other than a conventional return from function main. Function exit causes a program to terminate immediately. The function often is used to terminate a program when an input error is detected, or when a file to be processed by the program cannot be opened. Function atexit registers a function that should be called when the program terminates by reaching the end of main or when exit is invoked. 

Function atexit takes as an argument a pointer to a function (i.e., the function name). Functions called at program termination cannot have arguments and cannot return a value. 

Function exit takes one argument. The argument is normally the symbolic constant EXIT_SUCCESS or the symbolic constant EXIT_FAILURE. If exit is called with EXIT_SUCCESS, the implementation-defined value for successful termination is returned to the calling environment. If exit is called with EXIT_FAILURE, the implementation-defined value for unsuccessful termination is returned. When function exit is invoked, any functions previously registered with atexit are invoked in the reverse order of their registration. 

## Suffixes for Integer and Floating-Point Literals

C provides integer and floating-point suffixes for explicitly specifying the data types of integer and floating-point literal values. (The C standard refers to such literal values as constants). If an integer literal is not suffixed, its type is determined by the first type capable of storing a value of that size (first int, then long int, then unsigned long int, etc.). A floating-point literal that’s not suffixed is automatically of type double.

The integer suffixes are: u or U for an unsigned int, l or L for a long int, and ll or LL for a long long int. You can combine u or U with those for long int and long long int to create unsigned literals for the larger integer types. The following literals are of type unsigned int, long int, unsigned long int and unsigned long long int, respectively:

```c
174u
8358L
28373ul
9876543210llu
```

The floating-point suffixes are: f or F for a float, and l or L for a long double. The following constants are of type float and long double, respectively:

```c
1.28f
3.14159L
```

## Signal Handling

An external asynchronous event, or signal, can cause a program to terminate prematurely. Some events include interrupts (typing  c on a Linux/UNIX or Windows system or c on OS X) and termination orders from the operating system. The signalhandling library () provides the capability to trap unexpected events with function signal. Function signal receives two arguments—an integer signal number and a pointer to the signal-handling function. Signals can be generated by function raise, which takes an integer signal number as an argument.

| Signal  | Explanation                                                  |
| ------- | ------------------------------------------------------------ |
| SIGABRT | Abnormal termination of the program (such as a call to function abort). |
| SIGFPE  | An erroneous arithmetic operation, such as a divide-by-zero or an operation resulting in overflow. |
| SIGILL  | Detection of an illegal instruction.                         |
| SIGINT  | Receipt of an interactive attention signal ( c or  c).       |
| SIGSEGV | An attempt to access memory that is not allocated to a program. |
| SIGTERM | A termination request sent to the program.                   |

## Dynamic Memory Allocation: Functions calloc and realloc

Arrays are better than linked lists for rapid sorting, searching and data access. However, arrays are normally static data structures. The general utilities library (stdlib.h) provides two other functions for dynamic memory allocation—calloc and realloc. These functions can be used to create and modify dynamic arrays. Function calloc dynamically allocates memory for an array. The prototype for calloc is

```c
void *calloc(size_t nmemb, size_t size);
```

Its two arguments represent the number of elements (nmemb) and the size of each element (size). Function calloc also initializes the elements of the array to zero. The function returns a pointer to the allocated memory, or a NULL pointer if the memory is not allocated. The primary difference between malloc and calloc is that calloc clears the memory it allocates and malloc does not.

Function realloc changes the size of an object allocated by a previous call to malloc, calloc or realloc. The original object’s contents are not modified provided that the amount of memory allocated is larger than the amount allocated previously. Otherwise, the contents are unchanged up to the size of the new object. The prototype for realloc is 

```c
void *realloc(void *ptr, size_t size);
```

The two arguments are a pointer to the original object (ptr) and the new size of the object (size). If ptr is NULL, realloc works identically to malloc. If ptr is not NULL and size is greater than zero, realloc tries to allocate a new block of memory for the object. If the new space cannot be allocated, the object pointed to by ptr is unchanged. Function realloc returns either a pointer to the reallocated memory, or a NULL pointer to indicate that the memory was not reallocated.

## Unconditional Branching with goto

We’ve stressed the importance of using structured programming techniques to build reliable software that’s easy to debug, maintain and modify. In some cases, performance is more important than strict adherence to structured programming techniques. In these cases, some unstructured programming techniques may be used. For example, we can use break to terminate execution of an iteration statement before the loop-continuation condition becomes false. This saves unnecessary iterations of the loop if the task is completed before loop termination.

Another instance of unstructured programming is the goto statement—an unconditional branch. The result of the goto statement is a change in the flow of control to the first statement after the label specified in the goto statement. A label is an identifier followed by a colon. A label must appear in the same function as the goto statement that refers to it. Labels need not be unique among functions.

When the rules of structured programming are followed, it’s possible to create deeply nested control structures within a function from which it’s difficult to escape efficiently. Some programmers use goto statements in such situations as a quick exit from a deeply nested structure. This eliminates the need to test multiple conditions to escape from a control structure. There are some additional situations where goto is actually recommended—see, for example, CERT recommendation MEM12-C, “Consider using a Goto-Chain when leaving a function on error when using and releasing resources.” 