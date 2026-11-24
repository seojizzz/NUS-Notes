# CS1010 Programming Methodology - Lecture Notes
*By Seojin*

<details>

<summary>Table of contents</summary>

* [CS1010 Programming Methodology - Lecture Notes](#cs1010-programming-methodology---lecture-notes)
    * [Admin matters](#admin-matters)

* [L0: Introduction](#l0-introduction)
    * [0.0 Programming](#00-programming)
    * [0.1 Basic Program](#01-basic-program)
    * [0.2 Variables and data storage](#02-variables-and-data-storage)
        * [0.2.1 Variables](#021-variables)
        * [0.2.2 Format Specifiers](#022-format-specifiers)
    * [0.3 Arithmetic and Assignment Operators](#03-arithmetic-and-assignment-operators)
        * [0.3.1 Arithmetic Operators](#031-arithmetic-operators)
        * [0.3.2 Unary operators](#032-unary-operators)
        * [0.3.3 Comparison Operators](#033-comparison-operators)
        * [0.3.4 Logic Operators](#034-logic-operators)
        * [0.3.5 Assignment Operators](#035-assignment-operators)
        * [0.3.6 Integer Division](#036-integer-division)
        * [0.3.7 Division with `double`](#037-division-with-double)
        * [0.3.8 Operator Precedence](#038-operator-precedence)
    * [0.4 Ternary Operators](#04-ternary-operators)
        * [Common condition tests](#common-condition-tests)
    * [0.5 Undefined Behaviour](#05-undefined-behaviour)
        * [Example: Division by zero](#example-division-by-zero)
        * [Integer Overflow](#integer-overflow)
        * [Key takeaway](#key-takeaway)
    * [0.X Lab](#0x-lab)

* [L1: Conditionals and Functions](#l1-conditionals-and-functions)
    * [1.1 Abstraction I: Functions](#11-abstraction-i-functions)
    * [1.2 Conditional Statements](#12-conditional-statements)
        * [1.2.1 If/else constructs](#121-ifelse-constructs)
        * [1.2.2 Comparison and logical operators](#122-comparison-and-logical-operators)
        * [1.2.3 Boolean operators](#123-boolean-operators)
    * [1.X Lab](#1x-lab)

* [L2: Abstractions, Structs, and the Stack](#l2-abstractions-structs-and-the-stack)
    * [2.1 Abstraction II: Functions](#21-abstraction-ii-functions)
        * [2.1.1 Abstraction of Behavior: Functions](#211-abstraction-of-behavior-functions)
        * [2.1.2 Abstraction of Data: Structs](#212-abstraction-of-data-structs)
    * [2.2 The Stack and Block Scoping](#22-the-stack-and-block-scoping)
        * [2.2.1 Stack Frames](#221-stack-frames)
        * [2.2.2 Local variables](#222-local-variables)
    * [2.X Lab](#2x-lab)

* [L3: Fixed Size arrays and Recursion](#l3-fixed-size-arrays-and-recursion)
    * [3.1 Arrays](#31-arrays)
        * [3.1.1 Array Declaration](#311-array-declaration)
        * [3.1.2 Initializing elements](#312-initializing-elements)
        * [3.1.3 Accessing an Array (writing)](#313-accessing-an-array-writing)
        * [3.1.4 Copying Semantics](#314-copying-semantics)
        * [3.1.5 Arrays as arguments to functions](#315-arrays-as-arguments-to-functions)
        * [3.1.6 Length of arrays](#316-length-of-arrays)
        * [Setting Values inside Functions](#setting-values-inside-functions)
        * [Returning from functions](#returning-from-functions)
    * [3.2 Arrays and Structs](#32-arrays-and-structs)
        * [Zeroing out](#zeroing-out)
        * [UB](#ub)
        * [Variable-length arrays](#variable-length-arrays)
    * [3.3 Multidimensional Arrays](#33-multidimensional-arrays)
        * [3.3.1 Array of arrays](#331-array-of-arrays)
    * [3.4 Recursion](#34-recursion)
        * [3.4.1 Why Recursion](#341-why-recursion)
        * [3.4.2 Features of recursion](#342-features-of-recursion)
        * [3.4.3 Example: Printing an array in reverse](#343-example-printing-an-array-in-reverse)
        * [Example: Reverse an array](#example-reverse-an-array)
        * [Example: Sort an array](#example-sort-an-array)
    * [3.X Lab](#3x-lab)

</details>

### Admin matters:

**Instructors**:
- Dr. Eldon Chung
- Dr. Sriram Sami

**Schedule**:
| Activity | Time | Venue |
| -------- | ---- | ----- |
| Lecture | Monday 4pm-6pm | I3-LT38 |
| Tutorial | Wednesday 9am-10am | COM1-0120|
| Lab | Thursday 4pm-6pm | COM1-0120 |

**Exams**:
| Activity | Date | Time |
|--------- | ---- | ---- |
| Practical Exam | Tue, 15 Sep | 6pm-9pm |
| Midterm | Mon, 5 Oct | 4pm-6pm |
| Practical Exam | Tue, 13 Oct | 6pm-9pm |
| Practical Exam | Tue, 10 Nov | 6pm-9pm |
| **Final** | Wed, 25 Nov | 9am-11am |

**More info**:
[CS1010 website](https://cs1010.org)

# L0: Introduction

## 0.0 Programming

*Program*
: is a set of instructions that a computer runs.

*Programming*
: is writing code that is used to create a program.

More specifically,
1. The **CPU** (Central Processing Unit) reads information from the computer memory.
2. The CPU then writes information to the *Program Code*. The program code that we make is stored in the memory.
3. The Program stores data (Program data) for intermediate steps. These are also stored in memory.
\\
- We write in a higher-level programming language like C to create instructions that the CPU has to execute. A **compiler** (e.g. `clang` or `gcc`) takes the C code and produces assembly code.
- We use high-level language and compilers so that our code is *portable*; we leave lower level details to be handled by the compiler.
- We also leave hardware level optimisations to be handled by compilers.

**C**
: is a *compiled* programming language.

*Compiler*
: has to take C code written to produce assembly instructions that the CPU will execute.

| Pros | Cons |
| ---- | ---- |
| lots of control: imperative, low level | More work required by programmer |
| Simple language | Many footguns |
| little to no overhead | |

Nevertheless, C is:
- Low-level enough for hardware (firmware)
- Widely supported across embedded systems
- Pervasive in system code
- Good starter language.

## 0.1 Basic Program

Anatomy:
```c
#include <stdio.h>
int main(void) {
    printf("Hello world!\n");
    return 0;
}
```
1. `#include <stdio.h>` makes the C "standard input/output" header file available to this program.
2. `int main(void) {` declares the main function, and code **starts** executing from within `main`. The `void` means that the function does not take any input arguments. The opening brace `{` means the start of the code within `main`.
3. `    printf("Hello world!\n");` Creates a string `"Hello world!"` and a new line character `\n` and  passes the argument to `printf`, which is sent to the standard output of the program
4. Semicolon `;`  indicates the end of the statement.
5. Closing brace `}` ends the code within `main`. 

**Procedure**:
1. Create file with extension .c, (*e.g.*  `hello.c`)
2. Write C code inside.
3. Compile C code to an executable program\\
```bash
clang -o hello hello.c
```
4. Run if no errors.
```bash
./hello
```


## 0.2 Variables and data storage

### 0.2.1 Variables

Variables:
| **Type name(s)** | **Min value** | **Max value** | **Size (bytes)** |
| ------ | ------- | -------- | ------ |
| `char` | -128 | +127 | 1 (8 bits) |
| `unsigned char` | 0 | +255 | 1 (8 bits) |
| `int` | -32768 (-$2^{15}$) | +32767 ($2^{15}-1$) | 2 |
| `unsigned int` | 0 | +65535 ($2^{16}-1$) | 2 |
| `long` | -2147483648 ($2^{31}$) | +2147483647 ($2^{31}-1$) | 4 |
| `unsigned long` | 0 | +4294967295 ($2^{32}-1$) | 4 |
| `unsigned long long` | 0 | $2^{64}-1$ | 8 |
| `float` | 6-7 d.p. | 6-7 d.p. | 4 |
| `double` | 15-17 d.p. | 15-17 d.p.  | 8 |

*When to use which type*
- `char` for ASCII characters
- `int` for default integral types
- `unsigned int` if integer > 0
- `float` if you want to save memory and use decimals.
- `double` if your values might be more precise decimal. Use double and instead of float, unless with good reason.

*Initialization*
You can also initialize a variable without declaring its value.

```c
int a;
int b;
a = 372;
b = a - 200;
``` 

**Overflow**
If you have an `unsigned int` number at 255, and you increment it, you'll get 256 in return. As expected. If you have an `unsigned char` number at 255, and you increment it, you'll get 0 in return. It resets starting from the initial possible value.

If you have a `unsigned char` number at 255 and you add 10 to it, you'll get the number 9:

```c
#include <stdio.h>

int main(void) {
    unsigned char j = 255;
    j = j + 10;
    printf("%u", j); /* 9 */
}
```
If you don't have a signed value, the behavior is undefined. It will basically give you a huge number which can vary, like in this case:

```c
#include <stdio.h>

int main(void) {
    char j = 127;
    j = j + 10;
    printf("%u", j); /* 4294967177 */
}
```
In other words, C does not protect you from going over the limits of a type. You need to take care of this yourself. However, if you initialize a variable with a wrong value, you will likely receive a warning:

```c
#include <stdio.h>

int main(void) {
    char j = 1000;
    char i;
    i = 9999;
    // This will give warning.
}
```

However, incrementing the number will not give a warning and overflow.
```c
#include <stdio.h>

int main(void) {
    char j = 0;
    j += 1000;
}
```

**ASCII table:**
| Dec | Symbol | Dec | Symbol | Dec | Symbol | Dec | Symbol | Dec | Symbol |
|----:|:------:|----:|:------:|----:|:------:|----:|:------:|----:|:------:|
| 48 | 0 | 63 | ? | 78 | N | 93 | `]` | 108 | l |
| 49 | 1 | 64 | @ | 79 | O | 94 | ^ | 109 | m |
| 50 | 2 | 65 | A | 80 | P | 95 | _ | 110 | n |
| 51 | 3 | 66 | B | 81 | Q | 96 | ` | 111 | o |
| 52 | 4 | 67 | C | 82 | R | 97 | a | 112 | p |
| 53 | 5 | 68 | D | 83 | S | 98 | b | 113 | q |
| 54 | 6 | 69 | E | 84 | T | 99 | c | 114 | r |
| 55 | 7 | 70 | F | 85 | U | 100 | d | 115 | s |
| 56 | 8 | 71 | G | 86 | V | 101 | e | 116 | t |
| 57 | 9 | 72 | H | 87 | W | 102 | f | 117 | u |
| 58 | : | 73 | I | 88 | X | 103 | g | 118 | v |
| 59 | ; | 74 | J | 89 | Y | 104 | h | 119 | w |
| 60 | < | 75 | K | 90 | Z | 105 | i | 120 | x |
| 61 | = | 76 | L | 91 | `[` | 106 | j | 121 | y |
| 62 | > | 77 | M | 92 | \ | 107 | k | 122 | z |

It is possible to find the size of a variable.

**sizeof()**
```c
#include <stdio.h>
int main(void) {
    int myInt;
    float myFloat;
    double myDouble;
    char myChar;
    printf("%d\n", sizeof(myInt));
    printf("%d\n", sizeof(myFloat));
    printf("%d\n", sizeof(myDouble));
    printf("%d\n", sizeof(myChar));
    return 0;
}
```

output:
```terminal
4
4
8
1
```


### 0.2.2 Format Specifiers

*Format specifiers*
| **Specifier** | **Output** | **Example** |
| ------ | ------- | ------ |
| `d` or `i` | Signed decimal integer | `392` |
| `u` | Unsigned decimal integer | `7235` |
| `o` | Unsigned octal | `610` |
| `x` | Unsigned hexadecimal integer | `7fa` |
| `X` | Unsigned hexadecimal integer (uppercase) | `7FA` |
| `f` | Decimal floating point, lowercase | `392.65` |
| `F` | Decimal floating point, uppercase | `392.65` |
| `e` | Scientific notation (mantissa/exponent), lowercase | `3.9265e+2` |
| `E` | Scientific notation (mantissa/exponent), uppercase | `3.9265E+2` |
| `g` | Shortest representation: `%e` or `%f` | `392.65` |
| `G` | Shortest representation: `%E` or `%F` | `392.65` |
| `a` | Hexadecimal floating point, lowercase | `-0xc.90fep-2` |
| `A` | Hexadecimal floating point, uppercase | `-0XC.90FEP-2` |
| `c` | Character | `a` |
| `s` | String of characters | `sample` |
| `p` | Pointer address | `b8000000` |
| `n` | Nothing printed. Argument must be a pointer to a signed `int`; the number of characters written so far is stored there. | — |
| `%` | A literal `%` character | `%` |


Below is an example:
```c
#include <stdio.h>

int main(void) {
    int sixtyseven = 67;
    double pi = 3.1415926535897;
    char ahh = 'a';
    char pain[] = "what?"; //adding [] to the end of the variable will make it a string instead of a char
    printf("Integer: %d\n", sixtyseven);
    printf("2dp Float: %.2f\n", pi);
    printf("6dp Float: %.6f\n", pi);
    printf("Char: %c\n", ahh);
    printf("String: %s\n", pain);

    return 0;
}
```

**Integer Truncation**
When you output the value of `double` with `%d`, you will get the *floor* of the value, truncating the decimal point and leaving the integer part.
```c
int x = 5;
x = x + 0.1; // Behind the scenes: (int)((double)5.0 + 0.1)
printf("%d", x); 
```

## 0.3 Arithmetic and Assignment Operators

### 0.3.1 Arithmetic Operators
**Arithmetic operators** let us do math:

| Operator | Meaning            | Example |
| -------- | ------------------ | ------- |
| `=`      | Assignment         | `x=1`   |
| `+`      | Addition           | `x + y` |
| `-`      | Subtraction        | `x - y` |
| `*`      | Multiplication     | `x * y` |
| `/`      | Division           | `x / y` |
| `%`      | Modulo (remainder) | `x % y` |

### 0.3.2 Unary operators
**Unary operators** only take one operand:
| Operator | Name | Example |
| -------- | ---- | ------- |
| `+` | Unary plus  | `+a` |
| `-` | Unary minus | `-a` |
| `++` | Increment | `a++` or `++a` |
| `--` | Decrement | `a--` or `--a` |

Example:
```c
int a = 2;
int b;
b = a++ /* b is 2, a is 3 */
b = ++a /* b is 4, a is 4 */
b = a-- /* b is 4, a is 3 */
b = --a /* b is 2, a is 2 */
```
### 0.3.3 Comparison Operators
**Comparison Operators** 
| Operator | Name                    | Example  |
| :------: | ----------------------- | -------- |
|   `==`   | Equal operator          | `a == b` |
|   `!=`   | Not equal operator      | `a != b` |
|    `>`   | Bigger than             | `a > b`  |
|    `<`   | Less than               | `a < b`  |
|   `>=`   | Bigger than or equal to | `a >= b` |
|   `<=`   | Less than or equal to   | `a <= b` |



### 0.3.4 Logic Operators
**Logical operators:**  work with boolean values.
| Operator | Name | example |
|---|---|---|
| `!` | NOT | `!a` |
| `&` |AND |`a && b` |
| `\|` | OR | `a \|\| b` |

### 0.3.5 Assignment Operators
**Assignment Operators** perform arithmetic transformation and and assignment   
| Operator | Name                      | Example  |
| :------: | ------------------------- | -------- |
|   `+=`   | Addition assignment       | `a += b` |
|   `-=`   | Subtraction assignment    | `a -= b` |
|   `*=`   | Multiplication assignment | `a *= b` |
|   `/=`   | Division assignment       | `a /= b` |
|   `%=`   | Modulo assignment         | `a %= b` |

### 0.3.6 Integer Division

If `x` and `y` are **integer-like types**, `/` **truncates the fractional part**.

```c
printf("%d\n", 50 / 20);  // 2
printf("%d\n", 50 % 20);  // 10
```

* `50 / 20` → `2`, not `2.5`
* `50 % 20` → `10` (remainder)
* `%` only works on **integral types**; not `float`/`double`.

### 0.3.7 Division with `double`

If you want to preserve decimal values, make sure **at least one operand is `double`/`float`**:

```c
int x = 50;

x / 20       // 2
x / 20.0     // 2.5
50.0 / 20.0  // 2.5
(double)x / 20  // 2.5
```

You can explicitly convert a value using a **cast**:

```c
(double)x
```

### 0.3.8 Operator Precedence

* `*`, `/`, `%` have **higher priority** than `+` and `-`
* `()` has the **highest priority**
* Similar to the normal order of operations in mathematics.

```c
x + 3 / x * (3 + x)
```

is evaluated according to these precedence rules.

---

> **Important:** `=` means **assignment**, not mathematical equality.

```c
int x = 5;
x = x + 2;  // x is now 7
x += 2;     // x is now 9
```

Assignment **changes the state of the program** by changing the value stored in a variable.


## 0.4 Ternary Operators

The **ternary operator** provides a compact way to choose between two expressions based on a condition.

```c
<expression1> ? <expression2> : <expression3>;
```

In English:

> If `<expression1>` is true, evaluate `<expression2>`; otherwise, evaluate `<expression3>`.

Example:

```c
double product_cost = 888;

double discount_amt = (product_cost >= 670) ? 2 : 0;
```

Since `product_cost` is `888`:

```text
888 >= 670 → true
```

Therefore:

```text
discount_amt = 2
```

If `product_cost` were less than `670`:

```text
discount_amt = 0
```

### Common condition tests

| Operator | Meaning               |
| -------- | --------------------- |
| `>`      | More than             |
| `>=`     | More than or equal to |
| `<`      | Less than             |
| `<=`     | Less than or equal to |
| `==`     | Equal to              |
| `!=`     | Not equal to          |

Another example:

```c
(product_cost >= 670)
    ? printf("You've reached min-spend")
    : printf("Spend another %f cents\n", 670 - product_cost);
```

The ternary operator is useful for **simple conditions** where there are two possible outcomes.

## 0.5 Undefined Behaviour

**Undefined Behaviour (UB)** is a major recurring aspect of C.

C is defined by a document called the **C Standard**. CS1010 uses the **C23 standard**.

The standard specifies what should happen for valid C code. However, for some erroneous code, the standard **imposes no requirements**.

If a program contains **undefined behaviour**:

> The program is allowed to do anything.

It might:

* produce an unexpected result
* crash
* appear to work
* behave differently on another compiler/system
* do something else entirely

**There are no guarantees.**

### Example: Division by zero

```c
#include <stdio.h>

int main() {
    printf("%d\n", 5);
    printf("%d\n", 1 / 0);
    return 0;
}
```

The expression:

```c
1 / 0
```

has **undefined behaviour**.

Do **not** assume that it will always produce a particular result.

### Integer Overflow

Overflow occurs when a value exceeds the range that its type can represent.

Assuming `int` is 4 bytes (32 bits):

**Unsigned integer overflow is well-defined:**

```c
unsigned int c = 4294967295;
c = c + 1;
```

The value **wraps around**:

```text
c = 0
```

**Signed integer overflow is undefined behaviour:**

```c
int c = 2147483647;
c = c + 1;  // Undefined Behaviour!
```

So:

| Situation                 | Behaviour                  |
| ------------------------- | -------------------------- |
| Unsigned integer overflow | Well-defined; wraps around |
| Signed integer overflow   | **Undefined Behaviour**    |

### Key takeaway

**UB = the C Standard gives no requirements for what happens.**

Therefore, **never rely on what seems to happen when testing UB**. A program may behave differently depending on the compiler, optimisation, machine, or other circumstances.

> **UB is an unavoidable part of C**, so learning to recognise and avoid it is important.

**Compiler Warnings**

The compiler can warn you about **some** problematic cases.

```text
Listen to what your compiler says!
```

Compiler warnings are useful for catching potential problems before they become bugs.

## 0.X Lab

**Goal:** Practice working with variables, format specifiers, and the ternary operator.

**Exercise 1 — Temperature conversion**

Write a program that stores a temperature in Celsius as a `double`, converts it to Fahrenheit, and prints both values to 2 decimal places.

```c
#include <stdio.h>

int main(void) {
    double celsius = 30.0;
    double fahrenheit = celsius * 9.0 / 5.0 + 32;
    printf("%.2f C = %.2f F\n", celsius, fahrenheit);
    return 0;
}
```

**Exercise 2 — Even or odd, with a ternary**

Read an `int` and use the ternary operator (not `if`) to print whether it is even or odd.

```c
#include <stdio.h>

int main(void) {
    int n = 7;
    printf("%s\n", (n % 2 == 0) ? "even" : "odd");
    return 0;
}
```

**Things to watch out for**
- Integer division silently truncates — cast to `double` if you need a fractional result (see [0.3.7](#037-division-with-double)).
- `%` only works on integer types.
- Always double check your format specifier matches the variable's type (e.g. `%f` for `double`/`float`, `%d` for `int`) — mismatching them is undefined behaviour (see [0.5](#05-undefined-behaviour)).

# L1: Conditionals and Functions

## 1.1 Abstraction I: Functions

*Function*
: is a named, reusable block of code that performs a specific task. It takes zero or more **arguments** as input, and can **return** a single value as output.

**Why functions?**
- **Abstraction** — the caller only needs to know *what* a function does (its interface), not *how* it does it (its implementation).
- **Reuse** — write the logic once, call it many times.
- **Readability** — breaking a program into small, well-named functions makes it easier to follow.

**Anatomy of a function**

```c
int add(int a, int b) {
    int sum = a + b;
    return sum;
}
```
- `int` (leftmost) is the **return type** — the type of value the function sends back.
- `add` is the function's **name**.
- `(int a, int b)` are the **parameters** — the inputs the function expects, along with their types.
- `return sum;` sends the value of `sum` back to whoever called the function. A function with return type `void` does not return a value, and can use a bare `return;` (or nothing) to end early.

**Calling a function**
```c
int result = add(3, 4); // result is 7
```

**Function prototypes**

If a function is defined *after* `main`, or in another file, the compiler needs to know its signature before it's used. A **prototype** declares the signature without the body:
```c
int add(int a, int b); // prototype

int main(void) {
    int result = add(3, 4);
    return 0;
}

int add(int a, int b) { // definition
    return a + b;
}
```

## 1.2 Conditional Statements
### 1.2.1 If/else constructs

The `if` statement runs a block of code only when a condition is true.

```c
if (condition) {
    // runs when condition is true
}
```

Add an `else` to handle the opposite case:
```c
if (condition) {
    // condition is true
} else {
    // condition is false
}
```

Chain multiple conditions with `else if`:
```c
if (score >= 90) {
    printf("A\n");
} else if (score >= 75) {
    printf("B\n");
} else if (score >= 50) {
    printf("C\n");
} else {
    printf("F\n");
}
```
Only the **first** branch whose condition is true runs; the rest are skipped.

**Always use braces**

As seen in the L2 lab below, omitting `{ }` means only the *single statement* immediately after the `if`/`else` belongs to it — everything after that runs unconditionally regardless of the condition. Always wrap the body in `{ }`, even for one-line bodies, to avoid this class of bug.

### 1.2.2 Comparison and logical operators

Recall the comparison operators (`==`, `!=`, `<`, `>`, `<=`, `>=`) and logical operators (`&&`, `||`, `!`) from [0.3](#03-arithmetic-and-assignment-operators). Inside an `if`, these are combined to build more complex conditions.

**Truth tables**

| `a` | `b` | `a && b` | `a \|\| b` |
| --- | --- | -------- | -------- |
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 |

| `a` | `!a` |
| --- | ---- |
| 0 | 1 |
| 1 | 0 |

**Short-circuit evaluation**

`&&` and `||` evaluate left to right and stop early once the result is already decided:
- `a && b` — if `a` is false, `b` is **never evaluated** (the whole expression is already false).
- `a || b` — if `a` is true, `b` is **never evaluated** (the whole expression is already true).

This matters when the right-hand side has side effects (e.g. a function call that prints something), as seen in the `foo() && bar()` example in the L2 lab below.

### 1.2.3 Boolean operators

C did not have a built-in boolean type until relatively recently. `<stdbool.h>` provides one:

```c
#include <stdbool.h>

bool is_valid = true;
```

Under the hood:
- `bool` is really a small integer type; `true` is `1` and `false` is `0`.
- Any non-zero value is treated as "true" in a condition; only `0` is "false".

```c
int x = 5;
if (x) {        // true, since x != 0
    printf("x is truthy\n");
}
```

**Returning a `bool` from a function**

```c
#include <stdbool.h>

bool is_even(int n) {
    return n % 2 == 0;
}
```
This is the pattern used by `foo()` and `bar()` in the L2 lab below — functions that return `bool` and are combined with `&&`/`||` inside an `if`.

## 1.X Lab

**Goal:** Practice writing your own functions that use conditionals.

**Exercise — Grade classifier**

Write a function `char grade(int score)` that returns `'A'`, `'B'`, `'C'`, or `'F'` based on the boundaries used in [1.2.1](#121-ifelse-constructs), then call it from `main` and print the result.

```c
#include <stdio.h>

char grade(int score) {
    if (score >= 90) {
        return 'A';
    } else if (score >= 75) {
        return 'B';
    } else if (score >= 50) {
        return 'C';
    } else {
        return 'F';
    }
}

int main(void) {
    int score = 82;
    printf("Grade: %c\n", grade(score));
    return 0;
}
```

**Stretch goal**

Write `bool is_leap_year(int year)` using the rule: divisible by 4, except centuries, unless also divisible by 400. Combine `&&`, `||`, and `!` from [1.2.2](#122-comparison-and-logical-operators).

# L2: Abstractions, Structs, and the Stack
##  2.1 Abstraction II: Functions 
### 2.1.1 Abstraction of Behavior: Functions

Section [1.1](#11-abstraction-i-functions) introduced functions as reusable blocks of code. Here we look at *why* wrapping behaviour in a function is a form of **abstraction**.

When we call a function, we only need to know:
1. Its **name**
2. Its **parameters** (types and meaning)
3. Its **return type**

We don't need to know *how* it's implemented internally — that's hidden inside the function body. This is exactly what happens with `read_point()` and `print_movement()` in the lab below: `main` doesn't need to know how a point is read or how movement is computed, only that these functions exist and what they do.

**Pass-by-value**

In C, arguments are passed **by value** — the function receives a *copy* of the argument. Modifying a parameter inside a function does not affect the caller's variable.
```c
void increment(int x) {
    x = x + 1; // only changes the local copy
}

int main(void) {
    int n = 5;
    increment(n);
    printf("%d\n", n); // still 5
}
```

### 2.1.2 Abstraction of Data: Structs

Just as functions abstract *behaviour*, **structs** abstract *data* — they let us group related variables into a single named type.

```c
typedef struct {
    int x;
    int y;
} Point;
```
- `struct { ... }` defines a new structure with the listed fields (**members**).
- `typedef ... Point;` gives the struct the alias `Point`, so we can write `Point p;` instead of `struct { ... } p;` every time.

**Creating and accessing a struct**
```c
Point p;
p.x = 3;
p.y = 4;
printf("(%d, %d)\n", p.x, p.y); // (3, 4)
```
The `.` (dot) operator accesses a member of a struct.

**Why this is abstraction**

Without a struct, a point would be two separate, unrelated `int` variables (`px`, `py`), and a function relating two points would need four separate parameters. With `Point`, related data travels together as one value — as seen in the lab below, where `print_movement(Point start, Point end)` takes just two arguments instead of four.

## 2.2 The Stack and Block Scoping
### 2.2.1 Stack Frames

Every time a function is called, the program sets aside a small block of memory called a **stack frame** to hold that call's local variables, parameters, and return address.

- When a function is **called**, a new frame is **pushed** onto the **call stack**.
- When the function **returns**, its frame is **popped** off the stack, and its memory is reclaimed.
- Each call gets its **own** frame — calling the same function twice (e.g. `read_point()` for `p` then for `q` in the lab below) creates two separate frames, each with its own copy of `pt`.

```text
call main()
  -> call read_point()    [frame for read_point pushed]
  <- return                [frame for read_point popped]
  -> call read_point()    [a *new* frame pushed]
  <- return                [popped again]
  -> call print_movement() [frame pushed]
  <- return                [popped]
```
This is also why a function cannot "see" another function's local variables — they live in different frames.

### 2.2.2 Local variables

A **local variable** is declared inside a function or block, and only exists — is only *in scope* — within that block.

```c
void foo(void) {
    int a = 1; // local to foo
}

void bar(void) {
    int a = 2; // a different `a`, local to bar
}
```
`foo`'s `a` and `bar`'s `a` are unrelated; each lives in its own stack frame.

**Block scoping**

Any `{ }` introduces a new scope, not just function bodies — including `if`, `else`, and loop bodies:
```c
int main(void) {
    int x = 10;
    if (x > 5) {
        int y = 20;     // y only exists inside this block
        printf("%d\n", y);
    }
    // y is not visible here — out of scope
    return 0;
}
```

**Lifetime vs. scope**
- **Scope** — where in the code a variable's name is visible.
- **Lifetime** — how long the variable's memory actually exists (tied to its stack frame, from when the block is entered to when it's exited).

## 2.X Lab

**More If-Else, Abstraction, Structs**

Part 1a:

Does the code below compile? What is its output?
```c
#include <stdbool.h>
#include <stdio.h>
 
bool foo(){
	printf("foo called returning true\n");
	return true;
}
 
bool bar(){
	printf("bar called returning false\n");
	return false;
}
 
int main(){
	if(foo() && bar()){
		printf("line A reached\n");
	}
 
	printf("BOOP\n");
 
	if(foo() || bar()){
		printf("line B reached\n");
	}
}
```

Output:
**Only one line output **
- If you omit the curly braces `{    }` in your if statement, only the line **below** the `if` statement is used as its output.
- 


Consider the following code:
```C
#include "input.h"
#include <stdbool.h>
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Point;

int main() {
    Point p;
    p.x = read_int();
    p.y = read_int();

    Point q;
    q.x = read_int();
    q.y = read_int();

    int dx = q.x - p.x;
    int dy = q.y - p.y;

    bool moving_right = dx > 0;
    bool moving_up = dy > 0;
    bool on_same_x = dx == 0;
    bool on_same_y = dy == 0;

    if (on_same_x && on_same_y) {
        printf("same point\n");
    } else if (on_same_x) {
        printf("vertical movement\n");
    } else if (on_same_y) {
        printf("horizontal movement\n");
    } else if (moving_right && moving_up) {
        printf("northeast\n");
    } else if (!moving_right && moving_up) {
        printf("northwest\n");
    } else if (moving_right && !moving_up) {
        printf("southeast\n");
    } else {
        printf("southwest\n");
    }
    return 0;
}
```

We can simplify this to:

```c
#include "input.h"
#include <stdbool.h>
#include <stdio.h>

typedef struct {
    int x;
    int y;
} Point;

Point read_point() {
    Point pt;
    pt.x = read_int();
    pt.y = read_int();
    return pt;
}

void print_movement(Point start, Point end) {
    int dx = end.x - start.x;
    int dy = end.y - start.y;

    bool moving_right = dx > 0;
    bool moving_up = dy > 0;
    bool on_same_x = dx == 0;
    bool on_same_y = dy == 0;

    if (on_same_x && on_same_y) {
        printf("same point\n");
    } else if (on_same_x) {
        printf("vertical movement\n");
    } else if (on_same_y) {
        printf("horizontal movement\n");
    } else if (moving_right && moving_up) {
        printf("northeast\n");
    } else if (!moving_right && moving_up) {
        printf("northwest\n");
    } else if (moving_right && !moving_up) {
        printf("southeast\n");
    } else {
        printf("southwest\n");
    }
}

int main() {
    Point p = read_point();
    Point q = read_point();
    print_movement(p, q);
    return 0;
}
```

# L3: Fixed Size arrays and Recursion
## 3.1 Arrays
### 3.1.1 Array Declaration

Let's say we want to declare an array that stores 5 elements of type `double` that we want to call "costs".

An **array** is declared as such:
`<type> <array name>[<no. of elements>]`

```c
double costs[5];
```

> **Important:** Arrays have a fixed type. You cannot add multiple different types to an array unlike Python.

Arrays are stored on the stack. 
```stack
main

costs = {?,?,?,?,?}
```
An array will have all of its elements stored contiguously to each other in memory. * This has implications for both performance and security in the far future.

```c
double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
        // initializes the array with 5 values
```
It is stored in the stack as such:
```
stack:
|8.88|10.22|9.88|22.22|44.44|
```
### 3.1.2 Initializing elements
However, what if we initialize only 3 elements out of 5?

```c
double costs[5]= {8.88,10.22,9.88};
// the remaining elements will be initialized to 0.0 by default.


double zeroarray[5]={0};
//^^this is a very good way to initialize an entire array to 0!
```

What if we initialize more than 5 elements?
```c
double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44, 1.0};
```

If we have more values than the specified size, what happens is up to the compiler (technically not undefined behavior) [we don’t recommend doing this, there’s no good reason to at this stage]


What if we initialize it over 2 lines?
```c
double costs[5];
costs = {8.88, 10.22, 9.88, 22.22, 44.44, 1.0};
```
> This does **NOT** work and throws a `compile error`. Unlike scalar variables, arrays cannot be assigned new values as a whole.


### 3.1.3 Accessing an Array (writing)
We use the index.
```c
double costs[5];

costs[0] = 8.88;
// | 8.88 | ? | ? | ? | ? |

costs[4] = 44.44;
// | 8.88 | ? | ? | ? | 44.44 |
```

### 3.1.4 Copying Semantics
```c
int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    double costs_2[] = costs; // error!
}
```

> This does **NOT** work and will throw a *compile error*! `error: array initializer must be an initializer list.`

Arrays (unlike numerical types and structs) as a whole are **not copyable** via assignment operators.

### 3.1.5 Arrays as arguments to functions
```c
#include <stdio.h>
#include <stddef.h>

void print_doublearr_index(double arr[], size_t index) {
    printf("%f\n", arr[index]);
}

int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    print_doublearr_index(costs, 3);
}
```

`size_t`: unsigned type (typically `unsigned long`)
- Guaranteed to be large enough to index any array
- Intent is clear: use by default for array indices, unless we need negative values
- `size_t` is defined in `<stddef.h>`

Array indices can technically be any integral type (`char`, `int`, `long` ...)

### 3.1.6 Length of arrays
```c
void print_last_element (double arr[]) {
    printf("%f\n", arr[?])
}

int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    print_last_element(costs);
}
```
In **C**, we do **NOT** have `length/len` operators to measure the length of an array.

Instead, we use `size_t` for now:
```c
void print_last_element(double arr[], size_t length) {
    printf("%f\n", arr[length - 1]);
}

int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    print_last_element(costs, 5);
}
```

### Setting Values inside Functions

```c
int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    set_doublearr_index(costs, 3, 5.5);
    printf("%f\n", costs[3]);
}
void set_doublearr_index(double arr[], size_t index, double val) {
    arr[index] = val;
}
    //output is... 5.5.
```

This sets the index 3 (the 4th) element of costs to 5.5. But how is that possible? This is because arrays are pointers.
[](#)

### Returning from functions
For now, do not return arrays declared within functions.
```c
// DONT DO THIS
??? foo() {
    double costs[5] ={8.88, 10.22, 9.88, 22.22, 44.44, 1.0};
    return costs;
} // will return UB
```

## 3.2 Arrays and Structs
### Zeroing out

```c
#include <stdio.h>

typedef struct Position {
    int x;
    int y;
} Position;

int main(void){
    Position positions[2] = {0};
    printf("%d %d\n", positions[0].x, positions[0].y);
} // This will zero out all members of all structs.
```

### UB
```c
int main(void) {
    double costs[1] = {8.88};
    printf("%f\n", costs[1]);
}

// UB [1] 


int main(void) {
    double costs[1];
    printf("%f\n", costs[-1]);
}

// UB [2]

??? foo() {
    double costs[1] = {8.88};
    return costs;
}

// UB [3]

int main() {
    double costs[1];
    printf("%f\n", costs[0]);
}
```

### Variable-length arrays

Can we declare the size of an array as a variable? Yes.
```c
double costs[var];
```

> However, there are much better ways to do this (discussed later). We do not allow VLAs because of underlying issues. As a matter of fact, VLA was removed from Linux operating system.

## 3.3 Multidimensional Arrays
### 3.3.1 Array of arrays
```c
int main(void) {
    int a[2][3] = {{0,1,2},{3,4,5}};
    printf("%d\n", a[1][0]);
}
```

Then a is stored as:
$$a =
\left[\begin{matrix}
    0 & 1 & 2 \\ 3 & 4 & 5
\end{matrix}\right]
$$

We are storing an array of arrays.

Example: tic-tac-toe
```c
int grid[3][3] = {{1,2,3},{4,5,6},{7,8,9}};
```
$$\text{grid} =
\left[\begin{matrix}
    1 & 2 &3 \\ 4 & 5 & 6 \\ 7&8&9
\end{matrix}\right]$$

Arrays can have more dimensions!

> Only the first dimension size can be omitted.

## 3.4 Recursion
### 3.4.1 Why Recursion
You **cannot call yourself a programmer if you don't know how to recurse**.  You will be locking yourself away from future concepts if you don't learn this. This includes:
- Binary search trees
- Fast/Efficient sorting algorithms
- A lot of efficient algorithms. The fast Fourier transform (FFT) is an example

### 3.4.2 Features of recursion

- **Base Case:**
    - The simplest possible case that we have to solve manually.

- **Recursive Case:**
    - In this case we usually have to "steer" the general case into the smaller case somehow. 
    - We will rely on Cheems to solve the smaller version of the problem for us.
    - We will use whatever Cheems gives us + a little bit more work to solve the problems in general.


```c
<return_type> foo(<param(s) here>){
    if(<base case>){
    return; // or return value;
}

// handle recursive case here
// any computation before recursive call(s)

foo(<with smaller case>);
    // any computation after recursive call(s)
}
```

### 3.4.3 Example: Printing an array in reverse

Logic:
1. The base case is when the length of the array is 0, so we do nothing.
2. We have an entire array of $n$ elements.
3. 

- The entire array of $n$ elements
    - The last element will be our base case.
    - Cheems will handle the rest with: `print_arr_reverse(arr, len-1)`
-  We should do something only with the last element. We print the last element before Cheems.

```c
void print_arr_reverse(int arr[], size_t len){
    if (len == 0) {
        return; // array has nothing, we do nothing.
    }

    printf("%d\n", arr[len-1]);

    print_arr_reverse(arr, len-1); // cheems!
}
```

### Example: Reverse an array
Input: An array of length `len`.
Output: Reverse the elements of `arr`.

We need a helper function here:
The function will need: 
- take in an array
- Swap the first and last elements

```c
void reverse_arr_helper(int arr[], size_t start, size_t end) {
    if (start >= end) {
        return;
    }
    reverse_arr_helper(arr, start+1, end-1);
    int temp = arr[start];
    arr[start] = arr[end];
    arr[end] = temp;
}

void reverse_arr(int arr[], size_t len) {
    if (len==0) {return;}
    reverse_arr_helper(arr,0,len-1);
}
```

### Example: Sort an array
Let's say Cheems has already sorted the first $n-1$ elements for us. What should we do with the last element?
> We figure out where to put it.

```c
void shift_left(int arr[], size_t len, size_t count) {
    ...
}

void count_larger_than(int arr[], size_t len, size_t val) {
    ...
}

void sort_arr(int arr[], size_t len) {
    if(len==0){
        return;
    }
    size_t count = count_larger_than(arr, len-1, arr[len-1]);
    shift_left(arr, len, count);
}

```

# 3.X Lab
* When declaring `arrays[][]`, you need to at least declare the no. of columns `[][cols]`.

* `void` will not affect the variable inside `main` without `return`.
* However, `void` calls on the array directly and can redefine the array elements.


# L4: Loops

## 4.1 `while` Loops and `for` Loops

### Why loops?

Some problems can be solved using recursion, but recursion can use a lot of stack space. Consider printing every element of an array:

```c
void print_arr_from(double arr[], size_t length, size_t i) {
    if (i == length) {
        return;
    }
    printf("%f\n", arr[i]);
    print_arr_from(arr, length, i + 1);
}

void print_arr(double arr[], size_t length) {
    print_arr_from(arr, length, 0);
}
```

Each recursive call uses a stack frame and waits for the next call to finish. Printing an array of length \(n\) creates roughly \(n\) nested calls, so a sufficiently large array can exhaust the stack and cause a **stack overflow**. C does not guarantee tail-call optimization to avoid this.

Loops let us repeat code without making a new function call for every repetition.

### `while` loops

```c
while (expression) {
    // loop body
}
```

The expression is checked first. If it is true, the loop body runs. At the end of the body, execution returns to the condition and checks it again. If the expression is false, the loop body is skipped or the loop ends.

For example, print every element of an array:

```c
void print_arr(double arr[], size_t length) {
    size_t i = 0;

    while (i < length) {
        printf("%f\n", arr[i]);
        i += 1;
    }
}
```

Here, `i` is the **index** (or iterator). It starts at zero, increases after each iteration, and the loop ends when `i < length` becomes false.

If the loop body never changes anything that can make the condition false, the loop may run forever. For example, leaving out `i += 1` would repeatedly print `arr[0]`.

Array indices go from `0` to `length - 1`. Using `i <= length` would eventually access `arr[length]`, which is outside the array and causes undefined behavior.

For reverse iteration with `size_t`, avoid a condition such as `i >= 0`: `size_t` is unsigned, so that condition is always true, even after the value wraps around. One way to print in reverse is:

```c
void print_arr_reverse(double arr[], size_t length) {
    for (size_t i = 0; i < length; i += 1) {
        printf("%f\n", arr[(length - 1) - i]);
    }
}
```

### `for` loops

A `for` loop puts initialization, condition, and iteration in one place:

```c
for (expression1; expression2; expression3) {
    // loop body
}
```

- `expression1` runs once before the loop starts. It often declares and initializes an index.
- `expression2` is the condition. The body runs only when it is true.
- `expression3` runs after each execution of the body. It often updates the index.

The `while` and `for` versions below do the same thing:

```c
size_t i = 0;
while (i < length) {
    printf("%f\n", arr[i]);
    i += 1;
}
```

```c
for (size_t i = 0; i < length; i += 1) {
    printf("%f\n", arr[i]);
}
```

Variables declared in a `for` loop’s initialization are scoped to the loop, so `i` cannot be used after the loop. A variable declared before a `while` loop remains accessible after it.

## 4.2 Loop control with `break`, `continue`, `return`

### `break`

`break` immediately exits the **innermost loop** containing it. Execution continues after that loop.

```c
for (size_t i = 0; i < 5; ++i) {
    printf("%zu\n", i);
    if (i == 1) {
        break;
    }
}
printf("Loop ended!\n");
```

This prints `0`, `1`, and `Loop ended!`. In nested loops, `break` exits only the inner loop.

### `continue`

`continue` skips the rest of the current loop body and moves to the next iteration. In a `for` loop, the iteration expression runs before the condition is checked again.

```c
for (size_t i = 0; i < 5; ++i) {
    if (i == 1) {
        continue;
    }
    printf("%zu\n", i);
}
```

This prints `0`, `2`, `3`, and `4`.

### `return`

`return` immediately exits the **entire function**, including any loops inside it. For example, this function returns as soon as it finds a `1`:

```c
bool has_one_inside_array(int arr[], size_t length) {
    for (size_t i = 0; i < length; ++i) {
        if (arr[i] == 1) {
            return true;
        }
    }
    return false;
}
```

## 4.3 Array recursion

Array elements are commonly processed by iterating over their indices:

```c
for (size_t i = 0; i < length; ++i) {
    // process arr[i]
}
```

This is useful for tasks such as printing every element, initializing an array, and calculating a sum. The index starts at `0`, and the loop condition `i < length` ensures the last index accessed is `length - 1`.

## 4.4 Examples

### Initialize every array element

```c
void init_array(double arr[], size_t length, double val) {
    for (size_t i = 0; i < length; ++i) {
        arr[i] = val;
    }
}
```

`++i`, `i++`, and `i += 1` all increase `i` by one here.

### Nested loops: print a triangle

A loop can be placed inside another loop. The inner loop runs to completion during each outer loop iteration.

```c
void print_triangle(size_t height) {
    for (size_t i = 0; i < height; ++i) {
        for (size_t j = 0; j < i + 1; ++j) {
            printf("X ");
        }
        printf("\n");
    }
}
```

The outer loop controls the row number. The inner loop prints `i + 1` Xs on that row. Each loop’s index is scoped to its own `for` loop.

### A method for planning loops

1. Decide what condition must be true for the loop to continue.
2. If the loop needs an iterator, choose its type and initialize it.
3. Decide how to update the iterator after each iteration.


# L5: Pointers and Strings

## 5.1 Pointers
### memory
Before we talk about pointers, we need to first about memory.
Memory has two Features:
* **address** is the location of where data is stored
* **value** of the memory is the data stored at the location

For example:

```c
int x = 4;
int *p = &x;
```
Then the memory would look like so:
| Address | Value |
| --- | --- |
| '0x1000' | '0x4' |
| '0x1004' | '0x1000' |
| '0x1008' | |
| '0x100C' | |
| '0x1010' | |
| '0x1014' | |
| '0x1018' | |
| '0x101C' | |

### Pointers.
A pointer is a type of variable that points to another value's address.
We define integer `int x = 4`. 
In english, "integer named `x` is set to $4$."
And then we define `int *p = &x`
In english, "integer pointer named `p` is set to the *address* of `x`"
The asterisk `*` stands for pointer, while the ampersand `&` stands for address.

![fig 5.1.1: image of pointer](/assets/pointer.png)

A pointer takes the same number of bytes as the object it points to.

### Why pointers?
We break down functions in C based on the actions they perform. However, they are sometimes out of scope that we want. To get around this, we pass the struct using a pointer so that the pointer to the struct is in scope of the functions we want. This reduces the space by not copying.


## 5.2 Address-of (&) and Dereferencing (*), nullptr, pointers to pointers

### 5.2.1 Printing Addresses

```c
char x ='A';
printf("x is at %p\n,", &x);
```
- `%p` is a format specifier to print an address.
- `&x` is the addres of x.
- However, some addresses may have spillover addresses that stretch over 1 byte.

For multibyte addresses,
```c
int y =1000; // asume that y takes up 2 bytes here
printf("y is at %p\n,", (char *) &y);
```

- To print `&y`, we need to make it refer to a single byte (`&y` the first one).
- The address of x (`&x`) refers to the entire object `x`.

The addresses are printed in this strange-looking form
- (e.g. 0x7ffd7f613f2b)
- 7ffd7f613f2b is a number represented in hexadecimal form (base-16, where the 16 digits are 0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F)
- As a normal base-10 number, this address is 140726740533035
- Addresses aren't guaranteed to be the same across different executions of the program.

Takeaway: you have to use &x for e.g., to get the address of things (you can't just guess or assume what it is)


### 5.2.2 Address (&) and Dereferencing (*)

```c
int *p = &x;
int y = *p; 
```
when an asterisk is used without the type, it becomes a pointer **dereference**.
In english, "integer named `y` is set to *the thing pointed to* by `p`."


```c
int x =1;
int *ptr = &x;
printf("%d\n",*ptr);
// 1
```

`int *ptr = &x`
- type pointer to an integer.
- The unary operator `&` is the *address of* an object.
`*ptr = 1;` - dereferencing a pointer to its address

```c
int main(void) {
    int x = 5;
    int *y = &x;
    printf("%d\n", x);
    *y = 10; //Read this as "go to the address pointed to by y. Then, set the value at that address to 10
    printf("%d\n", x);
}
```

### 5.2.3 nullptr
* `nullptr` is a special value in C23 that is guaranteed not to point to anything valid
* Dereferencing a pointer to nullptr is **undefined behavior**!
* Sometimes, you can check if `ptr == nullptr`

e.g.
```c
int main(void) {
    int *y = nullptr;
    // *y is UB.
}
```

### 5.2.4 Pointer to a pointer
- A pointer variable is stored in memory, and has an address as well, so you can point to it!
- If i dereference `z` twice, I’ll get an `int` back
![pointer squared](assets\pointerpointer.png)

```c
int main(void) {
    int x = 5;
    int *y = &x;
    int **z = &y;
}
```

**Summary:** A pointer is a type of variable that stores an address.

Declaring a pointer to a specific type: `<type> *<ptr_name>;`
Getting the value pointed to by the pointer `*<ptr_name>;`
Getting the address of a variable: `&<var_name>;`
Setting the value pointed to by the pointer `*<ptr_name> = <value>`

## 5.3 Arrays, Pointer Arithmetic, `sizeof`, Structs, Functions

### 5.3.1 Array Memory Addresses
Surprise! Arrays are actually (kinda like) pointers.
- *They're *not identical*, but often, arrays can be treated as pointers. 
- Arrays decay into pointers when an array is used where a pointer is expected.
    - The array decays into the pointer of the `0th element`.
```c
void set_doublearr_index(double arr[] , size_t index, double val)
//                               ||
void set_doublearr_index(double *arr , size_t index, double val)
```

For example, in the below function, `costs` is interpreted as `&costs[0]`, or the address of the 0th element of `costs`.
```c
void set_doublearr_index(double arr[], size_t index, double val) {
    arr[index] = val;
}
int main(void) {
    double costs[5] = {8.88, 10.22, 9.88, 22.22, 44.44};
    set_doublearr_index(costs, 3, 5.5);
    printf("%f\n", costs[3]);
}
```

- Elements of an array are guaranteed to be consecutively placed in the stack. Their memory addresses are also stored "consecutively."
```c
int main(){
char chararr[4] = {0};
int intarr[4] = {0};
printf("chararr[0]: %p vs chararr[1]: %p\n\n", &chararr[0], &chararr[1]);
printf("intarr[0]: %p vs intarr[1]: %p\n", (char*) &intarr[0], (char*) &intarr[1]);
``` 

`char`: one byte apart
```bash
chararr[0]:     0x7ffe74df3b2c vs
chararr[0]:     0x7ffe74df3b2d
```

`int`: four bytes apart.
```bash
intarr[0]:     0x7ffe74df3b10 vs
intarr[0]:     0x7ffe74df3b14 vs
```


### 5.3.2 pointer arithmetic
- indexing e.g., `a[i]` is just shorthand for doing this: `*(a + i)`
- Between a and i, one has to be a pointer, and one has to be an integer-like type
- `*(x + i)` points `i` elements after `x`


**Incrementing pointers (Lab 5)**
Refer to Lab 5, activity 1.
Each function receives its own copy of the pointer `arr`, initially pointing to `arr[0]`. Moving that local pointer does not change the array; modifying `*arr` changes an actual array element.

| Expression | Parsed as | Effect |
|---|---|---|
| `++arr` | `++arr` | Moves the pointer to the next element |
| `++*arr` | `++(*arr)` | Increments the pointed-to integer |
| `*arr++` | `*(arr++)` | Moves the pointer to the next element |
| `(*arr)++` | `(*arr)++` | Increments the pointed-to integer |


### 5.3.3 `sizeof`
- The `sizeof` operator in C is a unary compile-time operator used to determine the exact memory size (in bytes) of a data type, variable, or expression.
- **Return Type**: It returns an unsigned integer of type size_t. When printing it using printf(), you should always use the %zu format specifier.
```c
    printf("Size of int: %zu bytes\n", sizeof(int));       // Output: Typically 4 or 2
    printf("Size of char: %zu byte\n", sizeof(char));     // Output: Always 1
    printf("Size of num: %zu bytes\n", sizeof num);        // Output: Typically 4
    
    int my_array[] = {10, 20, 30, 40, 50};
    size_t total_bytes = sizeof(my_array);                  // Get the total size in bytes
    size_t array_length = sizeof(my_array) / sizeof(my_array[0]); // Calculate the number of elements
    printf("Total memory size: %zu bytes\n", total_bytes); 
    printf("Number of elements: %zu\n", array_length);
```

### Important Array-pointer relationship
Arrays and pointers are not equivalent.

This causes a compile error:
```c
double arr1[5] = {0};
double arr2[] = arr1;
```

However, this works:
```c
double arr1[5] = {0};
double *arr2 = arr1;
```

### 5.3.4 Structs

- A **pointer to a struct** stores the address of a struct variable.
- Declare it using the struct's type followed by `*`, and initialize it with `&`.

```c
typedef struct {
    double x, y, z;
} Acceleration;

Acceleration a = {0.2, 0.3, -0.5};
Acceleration *p = &a;
```

Here, `p` points to `a`; dereferencing `p` gives access to that struct.

**Accessing struct members: `.` vs. `->`**

| Expression | Meaning |
| --- | --- |
| `a.x` | Access member `x` of struct `a`. |
| `(*p).x` | Dereference `p`, then access member `x`. |
| `p->x` | Shorthand for `(*p).x`. |

```c
printf("%f\n", a.x);    // 0.200000
printf("%f\n", (*p).x); // 0.200000
printf("%f\n", p->x);   // 0.200000

p->x = 1.5;
printf("%f\n", a.x);    // 1.500000: a itself was modified.
```

- Use **`.` with a struct object** and **`->` with a pointer to a struct**.
- Parentheses are needed in `(*p).x` because `.` has higher precedence than unary `*`.
- `sizeof p` gives the size of the pointer; `sizeof *p` gives the size of the struct.

**Why pass structs using pointers?**

- A function can modify the caller's original struct through its pointer.
- Passing a pointer avoids passing the entire struct by value, which can reduce copying for large structs.
- It does not guarantee faster execution; compiler optimizations and the task affect performance.
- For a function that should only read the struct, use a parameter such as `Acceleration const *p`.

### 5.3.5 Functions

- C passes arguments **by value**: each parameter receives a copy of its argument.
- Passing a pointer copies the **pointer value**, not the pointed-to object.
- Dereferencing that copied pointer accesses the caller's object, allowing the function to modify it.

**Passing a value vs. passing its address**

```c
#include <stdio.h>

void set_copy(int x) {
    x = 10; // Changes only the local copy.
}

void set_ptr(int *p) {
    *p = 10; // Changes the caller's integer.
}

int main(void) {
    int n = 5;

    set_copy(n);
    printf("%d\n", n); // 5

    set_ptr(&n);
    printf("%d\n", n); // 10
}
```

| Step | Meaning |
| --- | --- |
| `set_copy(n)` | Copy the value of `n` into the parameter `x`. |
| `set_ptr(&n)` | Copy the address of `n` into the parameter `p`. |
| `*p = 10` | Write `10` into the object pointed to by `p`, which is `n`. |

**Example: correcting a struct**

Using the `Acceleration` type from 5.3.4:

```c
// Pass the struct by value and return the corrected copy.
Acceleration correct_copy(Acceleration a) {
    a.x -= 0.00000002;
    a.y += 0.00000001;
    a.z -= 0.00000003;
    return a;
}

// Pass its address and modify the original struct directly.
void correct_ptr(Acceleration *a) {
    a->x -= 0.00000002;
    a->y += 0.00000001;
    a->z -= 0.00000003;
}
```

| Approach | Call in `main` | Effect |
| --- | --- | --- |
| Pass the struct by value | `a = correct_copy(a);` | Return a corrected copy and assign it back to `a`. |
| Pass the struct's address | `correct_ptr(&a);` | Modify the original `a` through its address. |

- Calling `correct_copy(a)` without assigning its return value leaves the caller's `a` unchanged.
- `correct_ptr` returns `void` because its result is written into the original struct.

**Changing the object vs. changing the local pointer**

```c
void redirect(int *p, int *q) {
    p = q; // Changes only this function's local pointer.
}

int main(void) {
    int x = 5;
    int y = 10;
    int *ptr = &x;

    redirect(ptr, &y);
    // ptr still points to x.
}
```

- Assigning to `*p` changes the pointed-to object.
- Assigning to `p` changes only the function's local pointer.
- To change the caller's pointer variable, pass its address using a **pointer to a pointer** (`int **`); see 5.2.4.

**Arrays as function parameters**

- `void f(int arr[])` and `void f(int *arr)` declare the same parameter type.
- The function receives a pointer to the first element; it can modify elements with `arr[i]`.
- Pass the array length separately, e.g., `void f(int *arr, size_t len)`.
- Inside such a function, `sizeof arr` gives the pointer size, so it cannot determine the original array length.

The caller must supply a pointer to a suitable live object; dereferencing an uninitialized, null, or dangling pointer is UB.

## 5.4 Strings

### 5.4.1 Strings and the null character.
A string is a sequence of `char`s.
The formal definition is: A string is a contiguous sequence of `char`s terminated by and including the first null character `'\0'`.

|N|N+1|N+2|N+3|N+4|N+5|
|--|--|--|--|--|--|
|`'H'`|`'e'`|`'l'`|`'l'`|`'o'`|`'\0'`|

- We don’t know how long a string is without the null character.
- It acts as the terminator for a string, and without it, printing/reading a string will make stack overflow.

### 5.4.2 Modifiable and read-only strings
Strings come in two types:
- A **Modifiable** `char` array:
    - All of these cases are identical and we can modify it e.g., p[0] = 'a';
    - Strings constructed with `" "` automatically include the extra `'\0'`.
    - You can declare an array size but it must include space for the `'\0'`.

```c
char p[] = "hi";
char p[] = {'h', 'i', '\0'};
char p[3] = "hi";
```

- A **Read-only** `char` array
    - We cannot modify the string e.g., p[0] = 'a'; is not allowed!
    - We cannot do p[0] = 'a' now (UB!)
    - For efficiency, C will often store these in a “read-only” part of computer memory.

```c
char *p = "hi";
```

### 5.4.3 Printing strings

```c
char *p = "Hello\n";
printf("%s\n", p);
```
- **Format Specifier**: `%s` prints entire strings
- It knows when to stop because of the ‘\0’

### 5.4.4 `const`

- `const` is a **type qualifier** that specifies that something should not be modified. For pointers, its position determines whether the pointed-to value, the pointer itself, or both are protected.
- Use it when a value or function input should not be modified. It makes the intent clear and helps the compiler catch mistakes.

```c
int const x = 5; // Equivalent to: const int x = 5;
// x = 10;      // Compiler error: x is const.
```

**`const` and string literals**

Modifying a string literal is **undefined behavior (UB)**, even when the pointer has type `char *`.

```c
char *p = "hi";
// p[0] = 'a'; // UB: attempts to modify a string literal.
```

Prefer a pointer to `const char` so the compiler catches attempts to write through it:

```c
char const *p = "hi"; // Equivalent to: const char *p = "hi";
// p[0] = 'a';       // Compiler error: cannot modify through p.
p = "bye";           // Allowed: the pointer itself can change.
```

**A pointer to a const value vs. a const pointer**

The position of `const` matters:

| Declaration | Meaning | Can reassign `p`? | Can assign to `*p`? |
| --- | --- | --- | --- |
| `int *p = &x;` | Pointer to an integer | Yes | Yes |
| `int const *p = &x;` | Pointer to a const integer | Yes | No |
| `int *const p = &x;` | Const pointer to an integer | No | Yes |
| `int const *const p = &x;` | Const pointer to a const integer | No | No |

Here, assume `x` is a modifiable `int`.

- `const` **before `*`** qualifies the pointed-to type.
- `const` **after `*`** qualifies the pointer itself.
- `int const *p` and `const int *p` are equivalent.

**`const` does not make every object it points to unchangeable**

A pointer to const prevents modification **through that pointer**. A modifiable object can still be changed through another name or pointer.

```c
char text[] = "hi";
char const *p = text;

// p[0] = 'H'; // Compiler error.
text[0] = 'H'; // Allowed: text is a modifiable array.
printf("%s\n", p); // Hi
```

However, if the object itself was declared `const`, attempting to modify it, even through a cast, is UB.

**`const` in function parameters**

```c
void print_arr(int const arr[], size_t len);
// Equivalent parameter type:
void print_arr(int const *arr, size_t len);
```

- The function can read `arr[i]`, but cannot assign to `arr[i]` through this parameter.
- The local pointer can still move, e.g., `++arr`.
- The caller can pass a modifiable array; passing it does not make the original array const.

Examples from `<string.h>`:

| Function declaration | Meaning of `const` |
| --- | --- |
| `size_t strlen(char const *s);` | Reads the string; returns its length excluding `'\0'`. |
| `char *strcpy(char *dest, char const *src);` | Copies `src`, including `'\0'`, into writable `dest`. |

For `strcpy`, `dest` must have enough space, and the source and destination must not overlap.

## 5.5 Pointer Provenance

A pointer's address alone does not tell us whether using it is valid. We also need to know **where it came from**, **what memory it can access**, and **whether that memory still exists**.

The lecture uses pointer provenance as a **mental model** with two components:

| Component | Question |
| --- | --- |
| **Spatial** | Which memory locations can this pointer access? |
| **Temporal** | During what part of the program's execution can it access them? |

These are facts we must reason about; ordinary C pointers do not automatically store an array length or expiry time.

### 5.5.1 Origins: what does the pointer represent?

Two pointers with the same type can represent different things:

```c
char ch = 'b';
char text[] = "abcd";

char *p = &ch;  // Points to one character.
char *q = text; // Points to the first character of a string.
```

- `*p` is valid, but `p` does not point to a null-terminated string. Do not pass it to `%s` or `strlen`.
- `q` points into an array containing `{'a', 'b', 'c', 'd', '\0'}`, so it can be used as a string.
- Similarly, `char **r` may point to one `char *` variable or to an element of an array of `char *` pointers.
- The type alone does not tell us the array length, whether there is a string terminator, or whether the contents are writable.

**Takeaway:** trace how the pointer was created and what the caller promises before deciding how to use it.

### 5.5.2 Spatial component: access within valid bounds

For an array of `n` elements:

- Dereference only pointers to actual elements: indexes `0` to `n - 1`.
- Pointer arithmetic may produce a pointer within the same array, or **one past its end**.
- A pointer one past the end may be formed, but **must not be dereferenced**.
- Forming a pointer farther outside the array using pointer arithmetic is already UB.

```c
int arr[] = {10, 20, 30};
int *p = arr;

printf("%d\n", p[2]); // 30: valid element.
int *end = arr + 3;   // Valid: one past the end.

// printf("%d\n", *end); // UB: no element exists here.
// printf("%d\n", p[-1]); // UB: before the array.
// int *bad = p + 4;      // UB: beyond one past the end.
```

- Knowing that another variable is nearby in memory does not allow accessing it by indexing beyond this array.
- Subtracting pointers requires both to refer to the same array, or one past it. The result counts **elements**, not bytes.

**Spatial reasoning for strings**

```c
void print_str(char const *ptr) {
    while (*ptr != '\0') {
        putchar(*ptr++);
    }
}

int main(void) {
    char const s[] = "halp";
    print_str(s);
}
```

- The caller must provide a valid string with an accessible `'\0'`.
- `*ptr++` means `*(ptr++)`: read the current character, then move the pointer forward.
- The loop checks the terminator and stops without reading beyond it.
- A larger character array may contain unused space after `'\0'`; the string ends at the first `'\0'`, while the array's bounds depend on its size.

### 5.5.3 Aliasing and overlapping ranges

**Aliasing** means different pointers refer to the same object.

```c
int value = 0;
int *x_ptr = &value;
int *y_ptr = &value;

*x_ptr = 5;
*y_ptr = 20;
printf("%d\n", *x_ptr); // 20, because both point to value.
```

Writing through one pointer can therefore change what another pointer reads.

**Example: copying an array without modifying the source**

```c
void copy_arr(int const from[], int to[], size_t nmemb) {
    for (size_t idx = 0; idx < nmemb; ++idx) {
        to[idx] = from[idx];
    }
}
```

To copy correctly while leaving the source unchanged, this function requires:

- `from` has at least `nmemb` readable elements.
- `to` has at least `nmemb` writable elements.
- The ranges `[from, from + nmemb)` and `[to, to + nmemb)` do not overlap. The closing `)` excludes the endpoint.

What if the caller passes overlapping parts of one array?

```c
int arr[] = {1, 2, 3, 4};
copy_arr(arr, arr + 1, 3);
// Result: {1, 1, 1, 1}, rather than the intended {1, 1, 2, 3}.
```

- Writing `to[0]` changes `from[1]` before it is read; subsequent iterations propagate that changed value.
- `const from` prevents writes **through `from`**, but does not prevent writes to the same elements through `to`.
- This loop's overlapping accesses are not automatically UB; this call violates the stated copying contract and gives the wrong result.

### 5.5.4 Temporal component: the pointed-to object must still exist

An object's **lifetime** is the period during which it exists. A pointer can only access it during that period.

**Returning a pointer to a local array**

```c
int *get_arr(void) {
    int arr[] = {0, 1, 2};
    return arr; // Bad: arr's lifetime ends when the function returns.
}

int main(void) {
    int *p = get_arr();
    printf("%d\n", p[0]); // UB: the local array no longer exists.
}
```

- Returning the pointer does not copy the array or extend its lifetime.
- The pointer is now a **dangling pointer**: its former object no longer exists.
- Memory that appears to retain the old values does not make accessing it valid.

**Leaving a block**

```c
int *p;
{
    int x = 10;
    p = &x;
} // x's lifetime ends here.

// printf("%d\n", *p); // UB: x no longer exists.
```

The pointer variable may still exist even after the pointed-to object has stopped existing.

### 5.5.5 Uninitialized pointers and pointers to pointers

Declaring a local pointer does not create an object for it to point to:

```c
int *p;
// *p = 5; // UB: p is uninitialized; it has no valid target.
```

Initialize it with the address of a suitable live object before dereferencing:

```c
int x;
int *p = &x;
*p = 5; // Valid: writes to x.
```

However, we can pass the **address of an uninitialized pointer variable** to a function that assigns it a value:

```c
void foo(int **x) {
    *x = nullptr; // C23: assigns a null pointer to the caller's p.
}

int main(void) {
    int *p;
    foo(&p);
    // p is now a null pointer; dereferencing p would be UB.
}
```

- `&p` is valid because the pointer variable `p` itself exists.
- `x` points to `p`, so `*x = nullptr` initializes `p`.
- The function does not read the old value of `p` or dereference it.

**Before using a pointer, check:** its origin, valid bounds, the object's lifetime, permission to read/write, and whether other pointers access the same memory.


# L6: Dynamic memory allocation
## 6.1 Memory regions, pointers, and `const`

### 6.1.1 Where objects are stored

A typical implementation separates program memory into these regions:

| Region | Contains | Lifetime / management |
| --- | --- | --- |
| Code | Compiled instructions | Exists while the program runs. |
| Read-only data | String literals such as `"hello"` | Static lifetime; modifying a string literal is UB. |
| Stack | Most ordinary local variables and function-call data | Automatic storage is reclaimed when the relevant block or call ends. |
| Heap | Objects created by dynamic allocation | Remain allocated until explicitly deallocated. |
| Static data | File-scope variables and local `static` variables | Exist for the entire program; covered in Lecture 9. |

These regions are an implementation model. **A pointer variable and the object it points to can have different lifetimes.**

```c
char s[] = "halp";
char const *t = "halp";
```

- `s` is a local array containing its own modifiable copy, including `'\0'`.
- `t` is a local pointer variable pointing to a string literal.
- Changing `t` does not change the literal. Modifying the literal itself is UB.

### 6.1.2 `const` in different positions

Assume `char str[] = "hi";` and consider each declaration separately:

| Declaration | Can change `p`? | Can change a character through `p`? |
| --- | --- | --- |
| `char *p = str;` | Yes | Yes |
| `char const *p = str;` | Yes | No |
| `char *const p = str;` | No | Yes |
| `char const *const p = str;` | No | No |

- `const char *p` is equivalent to `char const *p`.
- Before `*`: qualifies the pointed-to type. After `*`: qualifies the pointer itself.
- A pointer to const restricts access through that pointer; another valid reference may still modify an originally modifiable object.

## 6.2 Automatic and dynamic lifetimes

### 6.2.1 Why returning a local array fails

```c
double *bad_costs(void) {
    double costs[] = {1.0, 2.0, 3.0};
    return costs; // The local array's lifetime ends on return.
}
```

- `return costs` produces a pointer to the first element; it does not copy the array.
- Accessing that array through the returned pointer is UB because the array no longer exists.
- Returning a pointer does not extend the pointed-to object's lifetime.

### 6.2.2 Dynamic allocation

Dynamic allocation creates storage whose lifetime is independent of the function call that requested it.

Use it when:

- Data must survive after the allocating function returns.
- An array is too large for the available stack.
- The required size is known only at runtime.
- The storage may need resizing, or a data structure grows as the program runs.

**Course convention:** the slides allow assuming allocation succeeds in CS1010. General C code should check for failure; the examples below include checks. The slides also disallow VLAs for the remainder of the course.

The examples use C23's `nullptr`. In older C, use `NULL`. Allocation examples assume positive sizes and byte counts that fit in `size_t`.

## 6.3 The allocation family: `<stdlib.h>`

| Function | Purpose | Initial contents / important behavior |
| --- | --- | --- |
| `malloc(bytes)` | Allocate `bytes` contiguous bytes. | Contents are uninitialized. |
| `calloc(count, size)` | Allocate space for `count` elements of `size` bytes each. | Sets every allocated byte to zero. |
| `realloc(ptr, bytes)` | Resize a previously allocated block. | Preserves the initial contents up to the smaller of the old and new sizes; added bytes are uninitialized. |
| `free(ptr)` | Deallocate a block. | Does not reset the caller's pointer or free other allocations referenced by the block. |

The allocating functions return a pointer, or a null pointer on failure. `free` returns no value.

### 6.3.1 Allocating the correct number of bytes

```c
#include <stdlib.h>

int *arr = malloc(n * sizeof *arr); // n integers
```

- `sizeof *arr` is the size of one element; `sizeof arr` is the size of the pointer.
- `sizeof *arr` does not evaluate the dereference here, so the allocation declaration is valid.
- For non-VLA types, `sizeof` does not evaluate its operand. It returns a `size_t`; print it using `%zu`.
- In C, `void *` converts automatically to an object-pointer type on assignment. A cast on `malloc` is unnecessary; include `<stdlib.h>`.
- A `void *` must be converted to a suitable object-pointer type before accessing the stored object.
- Keep the element count separately: a pointer does not carry an array length.
- Ensure `n * sizeof *arr` cannot overflow before allocating from an unchecked size.

### 6.3.2 Returning a dynamically allocated array

```c
#include <stdio.h>
#include <stdlib.h>

double *get_costs(void) {
    double *costs = malloc(3 * sizeof *costs);
    if (costs == nullptr) {
        return nullptr;
    }

    costs[0] = 1.0;
    costs[1] = 2.0;
    costs[2] = 3.0;
    return costs; // Caller receives ownership of this allocation.
}

int main(void) {
    double *c = get_costs();
    if (c == nullptr) {
        return EXIT_FAILURE;
    }

    printf("%f\n", c[0]);
    free(c);
    c = nullptr;
}
```

The local pointer `costs` disappears when `get_costs` returns. The allocated array remains alive until `free(c)`.

### 6.3.3 `calloc`

```c
int *counts = calloc(n, sizeof *counts);
if (counts == nullptr) {
    // Handle failure before accessing counts[i].
}
```

- Allocates the array and initializes its bytes to zero; integer elements start at zero.
- Bytewise zeroing is the guarantee. Do not generalize it to every possible pointer or floating-point representation.
- `malloc` does not initialize the elements; assign values before reading them.

### 6.3.4 `realloc`

Use a temporary pointer when requesting a **positive** new size:

```c
int *resized = realloc(arr, new_count * sizeof *arr);
if (resized == nullptr) {
    // arr still owns the original allocation; handle the failure.
} else {
    arr = resized;
    // Use arr for future accesses; initialize any new elements.
}
```

- The allocation may stay in place or move to a new address.
- On success, use the returned pointer. Old pointers into the previous allocation must no longer be used, even if the returned address looks unchanged.
- On failure for a positive requested size, the original allocation remains valid.
- `arr = realloc(arr, ...)` can lose the only reference to the original block if resizing fails.
- Handle an intended zero-element result separately, e.g., by freeing the allocation.

## 6.4 Freeing memory and common mistakes

### 6.4.1 Rules for `free`

- Free each owned allocation exactly once when it is no longer needed.
- Pass its **base pointer**: the start returned by the allocator, not an interior element.
- `free(nullptr)` is valid and does nothing.
- Freeing a block does not set pointer variables to null.
- Setting one pointer to `nullptr` does not repair other aliases to the freed block.

```c
int *p = malloc(3 * sizeof *p);
// Check p, initialize its elements, and use them.
free(p);
p = nullptr;
```

### 6.4.2 Common errors

| Mistake | Example | Consequence |
| --- | --- | --- |
| Dereference after allocation failure | `p[0] = 1;` when `p == nullptr` | UB. |
| Read an uninitialized element | Reading an integer immediately after `malloc` | An indeterminate value; may cause UB. Initialize first. |
| Use after free | `free(p);` followed by `p[0]` | UB. |
| Double free | Free the same allocation twice, including through aliases. | UB. |
| Free an interior pointer | `free(p + 1);` | UB. |
| Free automatic storage | `int x; free(&x);` | UB. |
| Free a string literal | `free("hello");` | UB. |
| Lose the final pointer to an allocation | Overwrite `p` before freeing its old allocation. | Memory leak. |
| Free only an outer pointer array | `free(grid);` without freeing owned rows. | Row allocations leak. |

A **memory leak** is allocated storage that is no longer properly released or reachable. A leak alone is not automatically UB, but wastes resources.

## 6.5 Dynamically allocated grids and structs

### 6.5.1 An array of row pointers

For `rows` rows and `cols` columns, allocate:

1. An array of `rows` pointers.
2. A separate array of `cols` integers for each row.

```c
int **create_grid(size_t rows, size_t cols) {
    if (rows == 0 || cols == 0) {
        return nullptr;
    }

    int **grid = malloc(rows * sizeof *grid);
    if (grid == nullptr) {
        return nullptr;
    }

    for (size_t r = 0; r < rows; ++r) {
        grid[r] = malloc(cols * sizeof *grid[r]);
        if (grid[r] == nullptr) {
            for (size_t i = 0; i < r; ++i) {
                free(grid[i]);
            }
            free(grid);
            return nullptr;
        }
    }
    return grid;
}

void free_grid(int **grid, size_t rows) {
    if (grid == nullptr) {
        return;
    }
    for (size_t r = 0; r < rows; ++r) {
        free(grid[r]);
    }
    free(grid);
}
```

- Assign row elements before reading them; the rows above are uninitialized.
- `grid[r][c]` is equivalent to `*(*(grid + r) + c)`.
- Each row is contiguous, but separately allocated rows need not be adjacent.
- Free the rows **before** the pointer array, so their addresses remain accessible.
- This layout also supports **jagged arrays**, where each row has a different length.
- For an array of separately allocated strings, free each owned string, then the pointer array.

### 6.5.2 Pointer expressions in a grid

For `int **grid`:

| Expression | Type | Meaning |
| --- | --- | --- |
| `grid + 1` | `int **` | Address of the next row-pointer slot. |
| `grid[1]` | `int *` | Pointer stored in that slot: the start of the second row. |
| `*grid` | `int *` | The first row's pointer. |
| `*grid + 1` | `int *` | Pointer to the second integer of the first row. |
| `**grid` | `int` | First integer of the first row. |
| `**grid + 1` | `int` | That integer's value plus one. |

### 6.5.3 An array of pointers is different from a fixed 2D array

```c
char a[5][2];
char (*p)[2] = a; // Valid: pointer to a row containing two chars.
// char **q = a; // Incompatible types: a does not contain char* slots.
```

| Property | `int a[R][C]` | Separately allocated rows through `int **grid` |
| --- | --- | --- |
| What the outer elements are | Arrays of `C` integers. | Pointers to rows. |
| Layout | All rows are contiguous. | Row allocations may be scattered. |
| Decay of outer array | Pointer to a row: `int (*)[C]`. | A row-pointer array decays to `int **`. |
| Moving one outer element | Skips an entire row. | Skips one pointer slot. |
| Row lengths | Uniform. | Can differ. |

Both permit `[r][c]` syntax, but their types and memory layouts differ. Casting a fixed 2D array to `int **` does not create row pointers.

### 6.5.4 Allocating a struct

```c
typedef struct {
    int x, y;
} Position;

Position *get_pos(void) {
    Position *pos = malloc(sizeof *pos);
    if (pos == nullptr) {
        return nullptr;
    }
    pos->x = 5;
    pos->y = 6;
    return pos;
}
```

The caller checks the result, accesses members using `->`, and eventually calls `free` on the returned allocation. If a struct owns additional allocations, those require their own cleanup.

## 6.6 Ownership and borrowing

Ownership is a **programming convention**, not something C's pointer types enforce.

- An **owner** is responsible for releasing an allocation or transferring that responsibility.
- A **borrower** temporarily accesses an object without taking responsibility for freeing it.
- Copying a pointer creates another reference to the same object; it does not create another allocation.
- The **final owner** must perform the cleanup.
- Decide who owns each allocation, including allocations nested inside structs or pointer arrays.

### 6.6.1 Ownership through function calls

| Function contract | Caller responsibilities |
| --- | --- |
| Function borrows an input pointer. | Retain ownership; free the allocation later if it is yours. |
| Function consumes an owned input allocation. | Stop treating it as yours; the callee must release it or transfer ownership onward. |
| Function returns a new owned allocation. | Check the result and eventually free it or transfer ownership. |
| Function returns a borrowed pointer into an existing object. | Keep the original object alive; do not independently free the borrowed pointer. |

Returning a pointer alone does not establish ownership. **Follow the function's documented contract**, especially when it might return an alias or reuse an input allocation.

### 6.6.2 Returning an allocation through `int **`

```c
int create_ones(int **out, size_t n) {
    if (out == nullptr || n == 0) {
        return -1;
    }
    int *arr = malloc(n * sizeof *arr);
    if (arr == nullptr) {
        return -1;
    }
    for (size_t i = 0; i < n; ++i) {
        arr[i] = 1;
    }
    *out = arr; // Transfer the new allocation to the caller.
    return 0;
}
```

Call it with a pointer variable that is ready to receive the allocation:

```c
int *arr = nullptr;
if (create_ones(&arr, 5) == 0) {
    // Use arr[0] through arr[4].
    free(arr);
}
```

- `&arr` lets the function assign the caller's pointer.
- The function returns a status normally and the allocation through `out`.
- Do not overwrite an existing owned allocation without first handling its ownership.

# L7. Recursion II

## 7.1 Ownership across multiple functions

Ownership can pass through several functions before reaching the final owner.

- A row constructor allocates a row and returns ownership to a grid constructor.
- The grid constructor returns ownership of the grid and its owned rows to its caller.
- A printing function borrows the grid.
- The final owner frees each row, then the row-pointer array.

**Example: a find-and-replace function's contract matters**

| Design | Input string | Returned string | What the caller frees |
| --- | --- | --- | --- |
| Borrow input and return a fresh result. | Remains owned by caller. | New allocation owned by caller. | Both input and result. |
| Consume input and return an owned result. | Ownership passes to the function. | May reuse or replace the original allocation. | Result, according to the contract; do not separately free the consumed input. |

The Lecture 7 example uses the second design. An exam question may specify a different one: check whether inputs may be modified or freed, and whether the result must be independent.

## 7.2 Recursive data structures

A recursive data structure contains links to smaller instances of the same kind of structure. Recursive functions can follow that structure directly.

| Structure | Base case | Recursive case |
| --- | --- | --- |
| Linked list | Empty list. | One item followed by another list. |
| Tree | Empty tree. | One item with a collection of child trees. |

The examples below assume finite, acyclic structures. Cleanup examples assume separately allocated, owned nodes.

## 7.3 Linked lists

### 7.3.1 Definition

```c
typedef struct LinkedList {
    int item;
    struct LinkedList *tail;
} LinkedList;

LinkedList *list = nullptr; // Empty list.
```

- Each node stores an item and a pointer to the rest of the list.
- `tail == nullptr` means that node is the last one.
- `list == nullptr` means the entire list is empty.
- A declaration such as `LinkedList node;` creates a node object; it does not represent an empty list.

**Why a pointer member?**

```c
// Invalid: the type would need to contain another complete instance of itself.
// struct Bad { int item; struct Bad tail; };
```

A pointer has a finite size even when the pointed-to struct is not yet fully defined.

### 7.3.2 Print and sum

```c
void print_list(LinkedList const *list) {
    if (list == nullptr) {
        return;
    }
    printf("%d ", list->item);
    print_list(list->tail);
}

int sum_list(LinkedList const *list) {
    if (list == nullptr) {
        return 0;
    }
    return list->item + sum_list(list->tail);
}
```

- Printing handles the current item, then delegates the tail.
- Summing adds the current item to the tail's sum; assume the result fits in `int`.
- Moving the print after the recursive call prints the values in reverse order without changing the links.

### 7.3.3 Freeing a list

```c
void free_list(LinkedList *list) {
    if (list == nullptr) {
        return;
    }
    free_list(list->tail);
    free(list);
}
```

Free the tail before freeing the node that stores its address. After calling this function, the caller's old head pointer must not be used; set it to `nullptr` if retaining that variable.

An iterative cleanup can avoid deep recursion by saving `next = node->tail` **before** freeing `node`, then continuing from `next`.

### 7.3.4 Reversing a list

```c
LinkedList *reverse_list(LinkedList *list) {
    if (list == nullptr || list->tail == nullptr) {
        return list;
    }

    LinkedList *rest = reverse_list(list->tail);
    list->tail->tail = list;
    list->tail = nullptr;
    return rest;
}
```

1. An empty list or a one-node list is already reversed.
2. Recursively reverse the tail.
3. The old second node is now the end of that reversed tail; link it to the old first node.
4. Set the old first node's `tail` to `nullptr`, making it the new last node.
5. Return the head of the reversed tail.

Call using `list = reverse_list(list);` because the head changes. This reverses links without allocating or freeing nodes. Omitting `list->tail = nullptr` creates a cycle for a list with multiple nodes.

## 7.4 Trees

### 7.4.1 A tree with a linked list of children

Use a separate linked-list type to store child-tree pointers:

```c
typedef struct ChildLink {
    struct Tree *tree;
    struct ChildLink *tail;
} ChildLink;

typedef struct Tree {
    int item;
    ChildLink *sub_trees;
} Tree;
```

- A `Tree` stores its item and a pointer to its list of children.
- Each `ChildLink` stores a child-tree pointer and the next child-link pointer.
- `tree == nullptr`: empty tree.
- `tree->sub_trees == nullptr`: a leaf with no children.
- Child links and tree nodes are different objects; both may require freeing.

### 7.4.2 Traversing and counting

```c
void print_tree(Tree const *tree) {
    if (tree == nullptr) {
        return;
    }
    printf("%d ", tree->item);
    for (ChildLink const *p = tree->sub_trees;
         p != nullptr; p = p->tail) {
        print_tree(p->tree);
    }
}

size_t count_nodes(Tree const *tree) {
    if (tree == nullptr) {
        return 0;
    }
    size_t count = 1;
    for (ChildLink const *p = tree->sub_trees;
         p != nullptr; p = p->tail) {
        count += count_nodes(p->tree);
    }
    return count;
}
```

- Count a nonempty tree as **one current node plus the counts of all child trees**.
- `count_nodes` includes the root. Adjust this if the question asks only for descendants.
- Printing before visiting children is preorder; printing after them is postorder.
- For children stored in an array, loop over that array instead; the recursive decomposition is the same.

### 7.4.3 Freeing an owned tree

```c
void free_tree(Tree *tree) {
    if (tree == nullptr) {
        return;
    }

    ChildLink *p = tree->sub_trees;
    while (p != nullptr) {
        ChildLink *next = p->tail;
        free_tree(p->tree);
        free(p);
        p = next;
    }
    free(tree);
}
```

For this representation, free each child subtree, its child-link node, and finally the parent tree node. Save the next link before freeing the current one.

## 7.5 Planning recursive functions

1. Define exactly what the function returns or changes for one input structure.
2. Handle the empty or smallest structure before dereferencing pointers.
3. Identify the smaller recursive input: a tail or each child subtree.
4. Assume the recursive call fulfills its contract; combine that result with the current node.
5. For mutation and cleanup, decide which objects must still exist after each call.

Deep lists or trees can exhaust the call stack. For a tree, recursion depth follows its height; a long chain can be as deep as its number of nodes.

# L8. Problem solving techniques: recursive backtracking and loop invariants

## 8.1 Recursive backtracking

Backtracking explores possible solutions by making a choice, recursively solving the remaining problem, and undoing that choice when another branch must be tried.

1. Identify the current partial solution and the next undecided part.
2. Try a candidate choice.
3. Recursively solve the smaller remaining problem.
4. If the branch fails, restore the state before trying another choice.
5. At a complete candidate, check whether it satisfies the problem's rules.

**The recursive call's contract matters:** does it find one solution, print all solutions, count them, or return the best one?

| Goal | On finding a solution | On returning to the caller |
| --- | --- | --- |
| Find one solution in a shared array/grid. | Return success immediately. | Retain the successful choices. |
| Print or count all solutions. | Output the candidate or contribute to the count. | Restore state and continue exploring. |
| Find a best solution. | Compare against the best result found so far. | Preserve a copy of the best result before restoring shared state. |

Local scalar variables have separate copies in different calls. Mutations through pointers or array parameters affect shared storage, so they may need explicit undoing.

## 8.2 Example: generating permutations

Task: print all arrangements of the integers `1` through `n`, using each exactly once.

For `n = 3`, the outputs are `123`, `132`, `213`, `231`, `312`, and `321`.

### 8.2.1 The slide approach: generate, then verify

- State: an array and the index of the next unfilled position.
- At each position, try every value from `1` through `n`.
- Base case: all positions are filled.
- Print the candidate only if every value is distinct.

```c
bool all_distinct(int const arr[], size_t n) {
    for (size_t i = 0; i < n; ++i) {
        for (size_t j = i + 1; j < n; ++j) {
            if (arr[i] == arr[j]) {
                return false;
            }
        }
    }
    return true;
}

void permutations(int arr[], size_t n, size_t idx) {
    if (idx == n) {
        if (all_distinct(arr, n)) {
            for (size_t i = 0; i < n; ++i) {
                printf("%d%c", arr[i], i + 1 == n ? '\n' : ' ');
            }
        }
        return;
    }

    for (size_t value = 1; value <= n; ++value) {
        arr[idx] = (int)value;
        permutations(arr, n, idx + 1);
    }
}
```

Call `permutations(arr, n, 0)` with an array of at least `n` integers, and a positive `n` small enough to fit in `int`.

- The prefix `arr[0..idx)` represents the current partial solution.
- In this implementation, no explicit reset is needed: every recursive branch overwrites each remaining slot before reading the complete candidate.
- It generates `n^n` full candidates, of which `n!` are permutations.
- **Pruning:** reject a value already present in the prefix before recursing. This avoids exploring branches that cannot become valid permutations.

## 8.3 Example: 4-by-4 Sudoku

Each row, column, and 2-by-2 box must contain `1`, `2`, `3`, and `4` once each. Use `0` to represent a blank.

### 8.3.1 Testing a possible placement

The following helper assumes `grid[r][c]` is currently blank:

```c
bool can_place(int grid[4][4], size_t r, size_t c, int value) {
    for (size_t i = 0; i < 4; ++i) {
        if (grid[r][i] == value || grid[i][c] == value) {
            return false;
        }
    }

    size_t box_r = (r / 2) * 2;
    size_t box_c = (c / 2) * 2;
    for (size_t i = box_r; i < box_r + 2; ++i) {
        for (size_t j = box_c; j < box_c + 2; ++j) {
            if (grid[i][j] == value) {
                return false;
            }
        }
    }
    return true;
}
```

### 8.3.2 Solving with backtracking

```c
bool solve_sudoku(int grid[4][4]) {
    for (size_t r = 0; r < 4; ++r) {
        for (size_t c = 0; c < 4; ++c) {
            if (grid[r][c] != 0) {
                continue;
            }

            for (int value = 1; value <= 4; ++value) {
                if (!can_place(grid, r, c, value)) {
                    continue;
                }
                grid[r][c] = value;
                if (solve_sudoku(grid)) {
                    return true; // Retain the completed solution.
                }
                grid[r][c] = 0; // Undo this failed choice.
            }
            return false; // No value works in the first blank found.
        }
    }
    return true; // No blanks remain.
}
```

- This version assumes the original clues are in `1..4` and do not conflict. Validate them separately if the question does not promise this.
- Each call is responsible for the first blank it finds.
- Each recursive call handles the remaining blanks.
- Every unsuccessful branch restores the blank it filled.
- A successful branch returns without unsetting its choices, preserving the solution.
- The slides also motivate verifying a fully filled candidate. This version prunes invalid placements earlier, so a complete grid is valid under the stated input assumption.

## 8.4 Reasoning about loops using invariants

A **loop invariant** is a property that holds at a specified recurring point, usually the start of every iteration.

An index can represent a **boundary between processed and unprocessed work**.

Use half-open ranges:

- `arr[0..idx)` means indexes `0` through `idx - 1`.
- `arr[idx..n)` is the remaining suffix.
- `idx == 0`: the processed prefix is empty.
- `idx == n`: the entire array has been processed.

### 8.4.1 Initialization, preservation, and termination

| Stage | What to establish |
| --- | --- |
| Initialization | The invariant is true before the first iteration. |
| Preservation | Assuming it is true at an iteration's start, the body and update make it true at the next start. |
| Termination | The invariant together with the stopping condition implies the required result. |

Also identify **progress**: a nonnegative quantity such as `n - idx` or `end - begin` decreases, explaining why the loop eventually stops.

### 8.4.2 Bounds must be checked before array access

```c
size_t first_positive(int const arr[], size_t n) {
    size_t idx = 0;
    while (idx < n && arr[idx] <= 0) {
        ++idx;
    }
    return idx; // n means no positive element was found.
}
```

- At the loop's start, all elements in `arr[0..idx)` are nonpositive.
- `idx < n` is checked before `arr[idx]` because `&&` evaluates left to right and short-circuits.
- Reversing those conditions can access out of bounds when the array is empty or has no positive element.

## 8.5 Linear search and summation

### 8.5.1 Linear search

```c
size_t find_value(int const arr[], size_t n, int value) {
    for (size_t idx = 0; idx < n; ++idx) {
        if (arr[idx] == value) {
            return idx;
        }
    }
    return n;
}
```

Invariant at the start of an iteration: **no element in `arr[0..idx)` equals `value`**.

- Initially, that range is empty.
- A nonmatching element can be added to the checked prefix.
- If the loop finishes, the whole array has been checked.
- The sentinel `n` is not a valid element index; check it before indexing with the result.

### 8.5.2 Summation

```c
int sum_array(int const arr[], size_t n) {
    int total = 0;
    for (size_t idx = 0; idx < n; ++idx) {
        total += arr[idx];
    }
    return total;
}
```

Invariant: **`total` equals the sum of `arr[0..idx)`**, assuming the sums fit in `int`.

- Initialization: the empty prefix has sum zero.
- Preservation: adding `arr[idx]` extends the summed prefix by one element.
- Termination: `idx == n`, so the prefix is the entire array.

## 8.6 Binary search

Binary search uses sorted order to repeatedly discard a region that cannot contain the target.

The following follows the slides' boundary strategy, with an extra guard for an empty array. The array must be sorted in ascending, nondecreasing order.

```c
bool binary_exists(int const arr[], size_t length, int value) {
    if (length == 0 || value < arr[0]) {
        return false;
    }

    size_t begin = 0;
    size_t end = length;
    while (end - begin > 1) {
        size_t mid = begin + (end - begin) / 2;
        if (arr[mid] <= value) {
            begin = mid;
        } else {
            end = mid;
        }
    }
    return arr[begin] == value;
}
```

### 8.6.1 Boundary meanings

- `begin` is a valid index with `arr[begin] <= value`.
- Either `end == length`, or `arr[end] > value`.
- `0 <= begin < end <= length`; possible matches remain in `[begin, end)`.
- The conceptual upper boundary at `length` is not an element: **never read `arr[length]`**.

### 8.6.2 Why it works

- The initial guard establishes `arr[begin] <= value`.
- While the interval has at least two positions, `begin < mid < end`.
- If `arr[mid] <= value`, move `begin` to `mid`.
- Otherwise, move `end` to `mid`.
- Each update preserves the boundary properties and reduces `end - begin`.
- When one candidate index remains, compare it to `value`.
- Computing `mid` as `begin + (end - begin) / 2` avoids overflowing `begin + end`.

## 8.7 Partitioning an array

Task: rearrange the elements so that all values `<= pivot` precede all values `> pivot`.

Example: `{9, 5, 3, 10, 0}` with pivot `8` may become `{0, 5, 3, 10, 9}`. Neither region needs to be internally sorted.

### 8.7.1 Invariant and implementation

This version uses an **exclusive right boundary**, making empty arrays straightforward:

| Region | Property |
| --- | --- |
| `[0, left)` | Already known to be `<= pivot`. |
| `[left, right)` | Not yet classified. |
| `[right, n)` | Already known to be `> pivot`. |

```c
size_t partition(int arr[], size_t n, int pivot) {
    size_t left = 0;
    size_t right = n;

    while (left < right) {
        if (arr[left] <= pivot) {
            ++left;
        } else if (arr[right - 1] > pivot) {
            --right;
        } else {
            int temp = arr[left];
            arr[left] = arr[right - 1];
            arr[right - 1] = temp;
            ++left;
            --right;
        }
    }
    return left; // Boundary between the two completed regions.
}
```

- Each iteration classifies at least one element, shrinking the unknown region.
- At termination, `left == right`, so no unclassified elements remain.
- The return value `k` gives `[0, k)` with values `<= pivot`, and `[k, n)` with values `> pivot`.
- It handles an empty array, one element, all values on one side, and repeated values.

### 8.7.2 Mistakes illustrated in the slides

- Initializing an unsigned right index as `n - 1` when `n == 0` causes wraparound.
- An inner loop such as `while (arr[idx] <= pivot)` can run beyond the array unless it also checks bounds.
- Pointer/index movements must preserve the invariant and make progress.
- With an inclusive right index, stopping at equal indexes leaves one element whose classification must still be reasoned about.
- **Unsigned subtraction does not become negative:** decrementing `size_t` zero wraps to a large value.

# L9. Static lifetimes, file scope, and input

## 9.1 Scope and lifetime are different

- **Scope**: where an identifier can be used in the source code.
- **Lifetime**: when the object exists during execution.
- A name becoming inaccessible does not necessarily mean the pointed-to allocation is deallocated.

| Example | Identifier scope | Object lifetime |
| --- | --- | --- |
| Ordinary local `int x;` | Block | Automatic; ends when its block exits. |
| Local `int *p;` | Block | The pointer variable itself has automatic lifetime. |
| Allocation referenced by `p = malloc(...)` | The allocation has no identifier of its own. | Dynamic; until deallocated. |
| File-scope `int count;` | From its declaration to the end of the file. | Static; entire execution. |
| Local `static int count;` | Block | Static; entire execution. |

```c
void leak(void) {
    int *p = malloc(5 * sizeof *p);
} // p disappears; the allocation remains and has been leaked.
```

The same distinction applies to a file-scope pointer: its own static lifetime does not automatically free its dynamic allocation.

## 9.2 File-scope variables: shared state

A variable declared outside all functions has file scope and static storage duration.

```c
#include <stdio.h>

int count; // Initialized to zero.

void increment(void) {
    ++count;
}

int main(void) {
    increment();
    increment();
    printf("%d\n", count); // 2
}
```

- The variable exists for the entire program execution.
- Static-duration objects without an explicit initializer are initialized appropriately: arithmetic values to zero, pointers to null, and aggregate members recursively.
- Functions with access to the declaration can share and modify the variable.
- A function may therefore change state that is not mentioned in its parameters.

### 9.2.1 Uses and tradeoffs

- **Shared state:** e.g., several functions controlling the same robot motors.
- **Additional output:** e.g., an error indicator alongside a function's normal return value.
- Shared mutable state makes behavior harder to trace; prefer parameters and explicit output values when practical.

```c
int error = 0; // 0 means success; 1 means division by zero.

double safe_divide(double a, double b) {
    if (b == 0.0) {
        error = 1;
        return 0.0;
    }
    error = 0; // Clear an error from a previous call.
    return a / b;
}
```

The caller checks `error` after calling. An alternative is an output parameter, such as `int *err`, which makes the extra output explicit.

### 9.2.2 Library error state: `errno`

- `<errno.h>` provides `errno`, a macro used to access library error state.
- Some library functions document setting it when an error occurs.
- Reset it to zero before a call when that function's error-checking procedure requires it.
- Successful calls do not generally promise to reset a previous error.
- `perror("message")`, from `<stdio.h>`, writes a message describing the current `errno` to standard error.
- Follow the particular function's return-value and error contract; `errno` alone is not a universal success/failure indicator.

## 9.3 Local `static` variables

A local `static` variable has **block scope and static lifetime**: its name is local, but its stored value survives between calls.

```c
void log_msg(char const *msg) {
    static int count = 0;
    ++count;
    printf("%d: %s\n", count, msg);
}
```

Calling `log_msg("start")`, then `log_msg("done")`, prints:

```text
1: start
2: done
```

- The initializer does not run afresh on each function call.
- Without an explicit initializer, a static integer starts at zero.
- An ordinary local `int count = 0;` would be reinitialized on every call.
- Recursive calls also share the same local static object; they do not get separate copies of it.
- Persistent state can make later calls depend on earlier calls.

The slides focus on `static` for block-scope variables. Its uses with file-scope objects and functions concern linkage and are outside this lecture's examinable scope.

## 9.4 `strtok`: persistent state in a library function

`strtok`, from `<string.h>`, splits a **modifiable string** into tokens separated by delimiter characters.

```c
#include <stdio.h>
#include <string.h>

int main(void) {
    char text[] = "a,bc,d";
    char *part = strtok(text, ",");

    while (part != nullptr) {
        printf("%s\n", part);
        part = strtok(nullptr, ",");
    }
}
```

Output:

```text
a
bc
d
```

- First call: pass the input array.
- Later calls: pass `nullptr` to continue the same tokenization.
- It replaces separator characters with `'\0'`, making each returned token a string.
- It remembers where to continue between calls; a static pointer can implement that state.
- It returns `nullptr` when no tokens remain.
- The delimiter argument specifies a **set of separator characters**, not a substring to match.
- Consecutive separators are skipped; they do not produce empty tokens.
- Returned pointers refer into the original buffer; they are borrowed and must not be individually freed.
- The input buffer must remain alive. Do not pass a string literal for modification.
- Starting tokenization on another string changes the remembered state, which complicates nested tokenization.

## 9.5 A general input-processing workflow

1. Read characters or a string from `stdin`.
2. Check the reading function's result.
3. Convert or parse the string if other types are required.
4. Validate the conversion and pass the data to the rest of the program.
5. Free any owned input buffer when finished.

The lecture assumes ASCII input and focuses on standard input. Shell redirection can supply it from a file, e.g., `./program < input.txt`.

| Function | Main job | Who supplies storage? | Result to check |
| --- | --- | --- | --- |
| `getchar()` | Read one character. | No string buffer needed. | Character value as `int`, or `EOF`. |
| `fgets(buffer, count, stdin)` | Read into a fixed-capacity buffer. | Caller. | `buffer` on success; null pointer on failure/no characters at EOF. |
| `getline(&line, &capacity, stdin)` | Read a line with a resizable buffer. | Can allocate/resize for caller. | Character count, or `-1`. |
| `sscanf(text, format, ...)` | Parse an existing string. | Caller supplies output variables. | Number of successful assignments, or `EOF` for an initial input failure. |

## 9.6 `getchar`: one character at a time

```c
#include <stdio.h>

int main(void) {
    int ch;
    while ((ch = getchar()) != EOF) {
        putchar(ch);
    }
}
```

- The return type is `int` so it can represent character values and the distinct sentinel `EOF`.
- Store the result in an `int`; check `EOF` before converting to `char`.
- `EOF` indicates end of input or a reading error; use the named constant rather than assuming a particular number.
- Pressing Enter contributes a newline character, `'\n'`.
- In a typical terminal, Ctrl+D on Unix-like systems, or Ctrl+Z followed by Enter on Windows, signals end of input.

The parentheses in `(ch = getchar()) != EOF` ensure the character is assigned before the comparison.

## 9.7 `fgets`: reading into a caller-provided buffer

```c
char buffer[100];
if (fgets(buffer, sizeof buffer, stdin) != nullptr) {
    printf("%s", buffer);
}
```

- With a valid buffer and `count >= 2`, reads at most `count - 1` characters, then appends `'\0'` on success.
- Stops after reading a newline, reaching EOF, or filling that character limit.
- A newline is included if it was read.
- A line that is longer than the buffer is read in pieces; the remaining characters stay in the input stream.
- EOF after some characters can still produce a successful final partial line.
- If no characters are read before EOF, or a read error occurs, it returns a null pointer. Do not process the buffer as a successful new line then.
- `sizeof buffer` gives its capacity here because `buffer` is an actual array. For an allocated pointer or function parameter, pass the capacity separately.

For a buffer of five characters, input `asd\n` fits including its newline and terminator. Input `asdf\n` fills the four-character allowance, leaving the newline for a later read.

## 9.8 `getline`: reading a dynamically sized line

`getline` is **POSIX, not ISO C**. The slides use a Unix-like environment; support and build settings depend on the platform.

```c
#define _POSIX_C_SOURCE 200809L
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>

int main(void) {
    char *line = nullptr;
    size_t capacity = 0;
    ssize_t length;

    while ((length = getline(&line, &capacity, stdin)) != -1) {
        printf("Read %zd characters: %s", length, line);
    }

    free(line);
}
```

- `&line` has type `char **`: the function may assign or replace the caller's buffer pointer.
- `&capacity` lets it update the number of bytes allocated for that buffer.
- The return value counts characters read, including a newline if present, but excluding `'\0'`.
- **Capacity and string length are different.** The buffer may be larger than the current line requires.
- A blank line containing only `'\n'` is a successful read of length one.
- The buffer can be reused and resized across calls; free the final buffer once finished, including after the loop ends with an error or EOF.
- Free `line`, not `&line`. Token pointers returned into it are borrowed.
- `ssize_t` is signed so it can represent `-1`; `%zd` prints it in this POSIX environment.

## 9.9 `sscanf`: converting a string into values

```c
char const *text = "x=1234, y=5678.54344";
int x;
double y;

int assigned = sscanf(text, "x=%d, y=%lf", &x, &y);
if (assigned == 2) {
    printf("x=%d, y=%f\n", x, y);
} else {
    fprintf(stderr, "Unexpected input format\n");
}
```

- `sscanf` reads the existing string; it does not read from `stdin`.
- Pass addresses of output variables so the function can store converted values.
- The format describes the expected input structure; literal characters must match, with whitespace handled according to the conversion rules.
- Check that the number of assignments equals the number expected before using all outputs.
- Successful conversions can occur before a later conversion fails.
- Getting two assignments does not prove the entire string was consumed; trailing text may remain.

### 9.9.1 Common conversion formats

| Desired destination | Format for `sscanf` | Argument type |
| --- | --- | --- |
| Integer | `%d` | `int *` |
| Floating-point value stored in `float` | `%f` | `float *` |
| Floating-point value stored in `double` | `%lf` | `double *` |
| `size_t` value | `%zu` | `size_t *` |
| One character | `%c` | `char *` |

- For input conversion, `%f` and `%lf` require different destination types.
- This differs from `printf`, where a `float` argument is promoted to `double` and `%f` is used for both.
- For bounded string conversions, supply a field width that leaves room for `'\0'`, e.g., `%19s` for `char word[20]`.
- The slides also mention `strtol` for converting a single integer from a string.
- The course recommends reading a line and then converting it, rather than relying on direct `scanf` input.

## 9.10 The course's problem-solving workflow

1. **Understand the specification:** inputs, required output, constraints, ownership, and promises.
2. **Design test cases:** normal cases, empty/smallest cases, boundaries, and cases that challenge assumptions.
3. **Decompose the problem:** define helper functions and contracts for smaller tasks.
4. **Implement:** choose suitable loops, recursion, arrays, pointers, structs, and storage lifetimes.
5. **Debug:** compare actual behavior with the specification and revise the reasoning or implementation.

For recursive code, identify the base case, smaller input, and combination step. For loop code, identify the invariant, safe accesses, progress, and stopping condition. For allocated data, identify the owner and cleanup path.

...
...
...

# L8: Problem solving and recursive backtracking
Recursive data structures:
```c
typedef struct LinkedList{
struct Tree *tree;
struct LinkedList *tail;
} LinkedList;
typedef struct Tree {
int item;
LinkedList *sub_trees;
} Tree;
```


example:
given an integer n, print all possible permutations 1,...,n

e.g. n=3

base case: if array is entirely filled, and check if it is a permutation.

```c
#include <stdio.h>

bool is_valid_solution(int *arr, int N) {
    return false;
}

void print_soln(int *arr, int N) {
    for (int i=0; i<N, i++)

}

void permute_h(int *arr, int N, int i) {
    if (i==N) {
        //reached the end of the array
        // see if solution is valid
        // if so, we print it, if not, dont
        if (is_valid_solution(arr, N)) {
            print_soln(arr, N);
        }
    }
}

void permute(int *arr, int N) {
    permute_h(arr, N, 0);
}

int main() {
    // assume we read this as input
    int const N = 3;
    // assume this malloc succeeds
    int *arr = calloc(sizeof(int)*N); // makes it all zeroes

    //print all permutations
    permute(arr, N);
}
```

