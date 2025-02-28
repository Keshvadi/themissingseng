---
title: File Manipulation
parent: Basic Commands
nav_order: 22
layout: default
---

## File Manipulation

Efficient file manipulation is essential for working with files and directories within the Linux environment. This section covers fundamental commands for managing files in the Shell.

---

### `touch`

- **Description:** Creates an empty file or updates the _timestamp_ (last modified time) of an existing file.
- **Example Usage:**

  ```bash
  touch new_file.txt       # Creates a new empty file named 'new_file.txt'
  touch existing_file.txt  # Updates the timestamp of 'existing_file.txt' (without changing content)
  ```

  _Sample Output:_
  _(No output is printed to the console)_

  _Note:_ If `existing_file.txt` already exists, its modification time will be updated to the current time. If it doesn't exist, it will be created as an empty file.

---

### `nano`

- **Description:** A simple, terminal-based text editor. Good for quick edits.
- **Example Usage:**

  ```bash
  nano new_file.txt  # Opens 'new_file.txt' in Nano.  Creates it if it doesn't exist.
  ```

  _Note:_ Within Nano:

  - Type to enter text.
  - **Ctrl + O** (then Enter): Saves the file ("Write Out").
  - **Ctrl + X**: Exits Nano. If you haven't saved, it will prompt you.

  _Installation (if needed - usually pre-installed):_

  - Debian/Ubuntu: `sudo apt install nano`
  - CentOS/Fedora: `sudo yum install nano`

---

### `cat`

- **Description:** Displays the content of a file, or concatenates (joins) multiple files.
- **Example Usage:**

  ```bash
  cat file1.txt          # Displays the contents of 'file1.txt'
  cat file1.txt file2.txt # Displays the contents of file1.txt, then file2.txt, one after the other.
  ```

  _Sample Output (if `file1.txt` contains "Hello" and `file2.txt` contains "World"):_

  ```
  Hello
  World
  ```

---

### `echo`

- **Description:** Prints text or the value of variables to the terminal.
- **Example Usage:**

  ```bash
  echo "Hello, World!"   # Prints "Hello, World!"
  echo $USER             # Prints the current username
  echo $HOME             # Prints the path to your home directory
  echo $PATH             # Prints the list of directories where the shell looks for commands

  export MY_VAR="My Value"  # Sets a custom environment variable
  echo $MY_VAR            # Prints the value of MY_VAR ("My Value")
  ```

  _Sample Output (for `echo "Hello, World!"`):_

  ```
    Hello, World!
  ```

  _Note:_ `echo` is frequently used in shell scripts for displaying messages, debugging, and generating output.

---

### `>` (Output Redirection - Overwrite)

- **Description:** Redirects the output of a command to a file. _Overwrites_ the file if it already exists.
- **Example Usage:**

  ```bash
  echo "This is new content." > my_file.txt  # Creates 'my_file.txt' (or overwrites it) with the text.
  ls -l > file_list.txt                  # Saves the output of 'ls -l' to 'file_list.txt'
  ```

  _Sample Output:_
  _(No output on console. Check the contents of the file with cat)_

---

### `>>` (Output Redirection - Append)

- **Description** Redirects the output of a command to a file, adding to the end.
- **Example Usage:**
  ```bash
    echo "Adding more text." >> my_file.txt
  ```

---

### `<` (Input Redirection)

- **Description:** Redirects the _input_ of a command to come from a file, instead of from the keyboard.
- **Example Usage:**

  ```bash
  cat < my_file.txt  # Equivalent to 'cat my_file.txt'.  The '<' is often optional for simple cases.
  ```

  _Note:_ Input redirection is most useful in more complex scenarios, like shell scripting, where you might want to feed a file's content line-by-line to a loop:

  ```bash
  while read line; do
      echo "Line: $line"
  done < my_file.txt  # Reads each line of 'my_file.txt' into the 'line' variable.
  ```

---

### `cp`

- **Description:** Copies files or directories.
- **Example Usage:**

  ```bash
  cp file1.txt file2.txt       # Creates a copy of 'file1.txt' named 'file2.txt'
  cp file1.txt my_folder/      # Copies 'file1.txt' into the 'my_folder' directory
  cp -r dir1/ dir2/           # Recursively copies 'dir1' (and all its contents) to 'dir2'
  ```

  _Sample Output:_
  _(No output is printed to the console if the command is successful)_
  _Note:_ The `-r` option is _required_ for copying directories.

---

### `mv`

- **Description:** Moves or renames files or directories.
- **Example Usage:**

  ```bash
  mv file1.txt new_name.txt  # Renames 'file1.txt' to 'new_name.txt'
  mv file1.txt my_folder/   # Moves 'file1.txt' into the 'my_folder' directory
  mv dir1/ dir2/            # Moves 'dir1' *into* 'dir2' (dir1 becomes a subdirectory of dir2)
  ```

  _Sample Output:_
  _(No output is printed to the console if the command is successful)_

---

### `rm`

- **Description:** _Removes_ (deletes) files or directories. **Use with caution!**
- **Example Usage:**

  ```bash
  rm file1.txt         # Deletes 'file1.txt'
  rm -r my_folder/     # Recursively deletes 'my_folder' and *all its contents*!
  rm -f file1.txt     #forcefully deletes file1.txt
  ```

  _Sample Output:_
  _(No output is printed to the console if the command is successful)_

  _Important Notes:_

  - `rm` is permanent. There is no "trash" or "recycle bin" by default on the command line.
  - `rm -r` is extremely powerful and dangerous. Double-check your command before pressing Enter!
  - `-f` option means to forcefully remove the file. It will not ask for any confirmation.

---

### `head`

- **Description:** Displays the first few lines of a file (10 lines by default).
- **Example Usage:**

  ```bash
  head my_file.txt      # Shows the first 10 lines
  head -n 5 my_file.txt  # Shows the first 5 lines
  ```

---

### `tail`

- **Description:** Displays the last few lines of a file (10 lines by default).
- **Example Usage:**

      ```bash
      tail my_file.txt      # Shows the last 10 lines
      tail -n 5 my_file.txt  # Shows the last 5 lines
      tail -f logfile.txt # Continuously display new lines added to the file, usefull for viewing logs.
      ```

  _Note:_ The `-f` option is very useful for monitoring log files in real-time.

---

### `less`

- **Description:** A powerful file viewer that allows you to scroll up and down, search, and more.
- **Example Usage:**

  ```bash
  less my_file.txt  # Opens 'my_file.txt' in the 'less' pager
  ```

  _Key Commands within `less`:_

  - **Spacebar:** Page down.
  - **b:** Page up.
  - **Arrow keys:** Scroll up/down/left/right.
  - **/pattern:** Search for "pattern" (press Enter to search, 'n' for next match).
  - **q:** Quit.
  - **h:** help

  _Note:_ `less` is generally preferred over `more` because it's more feature-rich (e.g., it allows scrolling _up_, while `more` only allows scrolling down).

---
