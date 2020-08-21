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

```c
printf( "Welcome to C!\n" );
```

instructs the computer to perform an action, namely to print on the screen the string of characters marked by the quotation marks. A string is sometimes called a character string, a message or a literal. The entire line, including the printf function (the “f” stands for “formatted”), its argument within the parentheses and the semicolon (;), is called a statement. Every statement must end with a semicolon (also known as the statement terminator). When the preceding printf statement is executed, it prints the message Welcome to C! on the screen. The characters normally print exactly as they appear between the double quotes in the printf statement. 

### Escape Sequences

Notice that the characters \n were not printed on the screen. The backslash (\) as used here is called an escape character. It indicates that printf is supposed to do something out of the ordinary. When encountering a backslash in a string, the compiler looks ahead at the next character and combines it with the backslash to form an escape sequence. The escape sequence \n means newline. When a newline appears in the string output by a printf, the newline causes the cursor to position to the beginning of the next line on the screen.

| Escape sequence | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| \n              | Newline. Position the cursor at the beginning of the next line |
| \t              | Horizontal tab. Move the cursor to the next tab stop         |
| \a              | Alert. Produces a sound or visible alert without changing the current cursor position |
| \\\             | Backslash. Insert a backslash character in a string          |
| \\"             | Double quote. Insert a double-quote character in a string    |

Because the backslash has special meaning in a string, i.e., the compiler recognizes it as an escape character, we use a double backslash (\\) to place a single backslash in a string. Printing a double quote also presents a problem because double quotes mark the boundaries of a string—such quotes are not printed. By using the escape sequence \" in a string to be output by printf, we indicate that printf should display a double quote. The right brace, }, indicates that the end of main has been reached. 

We said that printf causes the computer to perform an action. As any program executes, it performs a variety of actions and makes decisions. 

### Return Value

Return a value to the caller.

Normally, returning 0 means ok, 1 means error.

### The Linker and Executables

Standard library functions like printf and scanf are not part of the C programming language. For example, the compiler cannot find a spelling error in printf or scanf. When the compiler compiles a printf statement, it merely provides space in the object program for a “call” to the library function. But the compiler does not know where the library functions are—the linker does. When the linker runs, it locates the library functions and inserts the proper calls to these library functions in the object program. Now the object program is complete and ready to be executed. For this reason, the linked program is called an executable. If the function name is misspelled, the linker will spot the error, because it will not be able to match the name in the C program with the name of any known function in the libraries.

### Using Multiple printfs

```c
#include <stdio.h>

int main(void) {
    printf("Welcome ");
    printf("to C!\n");
    return 0;
}
```

 This works because each printf resumes printing where the previous printf stopped printing. The first printf prints Welcome followed by a space (but no newline), and the second printf  begins printing on the same line immediately following the space. 

```c
#include <stdio.h>

int main(void) {
    printf("Welcome\nto\nC!\n");
    return 0;
}
```

One printf can print several lines by using additional newline characters. Each time the \n (newline) escape sequence is encountered, output continues at the beginning of the next line. 

## Another Simple C Program: Adding Two Integers

```c
// Addition program.
#include <stdio.h>

int main(void)
{
    int integer1; // first number to be entered by user
    int integer2; // second number to be entered by user

    printf("Enter first integer\n"); // prompt
    scanf("%d", &integer1);          // read an integer

    printf("Enter second integer\n"); // prompt
    scanf("%d", &integer2);           // read an integer

    int sum;                   // variable in which sum will be stored
    sum = integer1 + integer2; // assign total to sum

    printf("Sum is %d\n", sum); // print sum

    return 0;
} // end function main
```

### Variables and Variable Definitions

```c
int integer1; // first number to be entered by user
int integer2; // second number to be entered by user
```

are definitions. The names integer1 and integer2 are the names of variables—locations in memory where values can be stored for use by a program. These definitions specify that variables integer1 and integer2 are of type int, which means that they’ll hold integer values, i.e., whole numbers such as 7, –11, 0, 31914 and the like. 

### Define Variables Before They Are Used

All variables must be defined with a name and a data type before they can be used in a program. The C standard allows you to place each variable definition anywhere in main before that variable’s first use in the code (though some older compilers do not allow this). You’ll see later why you should define variables close to their first use.

### Defining Multiple Variables of the Same Type in One Statement

The preceding definitions could be combined into a single definition as follows:

```c
int integer1, integer2;
```

but that would have made it difficult to associate comments with each of the variables. 

