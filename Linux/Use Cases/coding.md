---
title: Coding with the Shell
parent: Common Use Cases
nav_order: 42
layout: default
---

## Coding with the Shell

The command-line interface (shell) is a powerful and efficient environment for software development. It's commonly used for writing, compiling (for compiled languages like C++), and running code. This section provides basic examples for C++ and Python.

---

### C++

1.  **Create the Source Code:** Use a text editor (like `nano` or `vim`) to create a C++ source file (usually with a `.cpp` extension).

    ```bash
    nano hello.cpp  # Create a new file named hello.cpp
    ```

2.  **Write the Code:** Enter your C++ code into the file. Here's a simple "Hello, World!" example:

    ```c++
    #include <iostream>

    int main() {
        std::cout << "Hello, World!" << std::endl;
        return 0;
    }
    ```

    _Note:_ Using `using namespace std;` is generally discouraged in larger projects, as it can lead to naming conflicts. It's better to use `std::cout`, `std::endl`, etc. I've used the more explicit form here.

3.  **Save and Exit (Nano):** Press Ctrl+O, then Enter (to confirm the filename), then Ctrl+X.

4.  **Compile the Code:** Use the `g++` compiler to compile your code into an executable.

    ```bash
    g++ hello.cpp -o hello  # Compile hello.cpp and create an executable named 'hello'
    ```

    _Explanation:_

    - `g++`: The GNU C++ compiler.
    - `hello.cpp`: The source code file.
    - `-o hello`: The `-o` option specifies the name of the output file (the executable). If you omit `-o`, the default output file name is `a.out`.

    _Installation (if needed):_

    - Debian/Ubuntu: `sudo apt install g++`
    - CentOS/Fedora: `sudo yum install gcc-c++` / `sudo dnf install gcc-c++`

5.  **Run the Executable:**

    ```bash
    ./hello  # Execute the compiled program
    ```

    _Sample Output:_

    ```
    Hello, World!
    ```

---

### Python

1.  **Create the Source Code:** Use a text editor to create a Python source file (usually with a `.py` extension).

    ```bash
    nano hello.py  # Create a new file named hello.py
    ```

2.  **Write the Code:** Enter your Python code. Here's a "Hello, World!" example:

    ```python
    print("Hello, World!")
    ```

3.  **Save and Exit (Nano):** Press Ctrl+O, then Enter, then Ctrl+X.

4.  **Run the Script:** Use the `python3` interpreter to execute your script.

    ```bash
    python3 hello.py  # Run the Python script
    ```

    _Sample Output:_

    ```
    Hello, World!
    ```

    _Note:_ On many systems, `python` might refer to Python 2, which is outdated. It's best to use `python3` explicitly to ensure you're using Python 3.

    _Installation (if needed - usually pre-installed, but sometimes you need to install it explicitly):_

    - Debian/Ubuntu: `sudo apt install python3`
    - CentOS/Fedora: `sudo yum install python3` / `sudo dnf install python3`

---

### Other Languages

The general workflow for other languages is similar:

1.  **Write Code:** Use a text editor to create your source file.
2.  **Compile (if necessary):** Use the appropriate compiler for your language (e.g., `javac` for Java, `gcc` for C).
3.  **Run:** Execute the compiled program (or use the interpreter for interpreted languages like Ruby, Perl, etc.).

**Example (Java):**

```bash
# 1. Create HelloWorld.java (using nano, vim, etc.)
# public class HelloWorld {
#     public static void main(String[] args) {
#         System.out.println("Hello, World!");
#     }
# }

# 2. Compile:
javac HelloWorld.java  # Creates HelloWorld.class

# 3. Run:
java HelloWorld
```
