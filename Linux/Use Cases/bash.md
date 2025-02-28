---
title: Bash Scripting
parent: Common Use Cases
nav_order: 43
layout: default
---

## Bash Scripting

Bash scripting allows you to automate tasks by writing sequences of commands in a file (a script) and then executing that file. This is incredibly powerful for repetitive tasks, system administration, and creating custom tools.

---

### Creating and Running a Bash Script

1.  **Create a new file:** Use a text editor (like `nano` or `vim`) to create a new file. It's common to use the `.sh` extension for shell scripts, but it's not strictly required.

    ```bash
    nano my_script.sh
    ```

2.  **Add the "shebang" line:** At the very top of the file, add the following line:

    ```bash
    #!/bin/bash
    ```

    This line (called the "shebang") tells the operating system which interpreter to use to execute the script (in this case, `bash`).

3.  **Write your script:** Add the commands you want to execute, one per line.

    ```bash
    #!/bin/bash
    echo "Hello, world!"
    echo "The current date is: $(date)"
    ```

4.  **Save the file:** In `nano`, press Ctrl+O, then Enter, then Ctrl+X.

5.  **Make the script executable:** Use the `chmod` command to give the script execute permissions:

    ```bash
    chmod +x my_script.sh
    ```

6.  **Run the script:** Execute the script using `./`:

    ```bash
    ./my_script.sh
    ```

    _Sample Output:_

    ```
    Hello, world!
    The current date is: Tue Oct 29 10:30:00 UTC 2024
    ```

---

### Variables

Variables store data (text or numbers) that you can use in your script.

- **Assigning Values:**

  ```bash
  my_variable="Hello"
  number=123
  ```

  _Note:_ There must be _no spaces_ around the `=` sign.

- **Accessing Values:** Use a `$` before the variable name:

  ```bash
  echo $my_variable
  echo "The number is: $number"
  ```

- **User Input:** Use the `read` command:

  ```bash
  #!/bin/bash
  echo "Enter your name:"
  read user_name
  echo "Hello, $user_name!"
  ```

---

### Comments

Comments are lines that are ignored by the interpreter. They are used to explain your code.

```bash
# This is a single-line comment

# This is another comment.
# This script displays a greeting.
echo "Hello"  # This comment is at the end of a line
```