### Identifiers and Case Sensitivity

A variable name in C can be any valid identifier. An identifier is a series of characters consisting of letters, digits and underscores (_) that does not begin with a digit. C is case sensitive—uppercase and lowercase letters are different in C, so a1 and A1 are different identifiers. 

### Prompting Messages

```c
printf( "Enter first integer\n" ); // prompt
```

displays the literal "Enter first integer" and positions the cursor to the beginning of the next line. This message is called a prompt because it tells the user to take a specific action. 

### The scanf Function and Formatted Inputs

```c
scanf( "%d", &integer1 ); // read an integer
```

uses scanf (the “f” stands for “formatted”) to obtain a value from the user. The function reads from the standard input, which is usually the keyboard. 

This scanf has two arguments, "%d" and &integer1. The first, the format control string, indicates the type of data that should be entered by the user. The %d conversion specifier indicates that the data should be an integer (the letter d stands for “decimal integer”). The % in this context is treated by scanf (and printf as we’ll see) as a special character that begins a conversion specifier. 

The second argument of scanf begins with an ampersand (&)—called the address operator—followed by the variable name. The &, when combined with the variable name, tells scanf the location (or address) in memory at which the variable integer1 is stored. The computer then stores the value that the user enters for integer1 at that location. The use of ampersand (&) is often confusing to novice programmers or to people who have programmed in other languages that do not require this notation. For now, just remember to precede each variable in every call to scanf with an ampersand.

When the computer executes the preceding scanf, it waits for the user to enter a value for variable integer1. The user responds by typing an integer, then pressing the Enter key (sometimes labeled as the Return key) to send the number to the computer. The computer then assigns this number, or value, to the variable integer1. Any subsequent references to integer1 in this program will use this same value. Functions printf and scanf facilitate interaction between the user and the computer. This interaction resembles a dialogue and is often called interactive computing.

### Prompting for and Inputting the Second Integer

```c
printf( "Enter second integer\n" ); // prompt
```

displays the message Enter second integer on the screen, then positions the cursor to the beginning of the next line. This printf also prompts the user to take action. 

```c
scanf( "%d", &integer2 ); // read an integer
```

obtains a value for variable integer2 from the user. 

### Defining the sum Variable

```c
int sum; // variable in which sum will be stored
```

defines the variable sum of type int just before its first use. 

### Assignment Statement

```c
sum = integer1 + integer2; // assign total to sum
```

calculates the total of variables integer1 and integer2 and assigns the result to variable sum using the assignment operator =. The statement is read as, “sum gets the value of the expression integer1 + integer2.” Most calculations are performed in assignments. The = operator and the + operator are called binary operators because each has two operands. The + operator’s operands are integer1 and integer2. The = operator’s two operands are sum and the value of the expression integer1 + integer2. 

### Printing with a Format Control String

```c
printf( "Sum is %d\n", sum ); // print sum
```

calls function printf to print the literal Sum is followed by the numerical value of variable sum on the screen. This printf has two arguments, "Sum is %d\n" and sum. The first is the format control string. It contains some literal characters to be displayed and the conversion specifier %d indicating that an integer will be printed. The second argument specifies the value to be printed. The conversion specifier for an integer is the same in both printf and scanf—this is true for most C data types. 

### Combining a Variable Definition and Assignment Statement

You can assign a value to a variable in its definition—this is known as initializing the variable. 

```c
int sum = integer1 + integer2; // assign total to sum
```

which adds integer1 and integer2, then stores the result in the variable sum. 

### Calculations in printf Statements

Calculations can also be performed inside printf statements.

```c
printf( "Sum is %d\n", integer1 + integer2 );
```

in which case the variable sum is not needed. 

## Memory Concepts

Variable names such as integer1, integer2 and sum actually correspond to locations in the computer’s memory. Every variable has a name, a type and a value. When

```c
scanf("%d", &integer1);
```

is executed, the value entered by the user is placed into a memory location to which the name integer1 has been assigned. Suppose the user enters the number 45 as the value for integer1. The computer will place 45 into location integer1.

![memory](./C_Intro/memory1.png)

Whenever a value is placed in a memory location, the value ***replaces*** the previous value in that location and the previous value is lost; thus, this process is said to be destructive. When

```c
scanf("%d", &integer2);
```

executes, suppose the user enters the value 72. This value is placed into the location integer2. These locations are not necessarily adjacent in memory. 

![memory2](./C_Intro/memory2.png)

