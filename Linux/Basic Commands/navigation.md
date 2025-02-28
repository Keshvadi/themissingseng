---
title: Navigation
parent: Basic Commands
nav_order: 21
layout: default
---

## Navigating The Shell

When connected to a Unix system via the shell, understanding how to navigate the file system is essential. This section covers fundamental commands for moving around and exploring directories.

_Note: The sample outputs below are examples. Your system's output may differ based on your files and directory structure._

---

### `pwd`

- **Description:** Prints the current working directory (the directory you are currently "in").
- **Example Usage:**

  ```bash
  pwd
  ```

  _Sample Output:_

  ```
  /home/user/projects
  ```

---

### `ls`

- **Description:** Lists the contents of a directory.
- **Example Usage:**

  ```bash
  ls           # Displays files and directories in the current directory
  ls -l        # Displays detailed information (permissions, owner, size, date)
  ls -a        # Displays all files, including hidden files (those starting with .)
  ls -la       # Combines -l and -a: detailed info, including hidden files
  ls -lt       # Sorts by modification time, newest first
  ```

  _Sample Output (for `ls`):_

  ```
  file1.txt  my_folder  another_file.pdf
  ```

---

### `man`

- **Description:** Displays the manual page (documentation) for a command. This is your best friend for learning about commands!
- **Example Usage:**

  ```bash
  man ls  # Shows the manual page for the 'ls' command
  ```

  _Important Note:_ On some systems (like Debian/Ubuntu), you might need to install the `man-db` package first:

  ```bash
  sudo apt install man-db  # Use this on Debian/Ubuntu if 'man' doesn't work
  ```

  (On other distributions, the package manager might be different, e.g., `yum` on CentOS/Fedora, or `pacman` on Arch.)

---

### `mkdir`

- **Description:** Creates a new directory.
- **Example Usage:**

  ```bash
  mkdir new_directory  # Creates a directory named 'new_directory'
  ```

  _Sample Output:_
  _(No output is printed to the console if the command is successful)_

---

### `cd`

- **Description:** Changes the current working directory.
- **Example Usage:**

  ```bash
  cd my_folder       # Moves into the 'my_folder' subdirectory
  cd ..             # Moves up one level (to the parent directory)
  cd ~/Documents     # Moves to the 'Documents' folder inside your home directory
  cd -              # Moves to the previously visited directory
  cd /              # Moves to the root directory of the file system
  ```

---

### Directory Symbols

These symbols are shortcuts for common directory locations:

- `.` : Represents the current directory.
- `..`: Represents the parent directory.
- `-` : Represents the previous directory.
- `~`: Represents your home directory (e.g., `/home/user`).
- `/`: Represents the root directory.

---

### Wildcards: `*` and `?`

Wildcards are special characters used to match multiple files or directories.

- **`*` (Asterisk):** Matches zero or more characters.

  - **Example Usage (with `ls`):**

    ```bash
    ls *.txt  # Lists all files ending with '.txt' (e.g., file1.txt, report.txt, notes.txt)
               # Will NOT match .txtfile (because * needs zero or more chars BEFORE .txt)
    ls docs/* # Lists all files and directories inside the 'docs' directory
    ```

- **`?` (Question Mark):** Matches exactly one character.

  - **Example Usage (with `ls`):**

    ```bash
    ls file?.txt  # Lists files like file1.txt, fileA.txt, file9.txt
                  # Will NOT match file10.txt (because ? matches only ONE character)
                  # or file.txt
    ```

---

### `tree`

- **Description:** Displays a tree-like diagram of a directory's structure. This command is often _not_ installed by default.
- **Installation (Debian/Ubuntu):**
  ```bash
  sudo apt install tree
  ```
  **(Installation for other distributions will vary)**
- **Installation (CentOS/Fedora):**

  ```bash
  sudo yum install tree
  ```

- **Example Usage:**

  ```bash
  tree        # Shows the tree structure of the current directory
  tree /home/user/projects # shows from the /home/user/projects directory
  tree -L 2  # Limits the display to 2 levels deep
  ```

  _Sample Output (truncated):_

  ```
  .
  ├── my_folder
  │   ├── file1.txt
  │   └── file2.txt
  └── another_folder
      └── notes.md

  2 directories, 3 files
  ```

---
