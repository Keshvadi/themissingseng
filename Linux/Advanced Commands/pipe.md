---
title: Pipe
parent: Advanced Commands
nav_order: 31
layout: default
---

## Pipe (`|`)

The pipe operator (`|`) is a fundamental concept in Unix/Linux shell scripting, embodying the philosophy of combining small, specialized tools to accomplish complex tasks. Instead of monolithic applications, Linux provides many small commands that do one thing well. The pipe allows you to chain these commands together, creating powerful workflows.

- **Description:** The pipe (`|`) takes the _standard output_ of one command and feeds it as _standard input_ to another command. This allows you to build a "pipeline" of commands, where each command transforms the data and passes it on to the next.

- **Syntax:**

  ```bash
  command1 | command2 | command3 ...
  ```

  - `command1`'s output becomes `command2`'s input.
  - `command2`'s output becomes `command3`'s input (and so on).

- **Example Usage (with explanations and sample output):**

  1.  **Basic Piping:**

      ```bash
      ls -l | less  # List files in long format, and pipe the output to 'less' for easy scrolling
      ```

      _Sample output (opens in `less`): You'll see the `ls -l` output, but scrollable._
      This is a very common pattern for dealing with long outputs.

  2.  **Sorting Files by Size:**

      ```bash
      ls -l | sort -k 5rn  # List files, sort by the 5th column (size) in reverse numerical order (largest first)
      ```

      _Sample Output (truncated):_

      ```
      total 8
      -rw-r--r-- 1 user user 1024 Jul 10 10:00 large_file.txt
      -rw-r--r-- 1 user user  512 Jul 10 09:55 medium_file.txt
      -rw-r--r-- 1 user user    0 Jul 10 09:50 empty_file.txt
      ```

      _Explanation:_

      - `ls -l`: Lists files in long format.
      - `sort -k 5rn`:
        - `sort`: The sorting command.
        - `-k 5`: Sort by the 5th field (which is the file size in `ls -l` output).
        - `r`: Reverse the sort order (largest to smallest).
        - `n`: Numerical sort (treat the field as a number, not text).

  3.  **Combining and Sorting File Contents:**

      ```bash
      cat file1.txt file2.txt | sort > sorted_combined.txt
      # Concatenate file1.txt and file2.txt, sort the combined output, and save to sorted_combined.txt
      ```

          *Sample output: (No output to console)* The results are in `sorted_combined.txt`

      _Explanation:_

      - `cat file1.txt file2.txt`: Outputs the contents of both files, one after the other.
      - `sort`: Sorts the combined lines alphabetically.
      - `> sorted_combined.txt`: Redirects the sorted output to a new file.

  4.  **Unique Lines:**

      ```bash
      cat file.txt | sort | uniq  # Display only unique lines from file.txt (must be sorted first)
      ```

      _Explanation:_

      - `cat file.txt`: Outputs content of `file.txt`
      - `sort`: Sorts the lines alphabetically. `uniq` requires sorted input to work correctly.
      - `uniq`: Filters out adjacent duplicate lines, leaving only unique lines.

  5.  **Extracting File Sizes:**

      ```bash
      ls -l | awk '{print $5}'  # Print only the 5th column (file size) from the output of 'ls -l'
      ```

      _Explanation:_

      - `ls -l`: Lists files in long format.
      - `awk '{print $5}'`: Uses `awk` (a powerful text processing tool) to print only the 5th field of each line.

  6.  **Finding Processes:**

      ```bash
      ps aux | grep "firefox"  # List all processes, then filter to show only lines containing "firefox"
      ```

      _Explanation:_

      - `ps aux`: Lists all running processes.
      - `grep "firefox"`: Filters the output, showing only lines that contain the string "firefox" (case-sensitive).

  7.  **Filtering Log Files:**

      ```bash
      cat app.log | grep "ERROR"  # Display lines from 'app.log' that contain the word "ERROR"
      ```

  8.  **Finding Largest Files:**

      ```bash
      du -ah | sort -rh | head -n 5  # Show the 5 largest files/directories in the current directory
      ```

      _Explanation:_

      - `du -ah`:
        - `du`: Disk Usage
        - `-a`: Show all files and directory.
        - `-h`: "Human-readable" sizes (e.g., 1K, 234M, 2G).
      - `sort -rh`:
        - `sort`: sort command
        - `-r`: Reverse sort order (largest to smallest).
        - `-h`: "Human-readable" numeric sort (understands K, M, G suffixes).
      - `head -n 5`: Show only the first 5 lines of the output.

  9.  **Counting Word Occurrences (Case-Insensitive):**

      ```bash
      cat romeo_and_juliet.txt | grep -i "romeo" | wc -l
      # Count how many times "romeo" (or "Romeo", "ROMEO", etc.) appears in the file.
      ```

      _Explanation:_

      - `cat romeo_and_juliet.txt`: Outputs the content of the file.
      - `grep -i "romeo"`:
        - `grep`: Searches for a pattern.
        - `-i`: Case-insensitive search.
        - `"romeo"`: The pattern to search for.
      - `wc -l`:
        - `wc`: Word count.
        - `-l`: Count lines (since each line from `grep` contains one occurrence).

  10. **Shuffling and Selecting Lines:**

      ```bash
      shuf data.txt | head -n 10 > newfile.txt
      # Shuffle the lines of 'data.txt', take the first 10, and save them to 'newfile.txt'.
      ```

      _Explanation:_

      - `shuf data.txt`: Randomly shuffles the lines of the input file.
      - `head -n 10`: takes the first 10 lines.
      - `> newfile.txt`: saves the output in the `newfile.txt` file.

---
