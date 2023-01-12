# Linux commands

## `ls`

`ls` is a command used to list the contents of a directory.
When run without any arguments, `ls` will list the files and directories in the current working directory.

Here are some common usage examples:

- `ls` - lists the files and directories in the current directory
- `ls -l` - lists the files and directories in a "long" format, including details such as file permissions, ownership, and timestamps
- `ls -a` - lists all files and directories, including hidden files and directories (those that begin with a dot ".")
- `ls -la` - combines the -l and -a options, showing a long listing of all files and directories
- `ls dirname` - lists the contents of the specified directory "dirname"
- `ls file1 file2` - lists information about the specified files "file1" and "file2"

The ls command has many options, some of them are:

- `-a`, --all
- `-d`, --directory
- `-h`, --human-readable
- `-l`, --long format
- `-r`, --reverse
- `-R,` --recursive
- `-t`, --sort-by-time

## `cd`

`cd` stands for "change directory".
It is used to navigate the file system by changing the current working directory.

Here are some common usage examples:

- `cd` - without any arguments, cd will change the current working directory to the user's home directory
- `cd dirname` - changes the current working directory to the directory "dirname"
- `cd ..` - changes the current working directory to the parent directory
- `cd -` - changes the current working directory to the previous directory

The `cd` command is a shell built-in command, meaning it is executed directly by the shell rather than by spawning an external process.
It works by modifying the value of the `PWD` (present working directory) environment variable.
It doesn't generate any output on the terminal when executed.

For some shells like `bash` also support `~` symbol as shortcut for the home directory, for example `cd ~` is the same as `cd`.

Please note that the directories must exist and you have the permissions to access it, otherwise it will give an error message.
Also the command will only change the current working directory for the shell session or terminal you are using, it won't affect other open terminals or sessions.

## `pwd`

`pwd` stands for "print working directory" and displays the full path of the current working directory.

This command doesn't accept any options or arguments, it just prints the current working directory to the terminal.

The `pwd` command is also a shell built-in command, meaning it is executed directly by the shell rather than by spawning an external process.
It works by reading the value of the `PWD` (present working directory) environment variable, which is automatically set and updated by the shell as you navigate the file system.

## `mkdir`

`mkdir` is a command in Linux and other Unix-like operating systems that stands for "make directory".
It is used to create new directories (also known as "folders") in the file system.

Here are some common usage examples:

`mkdir dirname` - creates a new directory with the name "dirname" in the current working directory
`mkdir -p dir1/dir2/dir3` - creates a nested directory structure, creating "dir1", "dir2", and "dir3" if they do not already exist.
mkdir command accepts some options:

`-p` or `--parents` - no error if existing, make parent directories as needed
`-v` or `--verbose` - print a message for each created directory
`-m` or `--mode` - set file mode (as in chmod), not rwxrwxrwx - umask
`-Z` or `--context` - set the SELinux security context of each created directory to the default type

By default, `mkdir` will only create a new directory if the specified name does not already exist.
If the directory already exists, `mkdir` will return an error message.

Also, if the user doesn't have write permissions on the parent directory where the new folder will be created, the command will fail with a "permission denied" error.

It is important to notice that when you specify a nested directory structure with mkdir, only the last directory will have the mode you specified, the parent directories will be created with the default permissions of the filesystem.

## `cp`

`cp` stands for "copy" and is used to copy files and directories in the file system.

Here are some common usage examples:

- `cp file1 file2` - copies the file "file1" to a new file "file2"
- `cp file1 dir1` - copies the file "file1" to the directory "dir1"
- `cp dir1 dir2` - copies the directory "dir1" to a new directory "dir2"
- `cp -r dir1 dir2` - copies the directory "dir1" and its contents to a new directory "dir2"
- `cp file1 file2 file3 dir1` - copies multiple files to a directory

`cp` command accepts some options:

- `-a` or `--archive` - same as -dpR --preserve=all
- `-d` or `--no-dereference` - same as --preserve=links
- `-f` or `--force` - if an existing destination file cannot be opened, remove it and try again (this option is ignored when the -n option is also used)
- `-i` or `--interactive` - prompt before overwrite (overrides a previous -n option)
- `-l` or `--link` - hard link files instead of copying
- `-L` or `--dereference` - always follow symbolic links in SOURCE
- `-n` or `--no-clobber` - do not overwrite an existing file (overrides a previous -i option)
- `-p` or `--preserve` - preserve attributes if possible (default: mode,ownership,timestamps), if an attribute cannot be preserved, give a diagnostic message and try to copy as much as possible
- `-r` or `--recursive` - copy directories recursively
- `-s` or `--symbolic-link` - make symbolic links instead of copying
- `-u` or `--update` - copy only when the SOURCE file is newer than the destination file or when the destination file is missing

