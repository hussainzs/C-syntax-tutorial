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
- **Common Specifiers:**

| Specifier | Description | Example Usage | Output |
|-----------|-------------|---------------|---------|
| `%s` | String | `printf("%s", "John");` | `"John"` |
| `%d` | Signed decimal integer | `printf("%d", 42);` | `"42"` |
| `%f` | Floating-point number | `printf("%.2f", 3.14159);` | `"3.14"` |
| `%c` | Single character | `printf("%c", 'A');` | `"A"` |
| `%x` | Hexadecimal (lowercase) | `printf("%x", 255);` | `"ff"` |
| `%X` | Hexadecimal (uppercase) | `printf("%X", 255);` | `"FF"` |
| `%%` | Literal % character | `printf("Score: 100%%");` | `"Score: 100%"` |

#### **Common Format Flags**

- **Purpose:** Modify the output format of `printf` specifiers.
- **Flags and Their Effects:**

| Flag | Description | Example Usage | Output |
|------|-------------|---------------|---------|
| `-`  | Left-justify within field width | `printf("%-10s", "Hello");` | `"Hello     "` |
| `+`  | Force sign for numbers | `printf("%+d", 42);` | `"+42"` |
| `0`  | Pad with leading zeros | `printf("%05d", 123);` | `"00123"` |
| ` `  | Space before positive numbers | `printf("% d % d", 5, -5);` | `" 5 -5"` |
| `#`  | Alternate form | `printf("%#x", 255);` | `"0xff"` |
| `.`  | Precision control | `printf("%.2f", 3.14159);` | `"3.14"` |

#### **Examples**

1. **Printing a String with Width and Alignment:**
    ```c
    #include <stdio.h>

    int main() {
        char name[] = "Alice";
        printf("Name: %-10s!\n", name); // Left-justified within 10 spaces
        return 0;
    }
    ```
    **Output:**
    ```
    Name: Alice     !
    ```

2. **Printing Numbers with Flags:**
    ```c
    #include <stdio.h>

    int main() {
        int num = 42;
        printf("Number with plus sign: %+d\n", num);
        printf("Number with leading zeros: %05d\n", num);
        return 0;
    }
    ```
    **Output:**
    ```
    Number with plus sign: +42
    Number with leading zeros: 00042
    ```

3. **Printing Hexadecimal with `#` Flag:**
    ```c
    #include <stdio.h>

    int main() {
        int value = 255;
        printf("Hexadecimal: %#x\n", value);
        return 0;
    }
    ```
    **Output:**
    ```
    Hexadecimal: 0xff
    ```

4. **Limiting String Length:**
    ```c
    #include <stdio.h>

    int main() {
        char str[] = "Hello, World!";
        printf("First 5 characters: %.5s\n", str);
        return 0;
    }
    ```
    **Output:**
    ```
    First 5 characters: Hello
    ```

5. **Printing a Literal `%` Character:**
    ```c
    #include <stdio.h>

    int main() {
        printf("Completion: 100%%\n");
        return 0;
    }
    ```
    **Output:**
    ```
    Completion: 100%
    ```

---

**Quick Reference Tables**

- **Format Specifiers:**

  | Specifier | Data Type                  | Example Usage                 |
  |-----------|----------------------------|-------------------------------|
  | `%s`      | String                     | `printf("Name: %s", name);`   |
  | `%d`      | Signed decimal integer     | `printf("Age: %d", age);`     |
  | `%f`      | Floating-point number      | `printf("Score: %.2f", score);` |
  | `%c`      | Single character           | `printf("Grade: %c", grade);` |
  | `%x`      | Hexadecimal (lowercase)    | `printf("Hex: %x", value);`   |
  | `%X`      | Hexadecimal (uppercase)    | `printf("Hex: %X", value);`   |
  | `%%`      | Literal `%` character      | `printf("100%% Complete");`    |

- **Format Flags:**

  | Flag | Description                                         | Usage Example                |
  |------|-----------------------------------------------------|------------------------------|
  | `-`  | Left-justify within the field width                 | `printf("%-10s", name);`     |
  | `+`  | Always show sign (`+` or `-`) for numeric types      | `printf("%+d", num);`         |
  | `0`  | Pad numeric output with leading zeros               | `printf("%05d", num);`        |
  | ` `  | Prefix positive numbers with a space                | `printf("% d", num);`         |
  | `#`  | Use alternate form (e.g., `0x` for hex)             | `printf("%#x", value);`       |
  | `.`  | Specify precision (decimal places or string length) | `printf("%.2f", score);`      |