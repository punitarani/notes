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
It works by modifying the value of the `pwd` (present working directory) environment variable.
It doesn't generate any output on the terminal when executed.

For some shells like `bash` also support `~` symbol as shortcut for the home directory, for example `cd ~` is the same as `cd`.

Please note that the directories must exist and you have the permissions to access it, otherwise it will give an error message.
Also the command will only change the current working directory for the shell session or terminal you are using, it won't affect other open terminals or sessions.
