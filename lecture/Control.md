# C Program Control

## Objectives

The essentials of countercontrolled iteration. 

To use the for and do…while iteration statements to execute statements repeatedly.

To understand multiple selection using the switch selection statement. 

To use the break and continue statements to alter the flow of control. 

To use the logical operators to form complex conditional expressions in control statements. 

To avoid the consequences of confusing the equality and assignment operators.

## Introduction

You should now be comfortable with writing simple, complete C programs. In this chapter, iteration is considered in greater detail, and additional iteration control statements, namely the for and the do…while, are presented. The switch multiple-selection statement is introduced. We discuss the break statement for exiting immediately from certain control statements, and the continue statement for skipping the remainder of the body of an iteration statement, then proceeding with the next iteration of the loop. 

## Iteration Essentials

Most programs involve iteration, or looping. A loop is a group of instructions the computer executes repeatedly while some loop-continuation condition remains true. We’ve discussed two means of iteration:

1. Counter-controlled iteration
2. Sentinel-controlled iteration

Counter-controlled iteration is sometimes called definite iteration because we know in advance exactly how many times the loop will be executed. Sentinel-controlled iteration is sometimes called indefinite iteration because it’s not known in advance how many times the loop will be executed.

In counter-controlled iteration, a control variable is used to count the number of iterations. The control variable is incremented (usually by 1) each time the group of instructions is performed. When the value of the control variable indicates that the correct number of iterations has been performed, the loop terminates and execution continues with the statement after the iteration statement

Sentinel values are used to control iteration when:

1. The precise number of iterations isn’t known in advance, and
2. The loop includes statements that obtain data each time the loop is performed.

The sentinel value indicates “end of data.” The sentinel is entered after all regular data items have been supplied to the program. Sentinels must be distinct from regular data items.

## Counter-Controlled Iteration

Counter-controlled iteration requires:

1. The name of a control variable (or loop counter).
2. The initial value of the control variable.
3. The increment (or decrement) by which the control variable is modified each time through the loop.
4. The condition that tests for the final value of the control variable (i.e., whether looping should continue).

```c
#include <stdio.h>

int main(void) {
    unsigned int counter = 1; // initialization
    
    while (counter <= 10) { // iteration condition
        printf("%u\n", counter);
        ++counter; // increment
    }
}
```

The definition and initialization of counter also could have been written as

```c
unsigned int counter;
counter = 1;
```

The definition is not executable, but the assignment is. We’ll use both methods of setting the values of variables. 

The statement

```c
++counter; // increment
```

increments the loop counter by 1 each time the loop is performed. The loop-continuation condition in the while statement tests whether the value of the control variable is less than or equal to 10 (the last value for which the condition is true). The body of this while is performed even when the control variable is 10. The loop terminates when the control variable exceeds 10 (i.e., counter becomes 11).

You could make the program more concise by initializing counter to 0 and by replacing the while statement with

```c
while (++counter <= 10) {
    printf("%u\n", counter);
}
```

This code saves a statement because the incrementing is done directly in the while condition before the condition is tested. Coding in such a condensed fashion takes some practice. Some programmers feel that this makes the code too cryptic and error prone. 

## for Iteration Statement

The for iteration statement handles all the details of counter-controlled iteration. 

```c
#include <stdio.h>

int main(void) {
    // initialization, iteration condition, and increment 
    // are all included in the for statement header.
    for (unsigned int counter = 1; counter <= 10; ++counter) {
        printf("%u\n", counter);
    }
}
```

### for Statement Header Components

Notice that the for statement “does it all”—it specifies each of the items needed for counter-controlled iteration with a control variable. If there’s more than one statement in the body of the for, braces are required to define the body of the loop, you should always place a control statement’s body in braces, even if it has only one statement. 

![for](./Control/for.png)

### Control Variables Defined in a for Header Exist Only Until the Loop Terminates

When you define the control variable in the for header before the first semicolon (;)

```c
for (unsigned int counter = 1; counter <= 10; ++counter) {
```

the control variable exists only until the loop terminates. 

### Off-By-One Errors

If you incorrectly wrote counter < 10, then the loop would be executed only 9 times. This is a common logic error called an off-by-one error.

### General Format of a for Statement

The general format of the for statement is 

```c
for (initialization; condition; increment) {
	statement
}
```

where the initialization expression initializes the loop-control variable, the condition expression is the loop-continuation condition and the increment expression increments the control variable.

