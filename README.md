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
   - [Examples](#examples)


## Section 1: Basic Program Structure, Directives, Linking, Compiling

### **1. Basic C Program Structure**

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


### Section 2: Printing Strings and Format Specifiers

#### **Using `printf` to Print Strings**

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

#### **Format Specifiers**

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

#### **Common Format Flags**

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

