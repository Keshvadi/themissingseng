---
title: More Advanced Commands
parent: Advanced Commands
nav_order: 33
layout: default
---

## More Advanced Commands

This section covers a collection of powerful command-line utilities that go beyond basic file and user management. These commands are essential for text processing, searching, and system administration tasks.

---

### `history`

- **Description:** Displays a list of previously executed commands in your current terminal session. This is extremely useful for recalling commands you've used before, especially long or complex ones.
- **Example Usage:**

  ```bash
  history       # Show the command history
  history | less # Pipe the history to 'less' for easier scrolling (if the history is long)
  !5            # Re-execute command number 5 from the history
  !-1           # Re-execute the *last* command (very useful!)
  !ls           # Re-execute the last command that *started* with 'ls'
  history | grep 'command_name' # search history for a certain command.
  ```

  _Sample Output (truncated):_

  ```
  1  ls -l
  2  cd my_folder
  3  pwd
  4  nano file.txt
  5  cat file.txt
  ...
  ```

  _Note:_ The history is usually stored in `~/.bash_history`. The number of commands stored is controlled by the `HISTSIZE` environment variable.

---

### `grep` (Global Regular Expression Print)

- **Description:** Searches for lines matching a given pattern (regular expression) within files or standard input. `grep` is one of the most fundamental and frequently used text processing tools.
- **Example Usage:**

  ```bash
  grep "pattern" file.txt            # Search for "pattern" in 'file.txt' (case-sensitive)
  grep -i "pattern" file.txt         # Search case-insensitively
  grep -v "pattern" file.txt         # Show lines that *do not* match "pattern"
  grep -r "pattern" directory/       # Recursively search for "pattern" in all files within 'directory/'
  grep -w "word" file.txt            # Match only the whole word "word" (not substrings)
  grep -n "pattern" file.txt         # Show line numbers along with matching lines
  grep -c "pattern" file.txt         # Count the number of matching lines (not the number of matches *within* lines)
  grep -E "pattern1|pattern2" file.txt # Use extended regular expressions (ERE) - match either pattern1 OR pattern2
  ls -l | grep "^d"                 # List only directories (lines starting with 'd' in 'ls -l' output)
  grep "^[^#]" config.txt         # Show lines from config.txt that do *not* start with '#' (useful for viewing config files without comments)
  ```

  _Sample Output (for `grep "error" my_log.txt`):_

  ```
  2023-10-27 10:15:22 ERROR: Database connection failed.
  2023-10-27 10:20:35 ERROR: File not found.
  ```

  _Key Options:_

  - `-i`: Ignore case (case-insensitive search).
  - `-v`: Invert the match (show lines that _don't_ match).
  - `-r` (or `-R`): Recursive search (search through directories).
  - `-w`: Match whole words only.
  - `-n`: Show line numbers.
  - `-c`: Count matching lines.
  - `-E`: Use extended regular expressions (allows for more complex patterns, like `|` for "or").
  - `-l`: List only the _filenames_ that contain matches (useful when searching multiple files).
  - `^`: Matches the beginning of the line.
  - `$`: Matches the end of the line.
  - `[]`: define a set of charachters.

---

### `find`

- **Description:** A powerful command for searching for files and directories based on various criteria (name, type, size, modification time, etc.). `find` is essential for locating files on your system.
- **Example Usage:**

  ```bash
  find . -name "*.txt"                # Find all files ending in '.txt' in the current directory and subdirectories
  find /home -user johndoe -type f    # Find all files owned by user 'johndoe' in /home
  find /var/log -name "*.log" -mtime +7 # Find log files in /var/log that were modified more than 7 days ago
  find . -type f -size +10M            # Find files larger than 10 megabytes in the current directory
  find . -type f -empty                # Find empty files
  find . -type d -empty                # Find empty directories
  find . -name "*.txt" -exec ls -l {} \;  # Find .txt files and run 'ls -l' on each one
  find . -name "*.tmp" -delete        # Find and *delete* all files ending in '.tmp' (USE WITH CAUTION!)
  ```

  _Key Options:_

  - `.`: The starting directory for the search ( `.` means the current directory). You can use any path (e.g., `/`, `/home/user`, `/var/log`).
  - `-name "pattern"`: Search by filename (supports wildcards like `*` and `?`). Always put the pattern in quotes.
  - `-type f`: Search for files.
  - `-type d`: Search for directories.
  - `-user username`: Search for files owned by a specific user.
  - `-mtime n`: Search for files modified `n` days ago. `+n` means older than `n` days, `-n` means newer than `n` days.
  - `-size +n[kMG]`: Search for files larger than `n` kilobytes (k), megabytes (M), or gigabytes (G). `-size -n[kMG]` for smaller than.
  - `-empty`: Search for empty files or directories.
  - `-exec command {} \;`: Execute a command on each found file. `{}` is replaced by the filename. The `\;` is essential to terminate the command.
  - `-delete`: Delete the found files. _Extremely dangerous_ - double and triple-check before using!

---

### `sort`

- **Description:** Sorts lines of text alphabetically or numerically. Often used in pipelines with other commands.
- **Example Usage:**

  ```bash
  sort file.txt          # Sort lines alphabetically
  sort -r file.txt         # Sort in reverse alphabetical order
  sort -n numbers.txt     # Sort numerically
  sort -nr numbers.txt    # Sort numerically, in reverse order (largest to smallest)
  sort -k 2 file.txt      # Sort by the second field (assuming fields are separated by whitespace)
  sort -t ':' -k 3n /etc/passwd  # Sort /etc/passwd numerically by the 3rd field (user ID), using ':' as the field separator
  ls -l | sort -k 5rn   # as we saw before.
  ```

  _Key Options:_

  - `-r`: Reverse the sort order.
  - `-n`: Numerical sort.
  - `-k N`: Sort by the Nth field (column).
  - `-t CHAR`: Use CHAR as the field separator (default is whitespace).
  - `-u`: output only unique lines

---

### `shuf`

- **Description:** Randomly shuffles lines of text from a file or standard input. Useful for creating random samples, shuffling playlists, etc.
- **Example Usage:**

  ```bash
  shuf file.txt       # Shuffle the lines of 'file.txt' and print to standard output
  shuf -n 5 file.txt  # Output 5 randomly selected lines from 'file.txt'
  shuf -o output.txt file.txt  # Shuffle 'file.txt' and save the result to 'output.txt'
  seq 1 10 | shuf    # Generate numbers 1 to 10 and shuffle them
  ```

  _Key Options:_

  - `-n COUNT`: Output at most COUNT lines.
  - `-o FILE`: write result to FILE instead of standard output.

---

### `uniq`

- **Description:** Filters adjacent matching lines from _sorted_ input, showing only unique lines (or a count of occurrences). _Important:_ `uniq` only works on _adjacent_ duplicates, so you usually need to `sort` the input first.
- **Example Usage:**

  ```bash
  sort file.txt | uniq        # Show unique lines from 'file.txt' (after sorting)
  sort file.txt | uniq -c     # Show unique lines, *prefixed with the count of occurrences*
  sort file.txt | uniq -d     # Show only the *duplicate* lines (lines that appear more than once)
  sort file.txt | uniq -u      # show only the unique lines
  ```

  _Key Options:_

  - `-c`: Prefix lines by the number of occurrences.
  - `-d`: Only print duplicate lines, one for each group.
  - `-u`: Only print unique lines.

---

### `sed` (Stream EDitor)

- **Description:** A powerful, non-interactive text editor that performs transformations on a stream of text (from a file or standard input). `sed` is incredibly versatile and often used for search and replace, but it can do much more. It uses regular expressions extensively.
- **Example Usage:**

  ```bash
  sed 's/old/new/' file.txt         # Replace the *first* occurrence of "old" with "new" on each line
  sed 's/old/new/g' file.txt        # Replace *all* occurrences of "old" with "new" on each line (global replacement)
  sed 's/old/new/2' file.txt       # replace the second occurrence.
  sed '2d' file.txt                # Delete the 2nd line
  sed '$d' file.txt                # Delete the last line
  sed '/pattern/d' file.txt         # Delete all lines containing "pattern"
  sed '1,5d' file.txt              # Delete lines 1 through 5
  sed -n '/pattern/p' file.txt     # Print only lines matching "pattern" (similar to grep, but -n is needed)
  sed -i 's/old/new/g' file.txt    # Edit 'file.txt' *in place* (make the changes directly to the file) - BE CAREFUL!
  sed 's/^/prefix /' file.txt   # add "prefix" to the beginnig of each line.
  sed 's/$/ ---/' file.txt       # add "---" to the end of each line
  ```

  _Key Concepts and Options:_

  - `s/old/new/`: The substitution command. `s` stands for substitute. `old` is the pattern to search for (a regular expression), and `new` is the replacement.
  - `g`: Global replacement (replace all occurrences on a line, not just the first).
  - `d`: The delete command (deletes entire lines).
  - `ADDRESSd`: Apply the `d` command only to lines matching the ADDRESS (a line number, a range, or a regular expression).
  - `-n`: Suppress automatic printing of lines. Used with the `p` command to print only specific lines.
  - `-i`: Edit files in place. _This modifies the original file_, so use it with caution. It's a good idea to make a backup first (e.g., `sed -i.bak 's/old/new/g' file.txt` creates `file.txt.bak`).
  - `p`: print the current line.
  - `^`: (in regular expression). Matches the beginnig of the line.
  - `$`: (in regular expression). Matches the end of the line.

---

### `cut`

- **Description:** Extracts sections (fields) from each line of a file or standard input. Useful for working with delimited data (like CSV files).
- **Example Usage:**

  ```bash
  cut -d ',' -f 1 file.csv      # Extract the first field from each line, using ',' as the delimiter
  cut -d ':' -f 1,3 /etc/passwd # Extract the 1st and 3rd fields (username and user ID) from /etc/passwd
  cut -c 1-5 file.txt          # Extract characters 1 through 5 from each line
  ls -l | cut -d ' ' -f 1,5-9 # getting some fields from ls -l
  ```

  _Key Options:_

  - `-d DELIMITER`: Use DELIMITER as the field separator (default is tab).
  - `-f FIELD_LIST`: Specify the fields to extract (e.g., `1`, `1,3`, `2-5`, `1-`).
  - `-c CHARACTER_LIST`: Extract characters by position (e.g., `1-5`, `3`, `7-`).

---
