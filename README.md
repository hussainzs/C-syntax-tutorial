# C Programming Basics 

Just keep reading and things will start to make sense even if you don't understand everything at first.

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

