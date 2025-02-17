# C Programming Basics 

The content is inspired from the amazing book: [`C Programming - A Modern Approach by K.N. King`](https://archive.org/details/c-programming-a-modern-approach-2nd-ed-c-89-c-99-king-by/mode/2up). I have tried to add as many code examples as possible to illustrate the concepts. I have also tried giving reference tables. I provide concise bullet points to convey the ideas.

I have also tried to cover some niche syntax that is not covered in most tutorials. My belief is that after reading this summarized introduction to C, you will have a good understanding of the language and might know a thing or two that many beginners don't know. 

# Table of Contents

1. [Section 1: Basic Program Structure, Directives, Linking, Compiling](#section-1-basic-program-structure-directives-linking-compiling)
   - [Basic C Program Structure](#1-basic-c-program-structure)
   - [Directives](#2-directives)
   - [Header Files](#3-header-files)
   - [Compiling and Linking](#4-compiling-and-linking)
   - [The main Function](#5-the-main-function)
2. [Section 2: Printing Strings and Format Specifiers](#section-2-printing-strings-and-format-specifiers)
   - [Using `printf` to Print Strings](#using-printf-to-print-strings)
   - [Format Specifiers](#format-specifiers)
   - [Common Format Flags](#common-format-flags)
3. [Section 3: Variables](#section-3-variables)
   - [Declaration and Initialization](#declaration-and-initialization)
   - [Data Types in C](#data-types-in-c)
   - [Examples: Using Variables](#examples-using-variables)
   - [Type Conversion in C](#type-conversion-in-c)
   - [Type Definitions](#type-definitions)
4. [Section 4: Operators](#section-4-operators)
   - [Types of Operators](#types-of-operators)
   - [Arithmetic Operators](#arithmetic-operators)
   - [Side Effects and the Assignment Operator](#side-effects-and-the-assignment-operator)
   - [Compound Assignments and Increment/Decrement Operators](#compound-assignments-and-incrementdecrement-operators)
   - [Relational, Equality, and Logical Operators](#relational-equality-and-logical-operators)
5. [Section 5: Conditional Statements](#section-5-conditional-statements)
   - [If, Else Syntax](#if-else-syntax)
   - [The Dangling Else Problem](#the-dangling-else-problem)
   - [Ternary Operator](#ternary-operator)
   - [Switch Statement](#switch-statement)
6. [Section 6: Loops](#section-6-loops)
   - [While Loops](#while-loops)
   - [For Loops](#for-loops)
   - [Break and Continue Statements](#break-and-continue-statements)
7. [Section 7: One-Dimensional Arrays](#section-7-one-dimensional-arrays)
   - [Declaration and Initialization](#71-declaration-and-initialization)
   - [Array Access and Indexing](#72-array-access-and-indexing)
   - [Using `sizeof()` with Arrays](#73-using-sizeof-with-arrays)
   - [Pitfalls: Out of Bounds Access](#74-pitfalls-out-of-bounds-access)
8. [Section 8: Two-Dimensional Arrays](#section-8-two-dimensional-arrays)
    - [Declaration and Initialization](#81-declaration-and-initialization)
    - [Accessing Elements](#82-accessing-elements)
    - [Example Printing and Manipulating 2D Arrays](#example-program-tic-tac-toe-board)
9. [Section 9: Functions](#functions-in-c)
    - [`main()` Function](#the-main-function)
    - [Function Declaration and Definition](#function-declaration-and-definition)
    - [Function Calling and Return Values](#calling-functions-and-return-values)
    - [Function Prototypes](#function-prototypes)
10. [Section 10: Pointers](#section-9-pointers)
    - [Understanding Memory](#understanding-memory)
    - [Pointer Variables](#pointer-variables)
    - [Declaring Pointers](#declaring-pointers)
    - [Dereferencing Pointers](#dereferencing-pointers)
    - [Common Confusions and Best Practices](#common-confusions-and-best-practices)
10. [Section 11: Pointers with Arrays](#section-11-pointers-with-arrays)  
    - [Understanding Pointers and Arrays](#understanding-pointers-and-arrays)  
    - [Pointer Arithmetic](#pointer-arithmetic)  
    - [Pointers for Array Processing](#pointers-for-array-processing)  
    - [Real-World Example: Using Pointers with Arrays](#real-world-example-using-pointers-with-arrays)  
11. [Example Program: Interactive Tic Tac Toe](#tic-tac-toe-example-with-pointers-functions-variables-and-arrays)
   

## Section 1: Basic Program Structure, Directives, Linking, Compiling

### **1. Basic C Program Structure**

Some of this maybe tricky to understand first. This section is meant to give a first expsoure to the concepts so atleast you are aware then you will master them as you practice more.

Every C program follows a standard structure. Here's a simple example:

```c
#include <stdio.h>  // Preprocessor Directive

int main() {        // "main" Function (must be named main)
    printf("Hello, World!\n");  // Statement
    return 0;       // Return Statement
}
```

**Components:**
- **Preprocessor Directives:** Lines starting with `#`, e.g., `#include <stdio.h>` 
    - here `#inlude` is a preprocessor directive 
    - `stdio.h` is a header file. It's enclosed in <> because it's a global header file. If you want to include a header file from your project, you will enclose it in "".
- **Main Function:** Entry point of the program, `int main()`. 
- **Statements:** Instructions executed by the program, e.g., `printf`
- **Return Statement:** Ends the `main` function, e.g., `return 0;`

**Note:** `printf` is imported from the standard input/output library `stdio.h`. It's used to print text to the console.

---

### **2. Directives**

Directives instruct the compiler to perform specific actions before actual compilation.

- **`#include`**
  - **Purpose:** Includes header files.
  - **Example:** `#include <stdio.h>`

- **`#define`**
  - **Purpose:** Defines macros or constants.
  - **Example:** `#define PI 3.14`
  > **Note:** Macros are fragments of code defined with `#define` that are replaced by their values or expressions before compilation. We will cover these later.

- **`#ifdef`, `#ifndef`, `#endif`**
  - **Purpose:** Conditional compilation, commonly used for header guards.
  - **Example:**
    ```c
    #ifndef MYHEADER_H
    #define MYHEADER_H
    // code
    #endif 
    ```
    **Purpose:**
    - Prevents multiple inclusion of the same header file
    - Without guards, if file A.h includes B.h, and C.h also includes B.h, then B.h would be included twice
    - Multiple inclusions could cause compilation errors (duplicate definitions)

    How it works:
    1. The `#ifndef MYHEADER_H` line:
        - Checks if `MYHEADER_H` is NOT defined

    2. The `#define MYHEADER_H` line:
        - Defines the macro `MYHEADER_H`
        - Only executes if the check above passed

    3. The content between guards

    4. The `#endif` line ends the guard
        
---

### **3. Header Files**

Header files contain declarations of functions and macros to be shared between several source files.

- **Standard Headers:** Provided by the standard library.
  - **Examples:** `stdio.h`, `stdlib.h`, `math.h`

- **Custom Headers:** Created by the programmer.
    - Example: `myheader.h`

**Including Headers:**
- **Angle Brackets (`< >`):** For standard headers.
  - `#include <stdio.h>`
- **Quotes (`" "`):** For custom headers.
  - `#include "myheader.h"`

---

### **4. Compiling and Linking**

**Compilation Steps:**

1. **Preprocessing:** Handles directives like `#include` and `#define`.
2. **Compilation:** Converts preprocessed code to assembly.
3. **Assembly:** Translates assembly code to machine code, generating an object file (`.o` or `.obj`).
4. **Linking:** Combines object files and libraries to create an executable.

**Commands:**

- **Compile to Object File:**
  ```bash
  gcc -c program.c -o program.o
  ```

- **Link Object Files to Executable:**
  ```bash
  gcc program.o -o program.exe
  ```

- TODO: Add later

| Aspect             | Object File (`.o` / `.obj`)             | Executable File (`.exe` / no extension) |
|--------------------|-----------------------------------------|------------------------------------------|
| **Contains**       | Machine code, but not fully linked      | Fully linked machine code ready to run   |
| **Usage**          | Intermediate step in compilation        | Final output that can be executed        |

---

### **5. The `main` Function**

The `main` function is the entry point of every C program.

**Structure:**
```c
int main() {
    // Code
    return 0;
}
```

**Return Value:**
- **`int`:** Indicates the program's return value (exit status).
  - `0`: Success
  - Non-zero: Error codes

**Variants:**
- **With Parameters:**
  ```c
  int main(int argc, char *argv[]) {
      // argc: Argument count
      // argv: Argument vector (array of strings)
      return 0;
  }
  ```
- **Using `void`:** (Less common)
  ```c
  void main() {
      // Code
  }
  ```
  *Note: Using `int main()` is standard and recommended.*


## Section 2: Printing Strings and Format Specifiers

### **Using `printf` to Print Strings**

- **`printf` Function:**
  - **Purpose:** Outputs formatted text to the console. 
  > Note: `printf` stands for "print formatted". You must include the `<stdio.h>` header file to use it since it comes from the standard input/output library.
  - **Basic Syntax:**
    ```c
    printf("format string", arguments);
    ```
  - **Basic Example:**
    ```c
    #include <stdio.h>

    int main() {
        string name = "Alice";
        printf("Hello, %s!\n", name);
        return 0;
    }
    ```
  - **Output:**
    ```
    Hello, Alice!
    ```

> **Note:** The `printf` function can take multiple arguments and format specifiers covered below. 

- **String Literals:**
  - Enclosed in double quotes (`" "`).
  - Include escape sequences like `\n` for newline.

### **Format Specifiers**

- **Purpose:** Define what kind of data is being printed and how it should be formatted.
- **List of some Specifiers:**

| Specifier | Description | Example Usage | Output |
|-----------|-------------|---------------|---------|
| `%s` | String | `printf("%s", "John");` | `"John"` |
| `%d` | Signed decimal integer | `printf("%d %d", 42, -42);` | `"42 -42"` |
| `%u` | Unsigned decimal integer | `printf("%u %u", 42, -42);` | `"42 4294967254"` |
| `%f` | Floating-point number | `printf("%.2f", 3.14159);` | `"3.14"` |
| `%c` | Single character | `printf("%c", 'A');` | `"A"` |
| `%p` | Pointer address | `printf("%p", ptr);` | `"0x7fff5fbff7e8"` |
| `%x` | Hexadecimal (lowercase) | `printf("%x", 255);` | `"ff"` |
| `%X` | Hexadecimal (uppercase) | `printf("%X", 255);` | `"FF"` |
| `%%` | Literal % character | `printf("Score: 100%%");` | `"Score: 100%"` |
| `%b` | Binary (C23, lowercase) | `printf("%b", 26);` | `"11010"` |
| `%e` | Scientific notation (lowercase) | `printf("%e", 123.456);` | `"1.234560e+02"` |
| `%g` | Shorter of %e or %f | `printf("%g", 123.456);` | `"123.456"` |
| `%i` | Signed decimal integer (auto-detects base) | `printf("%i %i %i", 100, 0x64, 0144);` | `"100 100 100"` |
| `%o` | Octal | `printf("%o", 64);` | `"100"` |
| `%lf` | Double | `printf("%lf", 3.14159);` | `"3.141590"` |
| `%Lf` | Long double | `printf("%Lf", 3.14159L);` | `"3.141590"` |

Some notable features about these specifiers:

- When given -42, `%u` interprets it as an unsigned value (4294967254 on a 32-bit system), while %d shows it as -42.
- `%i` automatically detects the base of the number (decimal, hexadecimal, or octal).
- Format specifiers can include width and precision modifiers (e.g., `%.2f` for 2 decimal places)
- Length modifiers like `l` (long), `ll` (long long), `h` (short) can be added to many specifiers
- The `%g` specifier automatically chooses between `%e` and `%f` based on the value's magnitude
- For floating-point values, uppercase specifiers (`%E`, `%G`) will output uppercase `E` in scientific notation

### **Common Format Flags**

- **Purpose:** Modify the output format of `printf` specifiers.
- **Flags and Their Effects:**

| Flag | Description | Example Usage | Output |
|------|-------------|---------------|---------|
| `+`  | Force sign for numbers | `printf("%+d", 42);` | `"+42"` |
| `0`  | Pad with leading zeros | `printf("%05d", 123);` | `"00123"` |
| `#`  | Alternate form | `printf("%#.3f", 23.2);` | `"23.200"` |
| `.`  | Precision control | `printf("%.2f", 3.14159);` | `"3.14"` |
| `-`  | Left-justify within field width | `printf("%-10s World!", "Hello");` | "Hello&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;World!" |

Note that:

The `#` flag adds prefixes to make number format explicit:
- For hex: adds "0x" prefix
- For octal: adds "0" prefix
- For floating point: forces decimal point
```c
// Without # flag
printf("%x", 255);    // Output: ff
printf("%o", 64);     // Output: 100

// With # flag
printf("%#x", 255);   // Output: 0xff
printf("%#o", 64);    // Output: 0100
```

## Section 3: Variables

### **Declaration and Initialization**

In C programming, **variables** are used to store data that your program can manipulate. Proper **declaration** and **initialization** of variables are crucial to ensure your program behaves as expected.

- **Declaration:**
  - **Syntax:** `<type> <variable_name>;`
  - **Purpose:** Tells the compiler to allocate memory for the variable. for example, an int variable takes 4 bytes of memory, char takes 1 and so on.
  - **Example:**
    ```c
    int age;
    // multiple declarations
    int a, b, c;
    float price, discount, total;
    bool isValid, isDone;
    ```
  
- **Initialization:**
  - **Syntax:** `<type> <variable_name> = <value>;`
  - **Purpose:** Assigns an initial value to the variable at the time of declaration.
  - **Example:**
    ```c
    int age = 25;
    float price = 19.99f; // add an f to indicate float for the compiler
    char grade = 'A';
    // multiple initializations
    int a = 10, b = 20, c = 30;
    ```

**Why Initialization Matters:**

- **Undefined Values:**
  - Declaring a variable without initializing it leaves the variable with an **undefined value**.
  - Accessing or using an uninitialized variable can lead to **unpredictable behavior** or **bugs**.
  
- **Memory Perspective:**
  - When a variable is declared, the compiler reserves a specific amount of memory based on its type.
  - Without initialization, the memory location contains **garbage data** (undefined values from memory).

  > **Warning ⚠️**: C will still execute your code even if you don't initialize variables, the result of that will be unpredictable and can lead to bugs that are hard to find. See the example below
  
- **Best Practices:**
  - **Always initialize** variables with a value before use. 
  - **Declare variables at the beginning** of a block to enhance code readability and maintainability.
  
**Example showcasing Bad Initialization Practice:**

Imagine you forget to initialize a value to `age` in the following example, then the if condition will use whatever garbage/unexpected value is stored in the memory location reserved for `age` and will result in unpredictable behavior (sometimes the if condition will be true, sometimes false).

```C
#include <stdio.h>

int main() {
    int age;            // Uninitialized variable ⚠️bad practice⚠️
    int bonus = 1000;   // Initialized variable
    
    // Let's pretend we forgot to assign a value to age
    if (age > 0) {     // Using uninitialized variable!
        bonus = bonus * 2; //double the bonus
    }
    
    printf("Employee bonus: $%d\n", bonus); // Output: Employee bonus: $1000 or $2000 or error
}
```

### **Data Types in C**

A **data type** specifies the type of data that a variable can hold. 

> In C there are 2 kinds of numeric types: `signed` and `unsigned`. 
> Signed integers can represent both positive and negative numbers, using one bit to indicate the sign (positive or negative). 
Unsigned integers represent only non-negative numbers, allowing a larger range of positive values since all bits are used for the magnitude.

| Data Type     | Description                                  | Example Declaration       | Memory Size (Typical)     | Value Range                      |
|---------------|----------------------------------------------|---------------------------|---------------------------|-----------------------------------|
| `int`         | integers (whole numbers)              | `int count = 10, temp = -2;` | 4 bytes                  | -2,147,483,648 to 2,147,483,647  |
| `float`       | floating-point numbers (approx. 6-7 decimal digits of precision) | `float temperature = 23.5f;` | 4 bytes                  | ±1.2E-38 to ±3.4E+38            |
| `double`      | floating-point numbers (approx. 15 decimal digits of precision) | `double price = 19.99;`   | 8 bytes                  | ±2.3E-308 to ±1.7E+308          |
| `char`        | single characters                      | `char grade = 'A';`       | 1 byte                   | 0 to 255 (or -128 to 127, signed)|
| `unsigned int`| non-negative integers                  | `unsigned int score = 100;` | 4 bytes                  | 0 to 4,294,967,295              |
| `long`        | larger integers                        | `long distance = 123456L;` | 8 bytes                  | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| `short`       | smaller integers                       | `short age = 25;`         | 2 bytes                  | -32,768 to 32,767               |
| `bool`        | boolean values (`true` or `false`)     | `bool isValid = true;`    | 1 byte                   | `true` or `false`               |


>**Note:** To use the `bool` type, include the header `<stdbool.h>`

> **Tip:** You can use `sizeof(<variable_name or constant name>)` to get the size of a variable in bytes. For example, `printf("%u", sizeof(23431241)"` will return 4 because an integer takes 4 bytes of memory.

### **Examples: Using Variables**

Let's explore how different variable types can be declared, initialized, and used in simple arithmetic operations and printed using `printf`.

```c
#include <stdio.h>
#include <stdbool.h> // Required for bool type

int main() {
    int apples = 10;
    float pricePerApple = 0.50f; // add an f to indicate float for the compiler
    double totalCost = -1; 

    char grade = 'A';
    unsigned int stock = 500; // we may use unsigned int because stock can't be negative, this is just a design choice however
    long population = 7800000000L;
    short temperature_celsius = 25; // be clear about the unit of your data when possible
    bool isOpen = true;

    // Simple Arithmetic
    totalCost = apples * pricePerApple;

    // Printing Variables
    printf("Apples: %d\n", apples); // use the %d format specifier for int
    printf("Price per Apple: $%.2f\n", pricePerApple); // price should be displayed with 2 decimal places so use %.2f
    printf("Total Cost: $%.2f\n", totalCost); // total cost can be a large number so use the 'l' flag 
    printf("Grade: %c\n", grade); 
    printf("Stock Available: %u units\n", stock); // use format specifier %u for unsigned int
    printf("World Population: %ld\n", population); // population is a large number so use 'l' flag with %d
    printf("Temperature: %+hd°C\n", temperature_celsius); // use %hd for short int and + flag to show positive temperature as it matters
    printf("Store Open: %s\n", isOpen ? "Yes" : "No"); // ternary operator ==> if isOpen is true print 'Yes' else print 'No'
    return 0;
}
```

**Output:**
```
Apples: 10
Price per Apple: $0.50
Total Cost: $5.00
Grade: A
Stock Available: 500 units
World Population: 7800000000
Temperature: +25°C
Store Open: Yes
```

> Note: for `totalCost` we intialized a sentinal value of -1 to indicate that the value is not yet calculated. If execution reaches the print statement without updating the -1 value, it will be clear that the value is not calculated. We won't see some random garbage value and be confused. You must decide what a sentinal value should be based on your program requirements.

### Type Conversion in C

Type Conversion is the process of converting a value from one data type to another. This can happen implicitly (automatically by the compiler) or explicitly (manually by the programmer). 

#### Implicit Type Conversion

Implicit type conversion, also known as **type coercion**, occurs automatically when the compiler converts a *narrower* data type to a *broader* data type to allow operations between different types. This is done to prevent data loss and ensure compatibility. For example:

- **int to float**: When an integer (narrows) is used in an expression with a float (broader), the integer is automatically converted to a float.
  ```c
  int a = 5;
  float b = 2.5;
  float result = a + b; // 'a' is implicitly converted to float so result is now float not int
  ```

- **short to int**: When a `short` (narrows) is used in an expression with an `int` (narrows), the `short` is promoted to an `int`.
  ```c
  short x = 10;
  int y = 20;
  int result = x + y; // 'x' is implicitly converted to int
  ```

#### Explicit Type Conversion

Explicit type conversion, also known as **type casting**, is when the programmer manually converts a value from one type to another. This is done using the cast operator `(type)`. For example:

- **float to int**: Converting a float to an integer truncates the decimal part.
  ```c
  float a = 3.14;
  int b = (int)a; // Explicitly convert 'a' to int
  ```

- **int to char**: Converting an integer to a char truncates the value to fit within the range of a char.
  ```c
  int a = 65;
  char b = (char)a; // Explicitly convert 'a' to char
  ```

- **unsigned to signed**: Converting an unsigned integer to a signed integer can lead to unexpected results if the value is too large.
```c
unsigned int x = 4294967295; // Maximum value for unsigned int
int y = (int)x; // y will be -1 due to overflow
printf("%d", y); // Output: -1
```

Explicit type conversion gives the programmer control over how data is interpreted, but it should be used carefully to avoid data loss or unexpected behavior.


### Type Definitions

The `typedef` keyword in C is used to create aliases for existing data types. This can make code more readable and easier to maintain, especially when dealing with complex data types or when the underlying type might change in the future.

#### Example of Typedef

Consider the following example where we define a new type `Dollars` as an alias for `float`:

```c
typedef float Dollars;
Dollars buy_cost, sell_cost;
```

In this example, `Dollars` is treated as a synonym for `float` by the compiler. This means that `buy_cost` and `sell_cost` are essentially `float` variables, but using the `Dollars` type makes the code more intuitive and self-documenting.

#### Benefits of Typedef

- **Improved Readability**: By using meaningful type names like `Dollars`, the code becomes easier to understand.
- **Ease of Maintenance**: If you later decide that all dollar-related variables should be of type `double` instead of `float`, you only need to change the `typedef` definition:
  ```c
  typedef double Dollars;
  ```
  This change will automatically update all variables of type `Dollars` throughout your code, reducing the risk of errors and saving time.

> ✅ We will study `struct` and `enum` soon, typedef is often used with them in practice


## Section 4: Operators

Operators  allow you to perform operations on variables and values. Understanding some non-obvious behaviors and best practices can help you write more bug free code.

### **Types of Operators**

1. **Arithmetic Operators:** Perform mathematical calculations.
2. **Relational Operators:** Compare two values.
3. **Logical Operators:** Combine multiple conditions.
4. **Assignment Operators:** Assign values to variables.
5. **Increment and Decrement Operators:** Increase or decrease a variable's value.

---

#### **Arithmetic Operators**

Arithmetic operators are used to perform mathematical operations such as addition, subtraction, multiplication, division, and modulus.

- **Common Arithmetic Operators:**

  | Operator | Description               | Example        |
  |----------|---------------------------|----------------|
  | `+`      | Addition                  | `a + b`        |
  | `-`      | Subtraction               | `a - b`        |
  | `*`      | Multiplication            | `a * b`        |
  | `/`      | Division                  | `a / b`        |
  | `%`      | Modulus (remainder)       | `a % b`        |

- **Important Notes:**
  
  - **Mixing `int` and `float`:**
    - When performing operations between `int` and `float`, the `int` is implicitly converted to `float`, and the result is a `float`.
    - **Example:**
      ```c
      int i = 70.99f;   // i will store 70 (fractional part truncated)
      float j = 132;    // j will store 132.0
      ```
  
  - **Division Operator `/`:**
    - **Integer Division:** If both operands are integers, the division truncates the fractional part.
      ```c
      int result = 1 / 2; // result is 0 not 0.5
      ```
    - **Floating-Point Division:** If at least one operand is a `float`, the division retains the fractional part.
      ```c
      float result = 1 / 2.0f; // result is 0.5
      ```
  
  - **Modulus Operator `%`:**
    - **Usage:** Only applicable to integer operands.
    - **Compilation Error:** Using `%` with non-integer types results in a compilation error.
      ```c
      int remainder = 5 % 2; // valid, remainder is 1
      float invalid = 5.0f % 2; // error, since % is not defined for float
      ```
  
  - **Division or Modulus by Zero:**
    - **Undefined Behavior:** Dividing or taking modulus by zero leads to undefined behavior.
    - **Modern Compilers:** Often throw a floating-point exception.
      ```c
      int division = 10 / 0; // Undefined, runtime error
      ```
  
  - **Operator Precedence:**
    - Determines the order in which operations are performed.
    - **Example:** Multiplication and division have higher precedence than addition and subtraction.
      ```c
      int result = 3 + 4 * 2; // result is 11, not 14 because it's equivalent to 3 + (4 * 2)
      ```
    - **Best Practice:** Use parentheses to explicitly define the desired order.
      ```c
      int result = (3 + 4) * 2; // result is 14
      ```

---

#### **Side Effects and the Assignment Operator**

The assignment operator (`=`) assigns the value on its right to the variable on its left. However, assignments can have side effects, especially when used within expressions.

- **Example of Side Effects:**
  ```c
  int j;
  int i = 1;
  int k = 1 + (j = i);
  printf("%d %d %d\n", i, j, k); // Outputs: 1 1 2
  ```
  
  **Explanation:**
  - The expression `(j = i)` assigns the value of `i` to `j` and returns the assigned value (`1`).
  - Therefore, `k` becomes `1 + 1`, which is `2`.
  
- **Why It's Bad Practice:**
  - **Readability:** Embedded assignments can make the code harder to read and understand.
  
- **Lvalue:**
  - Assignment Operator in C requires an Lvalue on the left. Lvalue refers to an object that occupies identifiable memory locations so they can not be a constant or expression.
  - **Example:**
    ```c
    int a = 5;   // 'a' is an lvalue
    5 = a;        // Error: 5 is not an lvalue
    ```
  
---

#### **Compound Assignments and Increment/Decrement Operators**

- **Compound Assignment Operators:**
  - Combine an arithmetic operation with assignment.
  - **Common Operators:**
    - `+=`, `-=`, `*=`, `/=`, `%=` 
  - **Example:**
    ```c
    int count = 10;
    count += 5; // Equates to count = count + 5; // count is now 15
    ```
  
- **Increment (`++`) and Decrement (`--`) Operators:**
  - **Purpose:** Increase or decrease a variable's value by one.
  - **Types:**
    - **Prefix:** `++variable` or `--variable`
      - Increments/decrements the value before it's used in the expression.
      - **Example:**
        ```c
        int a = 5;
        int b = ++a; // a becomes 6, then b is assigned 6
        ```
    - **Postfix:** `variable++` or `variable--`
      - Increments/decrements the value after it's used in the expression.
      - **Example:**
        ```c
        int a = 5;
        int b = a++; // b is assigned 5, then a becomes 6
        ```
  
  - **Side Effect:**
    - **Prefix:** Useful when the updated value is needed immediately.
    - **Postfix:** Useful when the original value is needed before updating.
  
  - **Example Showcasing Difference:**
    ```c
    #include <stdio.h>
    
    int main() {
        int x = 5;
        printf("Prefix: %d\n", ++x); // Outputs: 6 because x is incremented BEFORE use
        x = 5;
        printf("Postfix: %d\n", x++); // Outputs: 5 because x is incremented AFTER use
        printf("After Postfix: %d\n", x); // Outputs: 6
        return 0;
    }
    ```
  
---

#### **Relational, Equality, and Logical Operators**

- **Relational Operators:** Compare two values and determine the relationship between them.

  | Operator | Description               | Example        |
  |----------|---------------------------|----------------|
  | `>`      | Greater than              | `a > b`        |
  | `<`      | Less than                 | `a < b`        |
  | `>=`     | Greater than or equal to  | `a >= b`       |
  | `<=`     | Less than or equal to     | `a <= b`       |

- **Equality Operators:** Check if values are equal or not.

  | Operator | Description     | Example        |
  |----------|-----------------|----------------|
  | `==`     | Equal to        | `a == b`       |
  | `!=`     | Not equal to    | `a != b`       |

- **Logical Operators:** Combine multiple conditions.

  | Operator | Description                                 | Example              |
  |----------|---------------------------------------------|----------------------|
  | `&&`     | Logical AND (both conditions must be true)  | `a > 0 && b > 0`     |
  | `\|\|`    | Logical OR (at least one condition true)    | `a > 0 \|\| b > 0`   |
  | `!`      | Logical NOT (inverts the condition)         | `!a`                 |

- **Short-Circuit Evaluation:**
  - Logical operators evaluate expressions from left to right and stop as soon as the result is determined.
  - **Example:**
    ```c
    int a = 0;
    if (a != 0 && (10 / a) > 1) {
        // This block will not execute, and (10 / a) is not evaluated,
        // preventing a division by zero error.
    }
    ```

## Section 5: Conditional Statements

Conditional statements control the flow of a program based on certain conditions. In C, the primary conditional statements are `if`, `else`, the ternary operator, and `switch`.

### If, Else Syntax

- **`if` Statement**
  - **Purpose:** Execute code block if a condition is true.
  - **Syntax:**
    ```c
    if (condition) {
        // code to execute if condition is true
    }
    ```
  - **Example: Check Voting Eligibility**
    ```c
    int age = 20;
    if (age >= 18) {
        printf("Eligible to vote.\n");
    }
    ```

- **`if-else` Statement**
  - **Purpose:** Execute one block if condition is true, otherwise execute the "else" block.
  - **Syntax:**
    ```c
    if (condition) {
        // code if true
    } else {
        // code if false
    }
    ```
  - **Example: Voting Eligibility with Else**
    ```c
    int age = 16;
    if (age >= 18) {
        printf("Eligible to vote.\n");
    } else {
        printf("Not eligible to vote.\n");
    }
    ```

### The Dangling Else Problem

- **Issue:** In nested `if` statements without braces, `else` binds to the nearest `if`, which might not be the intended one.
- **C Rule:** `else` always associates with the closest preceding `if` not already associated.
- **Example of Dangling Else:**
  ```c
    int x = 2;
    if (x > 0)
      if (x > 5)
          printf("x is greater than 5\n");
    else
        printf("x is non-positive\n"); // Else binds to inner if
  ```

  ```
  Output: x is non-positive
  ```
  - **Misinterpretation:** Indentation suggests `else` belongs to the outer `if`, but it binds to the inner `if`. So even tho x = 2 which is 
  greater than 0 we still end up printing x is non-positive because the inner if condition returned false and the associated else block was executed.

- **Solution:** Use braces to clearly define intended blocks.
  ```c
  int x = 2;
  if (x > 0) {
      if (x > 5) {
          printf("x is greater than 5\n");
      }
  } else {
      printf("x is non-positive\n"); // Else now binds to outer if
  }
  ```
  ```
  Output: 
  ```
  In this case nothing will be outputted beacuse the else block is associated with outer if which executed successfully. Meanwhile, the inner if condition returned false and had no else block associated with it so nothing was printed.

### Switch Statement
As you can see above, nested if statements with lots of braces can be hard to read and follow. The switch statement is a better alternative in such cases.
- **Purpose:** Choose between multiple possible execution paths based on a single variable's value.
- **Syntax:**
  ```c
  switch (expression) {
      case value1:
          // code block
          break;
      case value2:
          // code block
          break;
      // ...
      default:
          // default code block
  }
  ```
- **Advantages:** Preferred over cascaded `if-else` for multiple discrete cases.
- **`break`:** Exits the `switch` statement. (see more below)

> **Warning ⚠️** Missing `break` leads to execution of subsequent cases unintentionally.

- **Example: Simple Calculator Operation**
  ```c
  char operator = '+';
  int num1 = 8, num2 = 5, result;

  switch (operator) {
      case '+':
          result = num1 + num2;
          break;
      case '-':
          result = num1 - num2;
          break;
      case '*':
          result = num1 * num2;
          break;
      case '/':
          result = num1 / num2;
          break;
      default:
          printf("Invalid operator.\n");
  }
  printf("Result: %d\n", result);
  ```
  ```
  Output: Result: 13
  ```

- **`switch` Statement Components**

| Component | Description |
|-----------|-------------|
| `switch(expression)` | Evaluates the expression once and compares it with each `case`. |
| `case value:` | Defines a block of code to execute if `expression` matches `value`. |
| `break;` | Exits the `switch` after executing a `case`. Prevents fall-through. |
| `default:` | Optional. Executes if no `case` matches the `expression`. |

### Ternary Operator

- Short-hand for simple `if-else` statements.
- **Syntax:**
  ```c
  condition ? expression_if_true : expression_if_false;
  ```
- **Use Case:** Assign value based on a condition.
- **Example: Determine Max of Two Numbers**
  ```c
  int a = 5, b = 10;
  printf("Maximum is %d\n", (a > b) ? a : b);
  ```
  ```
  Output: Maximum is 10
  ```

- **Usecase Example 2:** Assign discount based on customer type.
  ```c
  char customerType = 'R'; // 'R' for regular, 'P' for premium
  float discount = (customerType == 'R') ? 0.05 : 0.10; // give 5% discount for regular customers and 10% for premium
  printf("Discount: %.2f%%\n", discount * 100);
  ```
  ```
  Output: Discount: 5.00%
  ```

## Section 6: Loops

Loops allow you to execute a block of code multiple times based on a condition. In C, the primary loop constructs are `while`, `for`, and loop control statements like `break` and `continue`.

> Note: We omit the `do-while` loop since it's less common and `goto` due to the criticisms and potential misuse.

### While Loops

- **Execution Order:**
  1. **Condition Check:** Evaluates the loop condition *before* each iteration. (**Note:** If the condition is false before the loop executes, the loop body will not execute even once).
  2. **Code Execution:** Executes the loop body if the condition is true.
  3. **Condition Check:** Check condition again after each iteration.

- **Note:** `do-while` loops exist but are rarely used so we will focus on `while` and `for` loops.

**Syntax**

```c
while (condition) {
    // code to execute
}
```

**Common Pitfalls**

- **Infinite Loops:**
  - Occur when the loop condition never becomes false.
  - **Example:**
    ```c
    while (1) {
        printf("This loop runs forever.\n");
    }
    ```
  - **Expected Output:**
    ```
    This loop runs forever.
    This loop runs forever.
    This loop runs forever.
    ...
    ```

- **Intentional Infinite Loops:**
  - Used in scenarios like event-driven programs or servers that run continuously until manually stopped.
  - **Exiting the Loop:** Utilize `break` statements within conditional blocks to exit.
  - **Example:**
    ```c
    #include <stdio.h>

    int main() {
        int number;

        while (1) {
            printf("Enter a positive number (negative to exit): ");
            scanf("%d", &number);

            if (number < 0) {
                printf("Exiting loop.\n");
                break;
            }

            printf("You entered: %d\n", number);
        }

        return 0;
    }
    ```

  - **Expected Output:**
    ```
    Enter a positive number (negative to exit): 10
    You entered: 10
    Enter a positive number (negative to exit): 5
    You entered: 5
    Enter a positive number (negative to exit): -1
    Exiting loop.
    ```

**Example: Simple Calculator**

**Description:** Continuously takes user input for two numbers and an operator, performs the calculation, and displays the result. The loop continues until the user decides to exit.

```c
#include <stdio.h>
#include <stdbool.h>

int main() {
    char operator = '\0';
    double num1 = 0.0, num2 = 0.0;
    bool continueCalc = true;

    while (continueCalc) {
        printf("Enter operator (+, -, *, /) or 'q' to quit: ");
        scanf(" %c", &operator); // pass a space before %c to consume the newline character \n from the previous input

        if (operator == 'q') {
            break; // exit the loop if 'q' is entered
        }

        printf("Enter two operands: ");
        scanf("%lf %lf", &num1, &num2);

        switch (operator) {
            case '+':
                printf("Result: %.2lf + %.2lf = %.2lf\n", num1, num2, num1 + num2);
                break;
            case '-':
                printf("Result: %.2lf - %.2lf = %.2lf\n", num1, num2, num1 - num2);
                break;
            case '*':
                printf("Result: %.2lf * %.2lf = %.2lf\n", num1, num2, num1 * num2);
                break;
            case '/':
                if (num2 != 0) // if-else inside the switch can be used to prevent division by zero
                    printf("Result: %.2lf / %.2lf = %.2lf\n", num1, num2, num1 / num2);
                else
                    printf("Error: Division by zero.\n");
                break;
            default:
                printf("'%c' is an Invalid operator\n", operator);
        }
    }

    printf("Calculator exited.\n");
    return 0;
}
```
**Note**: We needed to add a space before %c in `scanf(" %c", &operator);` because the newline character \n is inserted automatically when the user presses Enter after entering the operands. Without the space, scanf will read the newline character as the operator in the next iteration and we will hit the default case of the switch statement.

Also Note that we didn't need a space in `scanf("%lf %lf", &num1, &num2);` because the %f specifier automatically skips whitespace characters until it finds its target data type.

**Expected Output:**
```
Enter operator (+, -, *, /) or 'q' to quit: +
Enter two operands: 5 3
Result: 5.00 + 3.00 = 8.00
Enter operator (+, -, *, /) or 'q' to quit: /
Enter two operands: 10 2
Result: 10.00 / 2.00 = 5.00
Enter operator (+, -, *, /) or 'q' to quit: q
Calculator exited.
```

### For Loops

- Ideal for scenarios involving a known number of iterations, such as iterating through arrays or counting occurrences.

**Syntax**

```c
for (initialization; condition; increment) {
    // code to execute
}
```

**C-specific Considerations**

- **Before C99:** Loop counter must be declared before the loop.
  ```c
  int i;
  for (i = 0; i < 10; i++) {
      // code
  }
  ```
- **C99 and Later:** Allows declaring the loop counter within the loop.
  ```c
  for (int i = 0; i < 10; i++) {
      // code
  }
  ```
- **Scope:** Variables declared within the `for` loop are not accessible outside the loop. So if you need to use the loop counter outside the loop, declare it before the loop like the old way.

**Workflow**

1. **Initialization:** Sets the starting point (e.g., `int i = 0`).
2. **Condition Check:** Evaluates the loop condition before each iteration (e.g., `i < 10`).
3. **Loop Body Execution:** Executes the code block if the condition is true.
4. **Increment/Decrement:** Updates the loop counter (e.g., `i++`).

**Example**

Print numbers from 1 to 5.

```c
#include <stdio.h>

int main() {
    for (int i = 1; i <= 5; i++) {
        printf("Number: %d\n", i);
    }
    return 0;
}
```

**Expected Output:**
```
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```


### Break and Continue Statements

**Break Statement**

- Immediately exits the innermost enclosing loop (`while`, `for`) or `switch` statement. 
- Only exits the nearest loop, not all enclosing loops.

**Example: Exit Loop When Number is Found**

```c
#include <stdio.h>

int main() {
    int numbers[] = {3, 7, 2, 9, 5};
    int target = 9;
    int found = 0;

    for (int i = 0; i < 5; i++) {
        if (numbers[i] == target) {
            printf("Number %d found at index %d.\n", target, i);
            found = 1;
            break;
        }
    }

    if (!found) {
        printf("Number %d not found.\n", target);
    }

    return 0;
}
```

**Expected Output:**
```
Number 9 found at index 3.
```

Note that if `break` is used in a nested loop, only the inner loop is exited. The outer loop will continue executing.

### Continue Statement

- Skips the remaining code in the current loop iteration and proceeds to the next iteration.
- **Effect in Nested Loops:** Only affects the current loop level.

**Example: Skip Even Numbers**

```c
#include <stdio.h>

int main() {
    printf("Odd numbers between 1 and 5:\n");
    for (int i = 1; i <= 5; i++) {
        if (i % 2 == 0) {
            continue; // Skip printing even numbers
        }
        printf("%d\n", i);
    }
    return 0;
}
```

**Expected Output:**
```
Odd numbers between 1 and 5:
1
3
5
```

**Contrast with Break Statement:**

```c
#include <stdio.h>

int main() {
    printf("Numbers until 3:\n");
    for (int i = 1; i <= 5; i++) {
        if (i == 3) {
            break; // Exit loop when i is 3
        }
        printf("%d\n", i);
    }
    return 0;
}
```

**Expected Output:**
```
Numbers until 3:
1
2
```
As you can see, the loop stops when `i` is 3 and does not print 4 and 5.


## Section 7: One-Dimensional Arrays

Arrays allow you to store multiple values of the same type in a single, contiguous block of memory. 

### 7.1 Declaration and Initialization

- **Syntax:**
  ```c
  type arrayName[arraySize];
  ```
- **Components:**
  - `type`: Data type of the array elements (e.g., `int`, `char`, `float`).
  - `arrayName`: Identifier for the array.
  - `arraySize`: Fixed integer constant representing the number of elements.

- **Best Practice:** Define a macro for array size to enhance readability 
  ```c
  #define ARRAY_SIZE 10
  int numbers[ARRAY_SIZE];
  ```

#### Initialization

- **Syntax:**
  ```c
  type arrayName[arraySize] = {value1, value2, ..., valueN};
  ```
- **Rules:**
  - If fewer initializers are provided than the array size, the remaining elements are automatically initialized to zero.
  - Example: Initializing all elements to zero or using boolean values.

- **Examples:**
  ```c
  int arr[5] = {1, 2, 3};       // arr = {1, 2, 3, 0, 0}
  int zeros[10] = {0};          // All elements set to 0
  int bools[10] = {false};     // All elements set to 0 (false)
  char letters[4] = {'a', 'b', 'c'}; // letters = {'a', 'b', 'c', '\0'}
  ```

#### Example: Student Grades Tracker

**Description:** Track the grades of 5 students. Initialize the array with some grades and set the rest to zero.

```c
#include <stdio.h>
#define NUM_STUDENTS 5

int main() {
    int grades[NUM_STUDENTS] = {85, 90}; // Initialize first two grades
    printf("Student Grades:\n");
    for (int i = 0; i < NUM_STUDENTS; i++) {
        printf("Student %d: %d\n", i + 1, grades[i]);
    }
    return 0;
}
```

**Expected Output:**
```
Student Grades:
Student 1: 85
Student 2: 90
Student 3: 0
Student 4: 0
Student 5: 0
```

### 7.2 Array Access and Indexing

#### Accessing Elements

- **Syntax:**
  ```c
  arrayName[index]
  ```
- **Index Range:** `0` to `arraySize - 1`
- **Example:**
  ```c
  int numbers[5] = {10, 20, 30, 40, 50};
  printf("First number: %d\n", numbers[0]); // Outputs 10
  printf("Last number: %d\n", numbers[4]);  // Outputs 50
  ```

#### Array Indexing Syntax

- Understand that the bracket notation for accessing an array element is syntactic sugar. Accessing `array[i]` is equivalent to dereferencing at index 0 + desired index. `*(array + i)` ==> in this example, `array` is the memory address of the first element.

Below is an example to illustrate 3 different ways to access the same element in an array.
- **Dereferencing Example:**
  ```c
    int arr[3] = {5, 10, 15};
    
    //syntax: using name which by default points to first element
    printf("%d \n", *(arr + 1));
    
    //syntax: using explicit pointer
    int *ptr = &arr[0]; //explicitely define pointer to first element
    printf("%d\n", *(ptr + 1)); // add pointer + 1 and dereference
    
    //syntax: syntactic sugar bracket notation provided by C 
    printf("%d\n", arr[1]);   
  ```

#### Example: Temperature Recorder

Record temperature for 7 days and then find the average temperature.

```c
#include <stdio.h>
#define NUM_DAYS 7

int main() {
  float temps[NUM_DAYS] = {0.0} // Initialize all elements to 0

  //take input for each day
  for (int i = 0; i < NUM_DAYS; i++) {
    printf("Enter temperature for day %d: ", i + 1); // remember i starts from 0 but day starts from 1 thus i + 1
    scanf("%f", &temps[i]); // to store the input into the array, we must pass the address of the element using &temps[i]
  }

  //average calculation
  float sum = 0.0;
  for (int i = 0; i < NUM_DAYS; i++) {
    sum += temps[i];
  }

  float average = sum / NUM_DAYS;
  printf("Average Temperature: %.2f°C\n", average); // remember to use %.2f to display 2 decimal places

}
```

**Expected Output:**
```
Enter temperature for day 1: 25
Enter temperature for day 2: 30
Enter temperature for day 3: 45
Enter temperature for day 4: 22
Enter temperature for day 5: 28
Enter temperature for day 6: 33
Enter temperature for day 7: 10
Average Temperature: 27.57°C
```

### 7.3 Using `sizeof()` with Arrays

Can be used to find the length of an array at compile time. Remember `sizeof()` returns the size in bytes so to get the number of elements in an array, divide the total size of the array by the size of a single element. 

- **Formula:**
  ```c
  int length = sizeof(array) / sizeof(array[0]);
  ```

```c
#include <stdio.h>

int main() {
    int arr[10] = {0};
    int length = sizeof(arr) / sizeof(arr[0]);
    printf("Array length: %d\n", length);
    return 0;
}
```

**Expected Output:**
```
Array length: 10
```

### Table: Using `sizeof()` with Different Data Types

| Data Type | Example Array             | `sizeof(array)` | `sizeof(array[0])` | Calculated Length |
|-----------|---------------------------|------------------|--------------------|-------------------|
| `int`     | `int nums[5];`            | 20 bytes         | 4 bytes            | 5                 |
| `char`    | `char letters[10];`       | 10 bytes         | 1 byte             | 10                |
| `float`   | `float temps[3];`         | 12 bytes         | 4 bytes            | 3                 |


### 7.4 Pitfalls: Out of Bounds Access

#### Security Risks

- **Buffer Overflows:** Writing beyond the allocated memory can corrupt data, cause crashes, or create security vulnerabilities.
- **Memory Exploits:** Attackers can exploit out-of-bounds access to execute arbitrary code.

#### Importance of Bounds Checking

- **Always validate indices** to ensure they are within the valid range (`0` to `arraySize - 1`).
- **Example:** Preventing invalid user input from accessing array elements.

#### Example: Safe Array Access

```c
#include <stdio.h>
#define SIZE 5

int main() {
    int numbers[SIZE] = {10, 20, 30, 40, 50};
    int index;

    printf("Enter an index (0-4): ");
    scanf("%d", &index);

    if (index >= 0 && index < SIZE) { // Check if index is within bounds
        printf("Value at index %d: %d\n", index, numbers[index]);
    } else {
        printf("Error: Index out of bounds.\n");
    }

    return 0;
}
```

**Expected Output:**
```
Enter an index (0-4): 2
Value at index 2: 30
```
*Or, if out of bounds:*
```
Enter an index (0-4): 5
Error: Index out of bounds.
```

> Note: Remember if you access out of bounds memory, C will not stop you and output whatever's is at that memory location.

## Section 8: Two Dimensional Arrays  
There are many usecases of 2D arrays. We will briefly introduce the structure of 2D arrays and how to access elements.  

### 8.1 Declaration and Initialization  
A 2D array is declared with the syntax:  

```c
data_type array_name[rows][columns];
```  

Initialization can be done in several ways:  
```c
// Fully specified initialization
int grid[2][3] = {{1, 2, 3}, {4, 5, 6}};

// Partial initialization (remaining elements set to 0)
int grid2[][3] = {{7}, {8, 9}}; // Row count inferred as 2
```  

> **Note**: The column size *must* be specified, while the row size can be inferred during initialization.  

### 8.2 Accessing Elements  
Elements are accessed using row and column indices: 

```c
int value = grid[1][2]; // Accesses 2nd row, 3rd column (value = 6)
```  

Use nested loops to traverse all elements:  
```c
for (int i = 0; i < 2; i++) {
    for (int j = 0; j < 3; j++) {
        printf("%d ", grid[i][j]);
    }
    printf("\n");
}
```  

### Example Program: Tic-Tac-Toe Board

```c
#include <stdio.h>

#define ROWS 3
#define COLS 3

int main() {
    // Initialize a 3x3 matrix representing a Tic-Tac-Toe board
    char board[ROWS][COLS] = {
        {'X', 'O', 'X'},
        {'O', 'X', 'O'},
        {' ', ' ', 'X'}
    };

    printf("Tic-Tac-Toe Board:\n");

    // Loop through each row 
    for (int i = 0; i < ROWS; i++) {
        // Loop through each column in the current row
        for (int j = 0; j < COLS; j++) {
            printf(" %c ", board[i][j]); // Print the cell value
            // Separator between columns except for the last column
            if (j < COLS - 1) {
                printf("|"); 
            }
        }
        printf("\n"); // Newline after each row

        // Print a horizontal line after each row except the last
        if (i < ROWS - 1) {
            printf("---|---|---\n");
        }
    }

    // Example of accessing and modifying an element
    // Suppose you detected that Player marks 'O' at position (row = 2, column = 0)
    board[2][0] = 'O';
    printf("\nAfter Player 'O' makes a move at (3,1):\n");

    // Display the updated board (in section 9 we will learn functions to avoid repetition)
    printf("Tic-Tac-Toe Board:\n");
    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            printf(" %c ", board[i][j]);
            if (j < COLS - 1) {
                printf("|");
            }
        }
        printf("\n");
        if (i < ROWS - 1) {
            printf("---|---|---\n");
        }
    }

    return 0;
}
```

**Expected Output:**
```
Tic-Tac-Toe Board:
 X | O | X 
---|---|---
 O | X | O 
---|---|---
   |   | X 

After Player 'O' makes a move at (3,1):
Tic-Tac-Toe Board:
 X | O | X 
---|---|---
 O | X | O 
---|---|---
 O |   | X 
```

## Functions in C

Functions are the building blocks of C programs. They allow you to break your code into reusable, modular pieces. 


### The `main()` Function
We have been using this function since the beginning of this tutorial. 

  - `main()` is a special function in C. It is the entry point of every C program.
  - When you execute a C program, the operating system calls the `main()` function to start the program.
  - It must have the exact name `main` and a specific return type (`int`).

**How does `main()` work?**
  - `main()` resides in the program's stack memory when executed.
  - It can take two optional parameters: `argc` (argument count) and `argv` (argument vector), which are used for command-line arguments. Though often not written explicitly.
  - It returns an integer value to the operating system, indicating the program's status. `0` indicates successful execution, while a non-zero value indicates an error.

### Function Declaration and Definition

- **Syntax of a Function:**
  ```c
  return_type function_name(parameter1_type parameter1, parameter2_type parameter2, ...) {
      // declarations
      // statements
      return value; // mandatory for non-void functions
  }
  ```

- **Key Points:**
  - **Return Type:** Specifies the type of value the function returns. Use `void` if the function doesn’t return anything.
  - **Function Name:** Must be unique and follow C’s naming rules.
  - **Parameters:** Optional. Specify the data type and name of each parameter.
  - **Function Body:** Contains the code to be executed.


> Note: Functions cannot return arrays directly but can return pointers to arrays declared outside their scope.


### Calling Functions and Return Values

- **How to Call a Function?**
  - Use the function name followed by parentheses `()` and pass arguments if required.
  - Example: `int sum = add(10, 20);`

- **Ignoring Return Values:**
  - You can call a function and ignore its return value.
  - Example: `add(5, 10);` (The result is not stored or used.)

### Function Prototypes

- **What are Function Prototypes?**
  - A function prototype is a declaration of a function that specifies its name, return type, and parameters.
  - It allows you to declare the function (without defining it) before the function is called. You can then define the function after it is called.

- **Why Use Prototypes?**
  - They are essential in header. files which we will cover later.
  - They help the compiler understand the function’s signature before it is used. Otherwise, the compiler does an implicit declaration however if the function later has an issue, the compiler will throw an error which can be hard to debug due to the flow of the program.

- **Example:**
```C
  #include <stdio.h>

  // Function declarations (function prototypes) 
  float calculateArea(float radius);
  float calculatePerimeter(float radius);

  int main() {
      float radius = 5.0;
      float area = calculateArea(radius); // function call
      float perimeter = calculatePerimeter(radius);

      printf("Circle with radius %.2f:\n", radius);
      printf("Area: %.2f\n", area);
      printf("Perimeter: %.2f\n", perimeter);

      return 0;
  }

  // Function definitions
  float calculateArea(float radius) {
      return 3.14159 * radius * radius;
  }

  float calculatePerimeter(float radius) {
      return 2 * 3.14159 * radius;
  }
```


**Output:**
```
  Circle with radius 5.00:
  Area: 78.54
  Perimeter: 31.42
```

# Section 10: Pointers

Pointers differentiate C from other high-level languages. They provide direct access to memory addresses, trusting the programmer to manage and optimize the memory usage. Java, Python, JavaScript, and other languages abstract memory management, making them easier to use but less efficient.

### Understanding Memory

- **Memory Structure:**
  - **Byte:** The smallest addressable unit in memory, consisting of 8 bits.
    - **32-bit:** Addresses range from `0` to `4,294,967,295` (2³² - 1).
    - **64-bit:** Addresses range from `0` to `18,446,744,073,709,551,615` (2⁶⁴ - 1) 
> **Fun Tidbit:** No supercomputer has yet required more than 64-bit addressable memory. Even Frontier, the world's largest supercomputer, has only 9200 TB RAM, which falls well within 64-bit addressing capabilities. A 64-bit architecture can theoretically address up to 16 million TB of memory.

- **Memory Addressing:**
  - Each byte in memory has a unique address.
  - Addresses are typically represented in hexadecimal format.

- **Pointers in C:**
  - **Usage:** Allow direct access to memory addresses and manipulation of data within those individual memory locations.
  - **Advantage:** Offers fine-grained control for performance optimizations, unlike languages like Java or Python where compilers handle pointer arithmetic.

### Pointer Variables

**What Are Pointers?**

- Variables that store the memory address of other variables, structs *(to be covered later)*, arrays, etc.
- **Syntax**
  ```c
  int *ptr;
  ```
  - `ptr` is a pointer to an integer.

### Declaring and Initializing Pointers

- **Declaring Pointers**
  ```c
  type *pointerName;
  ```
  - `type`: Data type the pointer can point to.
  - `*`: Indicates that the variable is a pointer.

- **Examples:**
  ```c
  int *ptrInt;       // Pointer to an integer
  char *ptrChar;     // Pointer to a character
  float *ptrFloat;   // Pointer to a float
  ```

- **Initializing Pointers:**
  Use the address-of operator `&` to assign the memory address of a variable to a pointer.
  ```c
  int i = 10;
  int *p = &i; // Pointer p stores the memory address of i
  ```

**Visual Representation of Memory**

| Variable | Value | Memory Address |
|----------|-------|-----------------|
| `int i`  | `10`  | 0x7ffee3b2a9a**0**|
| `int *p` | `0x7ffee3b2a9a0` | 0x7ffee3b2a9a**8**|

*In this table, the pointer `p` stores the memory address of the integer variable `i`.*
> Note: The actual value stored in `int *p` is the memory address of `i`. The value `10` is stored in `i`. We can access this value stored in `i` using the pointer `p` as we will cover in dereferencing.

#### Example: Pointer to an Integer

```c
#include <stdio.h>

int main() {
    int i = 42;     // Integer variable
    int *p = &i;    // Pointer variable storing address of i

    return 0;
}
```

### Dereferencing Pointers

- Accessing or modifying the value stored at the memory address a pointer points to.
- **Syntax:**
  ```c
  *pointerName;
  ```

#### Example: Dereferencing a Pointer

```c
#include <stdio.h>

int main() {
    int num = 25;
    int *p = &num; // Pointer p points to num

    printf("Value of num: %d\n", num);
    printf("p stores the address: %p\n", (void*)p); // use %p to print memory address, use void* to cast the pointer to a void pointer
    printf("p points to the value: %d\n", *p); // Dereferencing the pointer will return a int value thus use %d

    // Modifying the value using dereferencing
    *p = 30; //notice the *p is used to modify the value of num, only when initializing the pointer do we use int *p = &num
    printf("New value of num after modification: %d\n", num);

    return 0;
}
```

**Expected Output:**
```
Value of num: 25
p stores the address: 0x7ffee3b2a9a0
p points to the value: 25
New value of num after modification: 30
```

> #### Important Warning

- **Initialize Pointers:** Always initialize pointers before use to avoid undefined behavior.
  ```c
  int *ptr;       // Uninitialized pointer are dangerous
  int *ptr = NULL; // Initialized pointer (Safe)
  ```
- **Consequences of Uninitialized Pointers:**
  - May point to random memory locations.
  - Can lead to program crashes or security vulnerabilities.
  ```c
  int *ptr; // Uninitialized pointer
  *ptr = 50; // You are storing 50 at a random memory location which is undefined behavior and may cause a crash
  ```

### Common Confusions and Best Practices

#### Confusion with Asterisk `*`

- **Dual Use of `*`:**
  - **Declaration:** Indicates that a variable is a pointer.
    ```c
    int *ptr; // ptr is a pointer to an integer
    ```
  - **Dereferencing:** Accesses the value at the memory address the pointer points to.
    ```c
    int value = *ptr; // Retrieves the value pointed to by ptr
    ```

- **Clarifying the Context:**
  - **Declaration vs. Dereferencing:**
    - **Left Side of `=`:** Declaring a pointer.
    - **Right Side of `=`:** Dereferencing to get the value.

#### Best Practices

- **Always Initialize Pointers:**
  ```c
  int *ptr = NULL; // Safe initialization
  ```

- **Avoid Dereferencing NULL Pointers:**
  ```c
  if (ptr != NULL) {
      // Safe to dereference
  }
  ```

- **Use Meaningful Pointer Names:** Enhance code readability.
  ```c
  int *agePtr;    // Pointer to age variable
  char *namePtr;  // Pointer to name string
  ```

## Section 11: Pointers with Arrays

### Understanding Pointers and Arrays  
Using pointers with arrays is an essential concept in C programming. Since arrays and pointers are closely related, understanding their interaction helps in efficient memory management and code optimization.  

In C, the name of an array acts as a pointer to its first element. This means that if we have an array:

```c
#include <stdio.h>

int main() {
    int numbers[] = {10, 20, 30, 40, 50};
    int *ptr = numbers;  // Equivalent to traditional &numbers[0]

    printf("First element: %d\n", *ptr); //dereference the value at this location
    printf("First element: %d\n", numbers[0]);
    return 0;
}
```
**Output:**  
```
First element: 10
First element: 10
```
**Note:** Here, `ptr` is assigned `numbers`, which is the address of the first element in the array. Accessing `*ptr` gives `10`, the first element.
- Thus realize that `numbers` is equivalent to `&numbers[0]` as it gives address to the first element in array. 
- `*numbers` is equivalent to `numbers[0]` as it gives the value at the first element in the array.


### Pointer Arithmetic 
C supports three fundamental pointer arithmetic operations:

**1. Adding an Integer to a Pointer**  
When you add an integer `n` to a pointer, it moves forward by `n * sizeof(type)`.  where type is the data type of the pointer.

```c
#include <stdio.h>

int main() {
    int arr[] = {100, 200, 300, 400, 500};
    int *ptr = arr; //pointer to first element of arr (value at index 0  is 100 in arr)

    printf("Pointer address: %p, Value: %d\n", ptr, *ptr); //address = ptr, value at that address = *ptr
    ptr++;  // Moves to the next element
    printf("Pointer address: %p, Value: %d\n", ptr, *ptr);

    return 0;
}
```

**Output:**  
```
Pointer address: 0x12345678, Value: 100
Pointer address: 0x1234567C, Value: 200
```
The address increases by `sizeof(int)`, typically `4 bytes`. This means you don't have to worry about adding the correct bytes manually.

**2. Subtracting an Integer from a Pointer**  
Subtracting an integer `n` moves the pointer backward by `n * sizeof(type)`.

```c
#include <stdio.h>

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int *ptr = &arr[3]; //adress to 40 (element at index 3)

    printf("Pointer address: %p, Value: %d\n", ptr, *ptr);
    ptr--;  // Moves to the previous element
    printf("Pointer address: %p, Value: %d\n", ptr, *ptr);

    return 0;
}
```

**Output:**  
```
Pointer address: 0x12345684, Value: 40
Pointer address: 0x12345680, Value: 30
```
Again, it moves back by `sizeof(int)` bytes.

**3. Subtracting One Pointer from Another**  
You can subtract two pointers to determine the number of elements between them.

```c
#include <stdio.h>

int main() {
    int arr[] = {5, 10, 15, 20, 25, 30};
    int *ptr1 = &arr[1]; // Points to 10
    int *ptr2 = &arr[5]; // Points to 30

    printf("Difference: %d\n", ptr2 - ptr1);

    return 0;
}
```
**Output:**  
```
Difference: 4
```
The output shows that `ptr2` is 4 elements ahead of `ptr1`.

**Pointer Comparisons**  
Pointers can be compared using comparison operators:

```c
#include <stdio.h>

int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int *p1 = &arr[0];
    int *p2 = &arr[4];

    if (p1 < p2) {
        printf("p1 points to an earlier element than p2.\n");
    }
    return 0;
}
```
**Output:**  
```
p1 points to an earlier element than p2.
```
Pointers are compared based on their memory addresses.


### Pointers for Array Processing  

We can traverse an array using explicit pointer notation:

```c
#include <stdio.h>

int main() {
    int arr[] = {3, 6, 9, 12, 15};
    int *ptr = arr;

    for (int i = 0; i < 5; i++) {
        printf("%d ", *(ptr + i)); //add i = 1,2,3... to the pointer to access the next element and then dereference it
    }
    return 0;
}
```
**Output:**  
```
3 6 9 12 15
```
Here, `*(ptr + i)` accesses the ith element.

## **Real-World Example: Using Pointers with Arrays**  

Let’s implement a program that finds the maximum number in an array using pointer arithmetic.

```c
#include <stdio.h>

int findMax(int arr[], int size) { // int arr[] = int *arr = pointer to first element of array
    int max = arr[0];  // setting max to first element by default
    for (int i = 1; i < size; i++) {
        if (arr[i] > max) { // arr[i] is equivalent to *(arr + i)
            max = arr[i];
        }
    }
    return max;
}

int main() {
    int numbers[] = {23, 45, 67, 12, 89, 55};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    int max = findMax(numbers, size);
    printf("The maximum value in the array is: %d\n", max);

    return 0;
}
```

**Expected Output:**  
```
The maximum value in the array is: 89
```

## Tic Tac Toe Example with Pointers, Functions, Variables and Arrays
This is a complete self-contained program, try copying pasting this into an online free C compiler like [Programiz](https://www.programiz.com/c-programming/online-compiler/) to see it in action.

This can be improved in many ways, try improving it!

```c
// Online C compiler to run C program online
#include <stdio.h>
#include <stdbool.h>

#define ROWS 3
#define COLS 3

// Function to print the Tic-Tac-Toe grid
void gridPrinter(char board[ROWS][COLS]) {
    printf("Tic-Tac-Toe Board:\n");
    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            printf(" %c ", board[i][j]); // Print the cell value
            if (j < COLS - 1) {
                printf("|"); // Separator between columns except for the last column
            }
        }
        printf("\n");

        // Print a horizontal line after each row except the last
        if (i < ROWS - 1) {
            printf("---|---|---\n");
        }
    }
}

// Function to check if there is a winner
char checkWinner(char board[ROWS][COLS]) {
    // Check rows and columns
    for (int i = 0; i < ROWS; i++) {
        if (board[i][0] == board[i][1] && board[i][1] == board[i][2] && board[i][0] != ' ')
            return board[i][0]; // Row win
        if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != ' ')
            return board[0][i]; // Column win
    }

    // Check diagonals
    if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ')
        return board[0][0]; // Main diagonal
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0] && board[0][2] != ' ')
        return board[0][2]; // Secondary diagonal

    return ' '; // No winner yet
}

// Function to check if the board is full (draw)
bool isBoardFull(char board[ROWS][COLS]) {
    for (int i = 0; i < ROWS; i++) {
        for (int j = 0; j < COLS; j++) {
            if (board[i][j] == ' ')
                return false; // Found an empty space, not full
        }
    }
    return true;
}

int main() {
    // Initialize an empty 3x3 Tic-Tac-Toe board
    char board[ROWS][COLS] = {
        {' ', ' ', ' '},
        {' ', ' ', ' '},
        {' ', ' ', ' '}
    };

    bool gameState = true;
    char currentPlayer = 'X'; // X starts first
    int xCoord, yCoord;
    
    while (gameState) {
        // Print the current board
        gridPrinter(board);

        // Get user input
        printf("Player %c, enter your move (row and column: 0 0 to 2 2): ", currentPlayer);
        scanf("%d %d", &xCoord, &yCoord);

        // Validate move
        if (xCoord < 0 || xCoord >= ROWS || yCoord < 0 || yCoord >= COLS || board[xCoord][yCoord] != ' ') {
            printf("Invalid move out of range. Try again.\n");
            continue; // Ask for input again
        }

        // Place the move
        board[xCoord][yCoord] = currentPlayer;

        // Check for winner
        char winner = checkWinner(board);
        if (winner != ' ') {
            gridPrinter(board);
            printf("Player %c wins!\n", winner);
            gameState = false;
            break;
        }

        // Check for draw
        if (isBoardFull(board)) {
            gridPrinter(board);
            printf("It's a draw!\n");
            gameState = false;
            break;
        }

        // Switch player
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    return 0;
}
```

- Notice that `void gridPrinter(char board[ROWS][COLS])` we needed to define it like this because we are passing a 2D array and it needs column size to be defined, you can also define it as `void gridPrinter(char board[][COLS])` and it will work the same way since row can be left empty but column size is required.