Once the program has obtained values for integer1 and integer2, it adds these values and places the total into variable sum. The statement

```c
sum = integer1 + integer2; // assign total to sum
```

that performs the addition also replaces whatever value was stored in sum. This occurs when the calculated total of integer1 and integer2 is placed into location sum (destroying the value already in sum). The values of integer1 and integer2 appear exactly as they did before they were used in the calculation. They were used, but not destroyed, as the computer performed the calculation. Thus, when a value is read from a memory location, the process is said to be ***nondestructive***. 

![memory3](./C_Intro/memory3.png)

## Arithmetic in C

Most C programs perform calculations using the C arithmetic operators.

| C Operation    | Arithmetic operator | Algebraic expression | C expression |
| -------------- | ------------------- | -------------------- | ------------ |
| Addition       | +                   | f + 7                | f + 7        |
| Subtraction    | -                   | p – c                | p - c        |
| Multiplication | *                   | bm                   | b * m        |
| Division       | /                   | x / y or x ÷ y       | x / y        |
| Remainder      | %                   | r mod s              | r % s        |

The arithmetic operators are all binary operators.

### Integer Division and the Remainder Operator

Integer division yields an integer result. For example, the expression 7 / 4 evaluates to 1 and the expression 17 / 5 evaluates to 3. C provides the remainder operator, %, which yields the remainder after integer division. The remainder operator is an integer operator that can be used only with integer operands. The expression x % y yields the remainder after x is divided by y. Thus, 7 % 4 yields 3 and 17 % 5 yields 2.

### Arithmetic Expressions in Straight-Line Form

Arithmetic expressions in C must be written in straight-line form to facilitate entering programs into the computer. Thus, expressions such as “a divided by b” must be written as a/b so that all operators and operands appear in a straight line. The algebraic notation fraction is generally not acceptable to compilers, although some special-purpose software packages do support more natural notation for complex mathematical expressions.

### Parentheses for Grouping Subexpressions

Parentheses are used in C expressions in the same manner as in algebraic expressions. For example, to multiply a times the quantity b + c we write a*(b+c).

### Rules of Operator Precedence

C applies the operators in arithmetic expressions in a precise sequence determined by the following rules of operator precedence, which are generally the same as those in algebra

Operators in expressions contained within pairs of parentheses are evaluated first. Parentheses are said to be at the “highest level of precedence.” In cases of nested, or embedded, parentheses, such as

```c
((a + b) + c)
```

the operators in the innermost pair of parentheses are applied first. 

Multiplication, division and remainder operations are applied next. If an expression contains several multiplication, division and remainder operations, evaluation proceeds from left to right. Multiplication, division and remainder are said to be on the same level of precedence.

Addition and subtraction operations are evaluated next. If an expression contains several addition and subtraction operations, evaluation proceeds from left to right. Addition and subtraction also have the same level of precedence, which is lower than the precedence of the multiplication, division and remainder operations.

The assignment operator (=) is evaluated last.

The rules of operator precedence specify the order C uses to evaluate expressions.1 When we say evaluation proceeds from left to right, we’re referring to the associativity of the operators. We’ll see that some operators associate from right to left.

| Operators | Operations                        | Order of evaluation                                          |
| --------- | --------------------------------- | ------------------------------------------------------------ |
| ()        | Parentheses                       | Evaluated first. If the parentheses are nested, the expression in the innermost pair is evaluated first. If there are several pairs of parentheses “on the same level” (i.e., not nested), they’re evaluated left to right |
| */%       | Multiplication Division Remainder | Evaluated second. If there are several, they’re evaluated left to right. |
| +-        | Addition Subtraction              | Evaluated third. If there are several, they’re evaluated left to right. |
| =         | Assignment                        | Evaluated last.                                              |

### Sample Algebraic and C Expressions

### Evaluation of a Second-Degree Polynomial

### Using Parentheses for Clarity

As in algebra, it’s acceptable to place unnecessary parentheses in an expression to make the expression clearer. These are called redundant parentheses. 

```c
y = ( a * x * x ) + ( b * x ) + c;
```

## Decision Making: Equality and Relational Operators

