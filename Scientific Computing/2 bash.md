# Bash basics

## Computers in a nutshell

### Operating system

A collection of software that manages computer hardware resources and provides common services for computer programs.
The operating system is the most important type of system software in a computer system.

### Kernel

The core part of an operating system that controls all other parts of the system.
It is responsible for managing system resources such as memory, processors, and devices.
It also provides a communication interface between applications and hardware.

### Shell

A command-line interface that allows users to interact with an operating system by typing commands.
It provides an interface to the kernel, allowing users to execute various tasks such as file management, process management, and system configuration.
Examples of shells include the Windows Command Prompt and the Unix/Linux Bash shell.

## Bash

Bash is a Unix shell and command language written by Brian Fox for the GNU Project as a free software replacement for the Bourne shell.
It is a command-line interpreter that executes commands read from the standard input device or from a file.
It is also a scripting language that can be used to write shell scripts.

### Useful commands

- `ls` lists files
  - `ls - l` gives a ‘long’ listing ordering the files alphanumerically
  - `ls - a` includes ‘hidden’ files (. * ) `ls -r` lists files in reverse order
  - `-l` , `-a` , `-r` are options, and can be combined
  - `ls - lt` gives a ‘long’ listing ordering the files by modification time
  - `ls - ltr` lists files in long format by reverse modification time (most recent last)
  - `-F` appends a character to the end of a listing depending on filetype
- `chmod` manages file permissions
  - `chmod u+x f1` adds user execute permission to file `f1`
  - `chmod u-x f1` removes user execute permission to file `f1`
  - `chmod 644 f1` sets permissions to `-rw -r--r--` (r = 4, w = 2, x = 1)
  - `chmod 644 f*` sets permissions to `-rw -r--r--` for all files starting with `f`
- `head` and `tail` print the beginning or end of a file
  - `head f1` prints the first 10 lines in file `f1` (default)
  - `head -5 f1` prints the first 5 lines in file `f1`
  - `tail - 5 f1` prints the last 5 lines in file `f1`
    - `tail` can be used to monitor a stream of data as it comes in
- `pwd` prints the current working directory
- `mkdir dir` creates a directory called `dir`
- `cd dir` makes `dir` the current directory
  - `.` refers to the current directory and `..` to its parent
  - `cd ..` moves to the parent directory in the directory hierarchy (tree)
  - `cd ../dir2` navigates one directory up, then down to `dir2` (⇔ `cd ..; cd dir2`)
  - `cd /` moves to the top directory on the computer
  - `cd ~` (or simply `cd` ) moves to the top directory in the user’s account
  - `cd -` navigates to the previous directory
- `cp` copies files and directories
  - `cp f1 f2` copies file `f1` to file `f2`
  - `cp f1 dir1` copies file `f1` to directory `dir1`
  - `cp -r dir1 dir2` copies directory `dir1` to directory `dir2`
- `mv` moves or renames files and directories
  - `mv f1 f2` moves file `f1` to file `f2`
  - `mv f1 dir1` moves file `f1` to directory `dir1`
  - `mv dir1 dir2` moves directory `dir1` to directory `dir2`
  - `mv f1 f2` renames file `f1` to `f2`
- `rm` removes files and directories
  - `rm -r dir1` removes directory `dir1` and all its contents
- `sort` sorts lines of text files
  - `sort f1` does a lexicographical (ascending) sort on file `f1` (numbers first)
  - `sort -nr f1` sorts file f1 in reverse numeric order
  - `sort -k2 f1` sorts file f1 according to the second field in each line
  - `sort -n f1 > f1sorted` saves the output of sort in `f1sorted`. Overwrites `f1sorted` if file already exists. Same as `sort -n f1 -o f1sorted`
  - `sort - n f1 >> f1 sorted` appends the output of sort to `f1sorted`
  - `sort - n f1 | head -1` prints the line with the largest number in the first field
- `cat f1 f2 > f3` concatenates `f1` and `f2` and saves the result into `f3`
  - `cat f1 | cut -c15-20 > f2` extracts columns 15 to 20 of `f1` and saves them in `f2`
- `locate f1` looks for files in all of `/` whose name contains the string `f1`
  - `locate -b 'f1'` looks for files in all of `/` whose name contains the string `f1`
  - `find . -type f -name 'f*'` looks for files (not directories) whose name begins with `f` in the current directory and subdirectories
- `alias myfind='find . -type f -name'` enables to use the shorter `myfind'f*'` `man command` or `command --help` prints manual pages on command.
- `!-1` runs last command (can also use ↑). Type `history` for a list of past commands

#### Redirection

- `>` redirects all output
  - `1>` redirects standard output
  - `2>` redirects standard error
  - `&>` redirects both standard output and standard error
- `>>` appends all output
- `<` redirects all input
- `|` redirects output to input
