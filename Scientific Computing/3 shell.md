# Shell scripts and functions

## Shell scripts

A shell script is a text file containing a series of commands that can be executed by the shell.

```bash
#!/bin/bash
echo "Hello World!"
```

`#!` is the shebang and tells the shell to execute with `/bin/bash`.
Run the script with `./script.sh` after `chmod +x script.sh`.

### Variables

- `$0` the name of the script
- `$1`, `$2`, ... the first, second, ... argument passed to the script
- `$#` the number of arguments passed to the script
- `$@` all arguments passed to the script

### Operators

- `-lt` less than
- `-le` less than or equal to
- `-ge` greater than or equal to
- `-gt` greater than
- `-eq` equal to
- `-ne` not equal to
- `-a` and
- `-o` or
- `!` not
