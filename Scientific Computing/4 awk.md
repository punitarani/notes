# awk & applications

## awk

awk is a fully programmable file manipulator.
It is a precursor to the `perl` language.

Basic syntax: `awk 'condition{action} file'`

- `condition` is a boolean expression. Can be logical or `/pattern/`.
  - If no condition is specified, the action is executed for every line. 
- `action` is a command to be executed if the condition is true.
- `file` is the file to be processed.

- `NF` field count of the current line
- `FS` field separator (default is space " ")
- `RS` record separator (default is newline "\n")
- `$NR` number of the current record (line)
- `$FNR` number of the current record (line) within the current file
- `$NF` number of fields in the current record (line)
- `$0` the current line
- `$<n>` the n-th field of the current line
