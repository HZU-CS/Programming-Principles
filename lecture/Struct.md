# C Structures, Unions, Bit Manipulation and Enumerations

## Objectives

Create and use structs, unions and enums. 

Understand self-referential structs. 

Learn about the operations that can be performed on struct instances. 

Initialize struct members. 

Access struct members. 

Pass struct instances to functions by value and by reference. 

Use typedefs to create aliases for existing type names. 

Learn about the operations that can be performed on unions. 

Initialize unions. 

Manipulate integer data with the bitwise operators.

Create bit fields for storing data compactly.

Use enum constants.

Consider the security issues of working with structs, bit manipulation and enums.

## Introduction

Structures are collections of related variables under one name. They may contain variables of many different data types. 

Structures are commonly used to define records to be stored in files. 

Pointers and structures facilitate the formation of more complex data structures such as linked lists, queues, stacks and trees.

## Structure Definitions

Keyword struct introduces a structure definition

The identifier following keyword struct is the structure tag, which names the structure definition. The structure tag is used with the keyword struct to declare variables of the structure type

Variables declared within the braces of the structure definition are the structure’s members. 

Members of the same structure type must have unique names. 

Each structure definition must end with a semicolon.

Structure members can have primitive or aggregates data types. 

A structure cannot contain an instance of itself but may include a pointer to its type. 

A structure containing a member that’s a pointer to the same structure type is referred to as a selfreferential structure. Self-referential structures are used to build linked data structures.

Structure definitions create new data types that are used to define variables. 

Variables of a given structure type can be declared by placing a comma-separated list of variable names between the closing brace of the structure definition and its ending semicolon. 

The structure tag name is optional. If a structure definition does not contain a structure tag name, variables of the structure type may be declared only in the structure definition.

The only valid operations that may be performed on structures are assigning structure variables to variables of the same type, taking the address (&) of a structure variable, accessing the members of a structure variable and using the sizeof operator to determine the size of a structure variable. 

## Initializing Structures

Structures can be initialized using initializer lists.

If there are fewer initializers in the list than members in the structure, the remaining members are automatically initialized to 0 (or NULL if the member is a pointer). 

Members of structure variables defined outside a function definition are initialized to 0 or NULL if they’re not explicitly initialized in the external definition. 

Structure variables may be initialized in assignment statements by assigning a structure variable of the same type, or by assigning values to the individual members of the structure.

## Accessing Structure Members with . and ->

The structure member operator (.) and the structure pointer operator (->) are used to access structure members

The structure member operator accesses a structure member via the structure variable name. 

The structure pointer operator accesses a structure member via a pointer to the structure

## Using Structures with Functions

Structures may be passed to functions by passing individual structure members, by passing an entire structure or by passing a pointer to a structure. 

Stucture variables are passed by value by default. 

To pass a structure by reference, pass its address. Arrays of structures—like all other arrays—are automatically passed by reference. 

To pass an array by value, create a structure with the array as a member. Structures are passed by value, so the array is passed by value.

## typedef

The keyword typedef provides a mechanism for creating synonyms for previously defined types. 

Names for structure types are often defined with typedef to create shorter type names. 

Often, typedef is used to create synonyms for the basic data types. For example, a program requiring 4-byte integers may use type int on one system and type long on another. Programs designed for portability often use typedef to create an alias for 4-byte integers such as Integer. The alias Integer can be changed once in the program to make the program work on both systems.

## Unions

A union is declared with keyword union in the same format as a structure. Its members share the same storage space. 

The members of a union can be of any data type. The number of bytes used to store a union must be at least enough to hold the largest member. 

Only one member of a union can be referenced at a time. It’s your responsibility to ensure that the data in a union is referenced with the proper data type.

The operations that can be performed on a union are assigning a union to another of the same type, taking the address (&) of a union variable, and accessing union members using the structure member operator and the structure pointer operator. 

A union may be initialized in a declaration with a value of the same type as the first union member. 

## Bitwise Operators

Computers represent all data internally as sequences of bits with the values 0 or 1. 

On most systems, a sequence of 8 bits form a byte—the standard storage unit for a variable of type char. Other data types are stored in larger numbers of bytes.

The bitwise operators are used to manipulate the bits of integral operands (char, short, int and long; both signed and unsigned). Unsigned integers are normally used.