Executable statements either perform actions (such as calculations or input or output of data) or make decisions (we’ll soon see several examples of these). We might make a decision in a program, for example, to determine whether a person’s grade on an exam is greater than or equal to 60 and whether the program should print the message “Congratulations! You passed.” This section introduces a simple version of C’s if statement that allows a program to make a decision based on the truth or falsity of a statement of fact called a condition. If the condition is true (i.e., the condition is met), the statement in the body of the if statement is executed. If the condition is false (i.e., the condition isn’t met), the body statement isn’t executed. Whether the body statement is executed or not, after the if statement completes, execution proceeds with the next statement in sequence after the if statement. 

Conditions in if statements are formed by using the equality operators and relational operators. The relational operators all have the same level of precedence and they associate left to right. The equality operators have a lower level of precedence than the relational operators and they also associate left to right. [Note: In C, a condition may actually be any expression that generates a zero (false) or nonzero (true) value.]

| Algebraic equality or relational operator | C equality or relational operator | Example of C condition | Meaning of C condition          |
| ----------------------------------------- | --------------------------------- | ---------------------- | ------------------------------- |
| Relational operators                      |                                   |                        |                                 |
| >                                         | >                                 | x > y                  | x is greater than y             |
| <                                         | <                                 | x < y                  | x is less than y                |
| ≥                                         | >=                                | x >= y                 | x is greater than or equal to y |
| ≤                                         | <=                                | x <= y                 | x is less than or equal to y    |
| Equality operators                        |                                   |                        |                                 |
| =                                         | ==                                | x == y                 | x is equal to y                 |
| ≠                                         | !=                                | x != y                 | x is not equal to y             |

```c
// Using if statements, relational
// operators, and equality operators.
#include <stdio.h>

int main(void)
{
    printf("Enter two integers, and I will tell you\n");
    printf("the relationships they satisfy: ");

    int num1; // first number to be read from user
    int num2; // second number to be read from user

    scanf("%d %d", &num1, &num2); // read two integers

    if (num1 == num2)
    {
        printf("%d is equal to %d\n", num1, num2);
    } // end if

    if (num1 != num2)
    {
        printf("%d is not equal to %d\n", num1, num2);
    } // end if

    if (num1 < num2)
    {
        printf("%d is less than %d\n", num1, num2);
    } // end if

    if (num1 > num2)
    {
        printf("%d is greater than %d\n", num1, num2);
    } // end if

    if (num1 <= num2)
    {
        printf("%d is less than or equal to %d\n", num1, num2);
    } // end if

    if (num1 >= num2)
    {
        printf("%d is greater than or equal to %d\n", num1, num2);
    } // end if

    return 0;
}
```

The program uses scanf to read two integers into the int variables num1 and num2. Each conversion specifier has a corresponding argument in which a value will be stored. The first %d converts a value to be stored in the variable num1, and the second %d converts a value to be stored in the variable num2. 

### Comparing Numbers

```c
if (num1 == num2) {
    printf( "%d is equal to %d\n", num1, num2 );
} // end if
```

compares the values of variables num1 and num2 to test for equality. If the values are equal, the printf statement displays a line of text indicating that the numbers are equal. If the conditions are true in one or more of the if statements, the corresponding body statement displays an appropriate line of text. Indenting the body of each if statement and placing blank lines above and below each if statement enhances program readability.

A left brace, {, begins the body of each if statement . A corresponding right brace, }, ends each if statement’s body. Any number of statements can be placed in the body of an if statement.

Operators are shown top to bottom in decreasing order of precedence. The equals sign is also an operator. All these operators, with the exception of the assignment operator =, associate from left to right. The assignment operator (=) associates from right to left. 

| Operators | Associativity |
| --------- | ------------- |
| ()        | left to right |
| * / %     | left to right |
| + -       | left to right |
| < <= > >= | left to right |
| == !=     | left to right |
| =         | right to left |

Some of the words we’ve used in the C programs in this chapter—in particular int, if and void—are keywords or reserved words of the language.  You must be careful not to use these as identifiers such as variable names. 

In this chapter, we’ve introduced many important features of the C programming language, including displaying data on the screen, inputting data from the user, performing calculations and making decisions. In the next chapter, we build upon these techniques as we introduce structured programming. You’ll become more familiar with indentation techniques. We’ll study how to specify the order in which statements are executed—this is called flow of control.

```c
// Keywords
auto do goto signed unsigned
break double if sizeof void
case else int static volatile
char enum long struct while
const extern register switch
continue float return typedef
default for short union
// Keywords added in C99 standard
_Bool _Complex _Imaginary inline restrict
// Keywords added in C11 standard
_Alignas _Alignof _Atomic _Generic _Noreturn _Static_assert _Thread_local
```

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