---
title: The Shell
nav_order: 10
has_children: true
layout: default
---

## The Shell

Computers these days have a variety of interfaces for giving them commands; fanciful graphical user interfaces, voice interfaces, and even AR/VR are everywhere. These are great for 80% of use-cases, but they are often fundamentally restricted in what they allow you to do — you cannot press a button that isn’t there or give a voice command that hasn’t been programmed. When it comes to harnessing the full potential of our computer systems, we have to go old-school and drop down to a textual interface: **_The Shell_**.

<!-- Nearly all platforms you can get your hands on have a shell in one form or another, and many of them have several shells for you to choose from. While they may vary in the details, at their core they are all roughly the same: they allow you to run programs, give them input, and inspect their output in a semi-structured way. -->

In this tutorial, we will focus on the _Bourne Again SHell_, or “**_bash_**” for short (developed by Stephen Bourne in the late 1970s for the Unix operating system). This is one of the most widely used shells, and its syntax is similar to what you will see in many other shells. To open a shell prompt (where you can type commands), you first need a terminal.

<!-- Your device probably shipped with one installed, or you can install one fairly easily. -->

## Running Ubuntu in Docker

To explore Bash commands, we'll use Docker during this session. However, there are several options detailed in the [installation](./Installation) page that you can explore later.

For our current objectives, follow these steps:

1. Open Docker on your Windows system.
2. Open Command Line on your Windows system.
3. Run the following command to start an Ubuntu container:

   ```bash
   docker run -it --rm ubuntu:22.04
   ```

4. Inside the Ubuntu container, run the following command to update it:

   ```bash
   apt update -y # Update the package list on your system

   # Install 'unminimize' to restore a minimal installation to a more complete state
   unminimize
   ```

## Using the shell

When you launch your terminal, you will see a prompt that often looks a little like this:

```bash
root@ip-10-0-0-63:/#
```

This is the main textual interface to the shell. It tells you that you are on the machine ip-10-0-0-63 and that your "current working directory", or where you currently are, is \/ (short for “root” directory). The \# tells you that you are the root user (more on that later). At this prompt you can type a command, which will then be interpreted by the shell. The most basic command is to execute a program:

```bash
root@ip-10-0-0-63:/# date
Thu Jan  4 09:20:35 AM PST 2024
```

Here, we executed the **`date`** program, which (perhaps unsurprisingly) prints the current date and time. The shell then asks us for another command to execute.

_But how does the shell know how to find the date programs?_
Well, the shell is a programming environment, just like Python, and so it has variables, conditionals, loops, and functions. When you run commands in your shell, you are really writing a small bit of code that your shell interprets.

<!-- If the shell is asked to execute a command that doesn’t match one of its programming keywords, it consults an environment variable called `$PATH` that lists which directories the shell should search for programs when it is given a command. -->

## Flags and Options

Most commands accept flags and options (flags with values) that start with `-` to modify their behavior. Usually, running a program with the `-h` or `--help` flag will print some help text that tells you what flags and options are available.

For example, `ls` lists contents of the current directory, `ls -l` shows more detailed information, and `ls -a` displays hidden files.