The bitwise operators are bitwise AND (&), bitwise inclusive OR (|), bitwise exclusive OR (^), left shift (<<), right shift (>>) and complement (~).

The bitwise AND, bitwise inclusive OR and bitwise exclusive OR operators compare their two operands bit by bit. The bitwise AND operator sets each bit in the result to 1 if the corresponding bit in both operands is 1. The bitwise inclusive OR operator sets each bit in the result to 1 if the corresponding bit in either (or both) operand(s) is 1. The bitwise exclusive OR operator sets each bit in the result to 1 if the corresponding bits both operands are different. 

The left-shift operator shifts the bits of its left operand to the left by the number of bits specified in its right operand. Bits vacated to the right are replaced with 0s; bits shifted off the left are lost. 

The right-shift operator shifts the bits in its left operand to the right by the number of bits specified in its right operand. Performing a right shift on an unsigned int causes the vacated bits at the left to be replaced by 0s; bits shifted off the right are lost. 

The bitwise complement operator sets all 0 bits in its operand to 1 and all 1 bits to 0 in the result.

 Often, the bitwise AND operator is used with an operand called a mask—an integer value with specific bits set to 1. Masks are used to hide some bits in a value while selecting other bits. 

The symbolic constant CHAR_BIT (defined in <limit.h>) represents the number of bits in a byte (normally 8). It can be used to make a bit-manipulation program more generic and portable. 

Each binary bitwise operator has a corresponding bitwise assignment operator

## Bit Fields

C enables you to specify the number of bits in which an unsigned or signed integral member of a structure or union is stored. This is referred to as a bit field. Bit fields enable better memory utilization by storing data in the minimum number of bits required.

A bit field is declared by following an unsigned int or int member name with a colon (:) and an integer constant representing the width of the field. The constant must be an integer between 0 and the total number of bits used to store an int on your system, inclusive. 

Bit-field members of structures are accessed exactly as any other structure member. 

It’s possible to specify an unnamed bit field to be used as padding in the structure

An unnamed bit field with a zero width aligns the next bit field on a new storage-unit boundary.

## Enumeration Constants

An enum defines a set of integer constants represented by identifiers. Values in an enum start with 0, unless specified otherwise, and are incremented by 1. 

The identifiers in an enum must be unique.

The value of an enum constant can be set explicitly via assignment in the enum definition. 

## Secure C Programming

### CERT Guidelines for structs 

The boundary alignment requirements for struct members may result in extra bytes containing undefined data for each struct variable you create. Each of the following guidelines is related to this issue:

EXP03-C: Because of boundary alignment requirements, the size of a struct variable is not necessarily the sum of its members’ sizes. Always use sizeof to determine the number of bytes in a struct variable. As you’ll see, we use this technique to manipulate fixed-length records that are written to and read from files, and to create so-called dynamic data structures. 

EXP04-C: Struct variables cannot be compared for equality or inequality, because they might contain bytes of undefined data. Therefore, you must compare their individual members.

DCL39-C: In a struct variable, the undefined extra bytes could contain secure data—left over from prior use of those memory locations—that should not be accessible. This CERT guideline discusses compiler-specific mechanisms for packing the data to eliminate these extra bytes.

### CERT Guideline for typedef

DCL05-C: Complex type declarations, such as those for function pointers, can be difficult to read. You should use typedef to create self-documenting type names that make your programs more readable. 

### CERT Guidelines for Bit Manipulation

INT02-C: As a result of the integer promotion rules, performing bitwise operations on integer types smaller than int can lead to unexpected results. Explicit casts are required to ensure correct results.

INT13-C: Some bitwise operations on signed integer types are implementation defined—this means that the operations may have different results across C compilers. For this reason, unsigned integer types should be used with the bitwise operators.

EXP46-C: The logical operators && and || are frequently confused with the bitwise operators & and |, respectively. Using & and | in the condition of a conditional expression (?:) can lead to unexpected behavior, because the & and | operators do not use short-circuit evaluation. 

### CERT Guideline for enum

INT09-C: Allowing multiple enumeration constants to have the same value can result in difficult-to-find logic errors. In most cases, an enum’s enumeration constants should each have unique values to help prevent such logic errors.