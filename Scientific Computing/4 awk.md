# awk & applications

## awk

awk is a fully programmable file manipulator.
It is a precursor to the `perl` language.

Basic syntax: `awk 'condition{action} file'`

- `condition` is a boolean expression. Can be logical or `/pattern/`.
  - If no condition is specified, the action is executed for every line. 
- `action` is a command to be executed if the condition is true.
- `file` is the file to be processed.

### Variables

- `NF` field count of the current line
- `FS` field separator (default is space " ")
- `RS` record separator (default is newline "\n")
- `$NR` number of the current record (line)
- `$FNR` number of the current record (line) within the current file
- `$0` the current line
- `$<n>` the n-th field of the current line
- `$NF` the last field of the current line

### Examples

- `awk '/#/{print $0} file'`
  - Print all lines that contain a `#` character.
- `awk '{print $1}' file`
  - Print the first field of all lines.
- `awk '/^error/{print $2, $3}' file`
  - Print the second and third field of all lines that start with `error`.
- `awk '{print $1, log($2)}' file`
  - Print the first field and the logarithm of the second field of all lines.
- `awk '$2>0{print $1, log($2)}' file`
  - Print the first field and the logarithm of the second field of all lines where the second field is greater than zero.
- `awk -F"\t" '{print $1 ", " $2}' file`
  - Print the first and second field of all lines, separated by a comma and a space.
- `ps | awk '{print $NF "\t" $1}' | awk 'NR==1||/^[ap]/{print $0}'`
  - Get all processes
  - Get the last field (process name) and the first field (process id) of all lines separated by a tab
  - Print the first line and all lines that start with `a` or `p`

## awk scripts

```awk
!/usr/bin/awk -f
BEGIN { executed before the file is read }
{
    script applied to each line of the file
}
END { executed after the entire file has been read }
```

- The shebang `!/usr/bin/awk -f` is optional but allows the script to be executed directly.
  - With shebang: `./script.awk` after `chmod +x script.awk`
  - Without shebang: `awk -f script.awk`
  - Run `which awk` to find the path to the awk executable.
- The _BEGIN_ and _END_ blocks are optional.
- Spaces around `=` are optional.
- Semicolons are optional but required if multiple commands are on one line.

### Example: Table of Trig Values

```awk
#!/usr/bin/awk -f
BEGIN {
    pi = 4*atan2(1,1)
    
    fmt1 = "%3s %8s %8s %8s %8s\n"
    fmt2 = "%3i %8.4f %8.4f %8.4f %8.4f\n"
    
    printf(fmt1,"deg","rad","cos","sin","tan")
    
    for (n=0;n<=90;n++) {
        ang = n*(pi/180)
        printf(fmt2,n,ang,cos(ang),sin(ang),(n==90)?9999:sin(ang)/cos(ang))
    }
    exit
}
```