Please note that the `cp` command will overwrite the destination file or directory if it already exists and have the write permissions, otherwise the command will fail with a "permission denied" error.
Also, when you copy recursively, it will preserve the permissions, timestamps and attributes of the original files and directories, unless specified with options.

Also, if you want to rename a file or a folder you can use cp command with the same name for the source and destination file/folder.

## `mv`

`mv` stands for "move" and is used to move or rename files and directories in the file system.

Here are some common usage examples:

- `mv file1 file2` - renames the file "file1" to "file2"
- `mv file1 dir1` - moves the file "file1" to the directory "dir1"
- `mv dir1 dir2` - renames the directory "dir1" to "dir2" (if "dir2" doesn't exist)
- `mv dir1 dir2` - moves the directory "dir1" to the directory "dir2" (if "dir2" already exists)
- `mv file1 file2 file3 dir1` - moves multiple files to a directory

`mv` command also accepts some options:

- `-f` or `--force` - if an existing destination file cannot be opened, remove it and try again (this option is ignored when the -n option is also used)
- `-n` or ``--no-clobber` - do not overwrite an existing file (overrides a previous -i option)
- `-i` or `--interactive` - prompt before overwrite (overrides a previous -n option)
- `-T` or `--no-target-directory` - treat DEST as a normal file
- `-u` or `--update` - move only when the SOURCE file is newer than the destination file or when the destination file is missing
- `-v` or `--verbose` - explain what is being done

Please note that the `mv` command will overwrite the destination file or directory if it already exists and have the write permissions, otherwise the command will fail with a "permission denied" error.
When you move a directory, it changes the parent of the directory, so it will change the inode number of the file(s) inside the directory.
Also, it preserves the timestamps and attributes of the original files and directories, unless specified with options.

Also, as mentioned, `mv` command can be used to rename files and directories, it is useful when you want to change the name of a file/folder and you are already in the location where the file/folder is located.

## `rm`

`rm` stands for "remove" and is used to remove files and directories in the file system.

Here are some common usage examples:

- `rm file1` - removes the file "file1"
- `rm -r dir1` - removes the directory "dir1" and its contents
- `rm file1 file2 file3` - removes multiple files
- `rm -f file1` - removes the file "file1" without prompting for confirmation

`rm` also accepts some options:

- `-d`or `--dir` - remove empty directories
- `-f` or `--force` - ignore nonexistent files and never prompt
- `-i`or `--interactive` - prompt before every removal
- `-r` or `-R` or `--recursive` - remove directories and their contents recursively
- `-v` or `--verbose` - explain what is being done

## `rmdir`

`rmdir` stands for "remove directory" and is used to remove empty directories in the file system.

Here are some common usage examples:

- `rmdir dirname` - removes the empty directory "dirname"
- `rmdir dir1/dir2/dir3` - removes the empty directory "dir3" and its parent directories "dir2" and "dir1" if they are also empty.

`rmdir` command only accepts one option:

`-p` or `--parents` - remove DIRECTORY and its ancestors; e.g., `rmdir -p a/b/c` is similar to rmdir a/b/c a/b a

It is important to note that the rmdir command will only work on empty directories, it will not delete directories with files or other directories in them.
If the directory specified is not empty, the command will return an error message.
To remove a directory and its contents recursively, you should use rm `-r` command instead.

Also, if you don't have write permissions on the specified directory, the command will fail with a "permission denied" error.

Also, for safety reasons, some shells like bash provide the command `rm` with an option `-i` or `--interactive`, this way the command will prompt you to confirm before deleting a file, using this option can be helpful to prevent accidentally delete important files or directories.

## `touch`

`touch` is used to create new files or update the timestamps of existing files.

`touch file1` - creates an empty file with the name "file1" in the current working directory if the file doesn't exist, or update the timestamp of the file to the current time if it does exist.
`touch -a file1` - update the access time of the file "file1" to the current time
`touch -m file1` - update the modification time of the file "file1" to the current time

`touch` command accepts some options:

`-a` or `--time=atime` - change only the access time
`-c` or `--no-create` - do not create any files
`-m` or `--time=mtime` - change only the modification time
`-r` or `--reference=FILE` - use this file's times instead of current time
`-t` or `--time=TIME` - use [[CC]YY]MMDDhhmm[.ss] instead of current time

The `touch` command is often used as a simple way to create new, empty files, but it can also be used to update the timestamps of existing files.
This can be useful when you want to "touch" a file to indicate that it has been updated, even if the file's contents haven't actually changed.
It can be also used to change the timestamps of multiple files at once by specifying the files you want to update as arguments,

Also, if the specified file doesn't exist, `touch` command will create the file but if you don't have write permissions on the current working directory the command will fail with a "permission denied" error.

## `chmod`

`chmod` stands for "change mode" and is used to change the permissions of files and directories in the file system.

File permissions in linux are controlled by three sets of access rights, each one associated with a specific category of users:

- User (or owner): the owner of the file
- Group: the group that owns the file
- Others: all other users

Each set of permissions is represented by a three-digit octal number, where each digit represents the permissions for one category of users. Each digit is the sum of the values of the permissions it represents. The possible values for each digit are:

- 0 (no permissions)
- 1 (execute)
- 2 (write)
- 4 (read)

Here are some common usage examples:

- `chmod 755 file1` - gives read, write, and execute permissions to the owner, and read and execute permissions to others, for the file "file1"
- `chmod 644 file1` - gives read and write permissions to the owner, and read permissions to others, for the file "file1"
- `chmod +x file1` - adds execute permissions to the owner of the file "file1"
- `chmod -w file1` - removes write permissions from the owner of the file "file1"

`chmod` command accepts some options:

- `-c` or `--changes` - like verbose but report only when a change is made
- `-f` or -`-silent` - do not report when permissions on a file cannot be changed
- `-R` or `--recursive` - change files and directories recursively
- `-v` or `--verbose` - verbosely describe the action

It is important to note that the chmod command can only be executed by the owner of the file or by a superuser.
Also, that the permissions can be represented either in octal notation or symbolic notation, where `+` adds, `-` removes and `=` sets permissions to the users.
Also, you can use the `u`,  `g`,  `o` , and `a` letters to specify the category of users, for example: `chmod u+x file1` will give execute permissions to the owner of the file file1.

Also, it's worth to notice that with `chmod`, as well as other commands that modify files, it's recommended to make a backup copy of the files before making changes, in case any unintended consequences happen.

## `grep`

`grep` stands for "global regular expression print".
It is used to search for patterns in text files, streams or standard input.
It's a powerful command that allows you to search for specific words, phrases, or regular expressions in one or more files.

Here are some common usage examples:

`grep "word" file1` - searches for the string "word" in the file "file1"
`grep -r "word" dir1` - searches for the string "word" in all files under the directory "dir1" recursively
`grep -n "word" file1` - searches for the string "word" in the file "file1" and also display the line numbers where the match was found
`cat file1 | grep "word"` - searches for the string "word" in the standard input, in this case the output of the cat command applied to "file1"
`grep -v "word" file1` - searches for all lines that do not contain the string "word" in the file "file1"

grep command accepts many options, some of the most common are:

`-r` or `-R` or `--recursive` - search recursively through the directory
`-n` or `--line-number` - prefix each line of output with the line number within its input file
`-c` or `--count` - only display a count of matching lines instead of the matching lines themselves
`-i`  or `--ignore-case` - perform the search ignoring case distinctions
`-v` or `--invert-match` - invert the sense of matching, to select non-matching lines
`-w` or `--word-regexp` - only match whole words
`-e` or `--regexp` - specify a pattern to search for, this option can be used multiple times to search for multiple patterns
`-f` or `--file` - obtain patterns from a file
`-E` or `-G` or `-P` - specifies the type of regular expression used, `-E` for extended, `-G` for basic, `-P` for Perl-compatible
`-o` or `--only-matching` - show only the part of a line matching the pattern

By default `grep` will search for the specified pattern or regular expression in a case-sensitive way and print the lines that contain the match.
Using these options, you can customize the behavior of the grep command to suit your specific needs.
