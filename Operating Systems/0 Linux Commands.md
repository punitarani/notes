# Linux commands

## `ls`

`ls` is a command used to list the contents of a directory.
When run without any arguments, `ls` will list the files and directories in the current working directory.

Here are some common usage examples:

- `ls` - lists the files and directories in the current directory
- `ls -l` - lists the files and directories in a "long" format, including details such as file permissions, ownership, and timestamps
- l`s -a` - lists all files and directories, including hidden files and directories (those that begin with a dot ".")
- `ls -la` - combines the -l and -a options, showing a long listing of all files and directories
- l`s dirname` - lists the contents of the specified directory "dirname"
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
