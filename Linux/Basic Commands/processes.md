---
title: Processes (ps, top, kill)
parent: Basic Commands
nav_order: 25
layout: default
---

## Processes (`ps`, `top`, `kill`, `htop`)

Processes are running instances of programs on your system. Understanding how to view, manage, and terminate processes is fundamental to working with Linux. This section covers essential commands for process management.

---

### `ps`

- **Description:** Displays information about currently running processes. `ps` by itself shows only processes associated with your current terminal session, which is usually not very informative. The real power of `ps` comes with its options.
- **Example Usage:**

  ```bash
  ps aux  # The most common and useful combination of options
  ```

  _Sample Output (truncated):_

  ```
  USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
  root         1  0.0  0.1  167748  9560 ?        Ss   Jul04   0:01 /sbin/init
  root         2  0.0  0.0       0     0 ?        S    Jul04   0:00 [kthreadd]
  user     12345  0.1  0.5  456789 20000 ?        S    09:30   0:05 /usr/bin/my_program
  user     12346  0.0  0.1   12345  4000 pts/0    Ss   09:31   0:00 bash
  user     12400  0.0  0.1   13456  4500 pts/0    R+   09:45   0:00 ps aux
  ```

  _Explanation of Output Columns:_

  - **USER:** The user who owns the process.
  - **PID:** The Process ID (a unique number assigned to each process). This is _critical_ for `kill`.
  - **%CPU:** The percentage of CPU time the process is using.
  - **%MEM:** The percentage of system RAM the process is using.
  - **VSZ:** Virtual memory size (in KB).
  - **RSS:** Resident Set Size (physical memory in use, in KB).
  - **TTY:** The controlling terminal (often `?` for daemons/system processes).
  - **STAT:** The process state (e.g., `S` = sleeping, `R` = running, `Z` = zombie).

    - **S:** Interruptible sleep (waiting for an event to complete)
    - **R:** Running or runnable (on run queue)
    - **D:** Uninterruptible sleep (usually IO)
    - **T:** Stopped, either by a job control signal or because it is being traced.
    - **Z:** "zombie" process, terminated but not reaped by its parent.
    - A trailing `+` indicates the process is in the foreground process group.

  - **START:** The time the process started.
  - **TIME:** The total CPU time the process has used.
  - **COMMAND:** The command that started the process.

  _Key Options for `ps`:_

  - `ps aux`: Shows _all_ processes on the system, in a detailed format, including processes not associated with a terminal. This is generally the most useful way to use `ps`.
  - `ps -ef`: Another common way to view all processes, but with slightly different output format (includes parent process ID - PPID).
  - `ps -u [username]`: shows the processes which are related to a certain user.
  - `ps -p <PID>`: Shows information about a specific process ID. Useful after you've found a PID with `ps aux` or `top`.

---

### `top`

- **Description:** Displays a dynamic, real-time view of running processes. Think of it as a task manager for the command line.
- **Example Usage:**

  ```bash
  top
  ```

  _Sample Output (truncated - it's a live, updating display):_

  ```
  top - 10:01:23 up 1 day,  2:34,  1 user,  load average: 0.50, 0.45, 0.40
  Tasks: 250 total,   1 running, 249 sleeping,   0 stopped,   0 zombie
  %Cpu(s):  5.0 us,  1.7 sy,  0.0 ni, 93.3 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
  MiB Mem :   7853.0 total,   4000.0 free,   2000.0 used,   1853.0 buff/cache
  MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   5500.0 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
  12345 user      20   0  456789  20000  15000 S   5.0   0.3   0:05.00 my_program
      1 root      20   0  167748   9560   6000 S   0.0   0.1   0:01.00 init
  ...
  ```

  _Key Interactive Commands within `top`:_

  - **q:** Quit `top`.
  - **k:** Kill a process (you'll be prompted for the PID).
  - **u:** Show processes for a specific user.
  - **P:** Sort by CPU usage (default).
  - **M:** Sort by memory usage.
  - **h:** Display help.
  - **1**: show per-core CPU.
  - **z**: toggle colors.
  - **space**: Immediately refresh display.

---

### `kill`

- **Description:** Sends a signal to a process. The most common use is to terminate a process, but `kill` can send other signals as well.
- **Example Usage:**

  ```bash
  kill 12345     # Sends the default signal (TERM - terminate) to process ID 12345
  kill -9 12345  # Sends the SIGKILL signal (forcefully terminate) to process ID 12345
  kill -l        #list all signal names.
  kill -s HUP 123 #Sends the HUP signal to process with PID 123.

  ```

  _Important Signals:_

  - **-1 (SIGHUP):** "Hang up." Some daemons reload their configuration when they receive this signal.
  - **-2 (SIGINT):** Interrupt. Usually same as pressing Ctrl+C.
  - **-9 (SIGKILL):** "Kill." This forcefully terminates the process _immediately_. It should be used as a last resort, as the process doesn't get a chance to clean up.
  - **-15 (SIGTERM):** "Terminate." This is the _default_ signal sent by `kill`. It allows the process to terminate gracefully (e.g., save files, close connections). This is generally the first signal you should try.

  _Note:_ You can only kill processes that you own (or processes you have root privileges to kill).

---

### `htop` (Suggested Addition)

- **Description:** An enhanced, interactive process viewer, similar to `top` but with a more user-friendly interface, color-coding, and mouse support. It's often not installed by default.
- **Installation (Debian/Ubuntu):**
  ```bash
  sudo apt install htop
  ```
  **(Installation for other distributions will vary)**
- **Installation (CentOS/Fedora):**

  ```bash
  sudo yum install htop
  #OR
  sudo dnf install htop
  ```

- **Example Usage:**

  ```bash
  htop
  ```

  _Key Features of `htop`:_

  - Color-coded display for easy readability.
  - Mouse support for scrolling and selecting processes.
  - Tree view of processes (showing parent-child relationships).
  - Easier process killing (select a process and press F9, or k).
  - Customizable display options.

  _Key Interactive commands within `htop`:_

  - **F1,h,?:** help.
  - **F2, S:** Setup options.
  - **F3, /**: Search processes.
  - \*\*F4, \*\*: Filter Processes
  - **F5, t:** Tree view.
  - **F6, >:** Sort processes.
  - **F7, ]:** Increase priority.
  - **F8, [:** Decrease priority.
  - **F9, k**: kill process.
  - **F10, q:** Quit.
  - **Space**: tag/untag a process.
  - **U**: Untag all processes.

  _Sample Output (not representable in text, but it's a colorful, interactive display)_

---
