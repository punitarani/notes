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

### Example 1: Sum of first n integers

```bash
#!/bin/bash
sum=0

for i in $(seq 1 $1)
do
    sum=$((sum+i))
done

echo $sum
```

The `$1` is the first argument passed to the script.
The `seq 1 $1` command generates a sequence of numbers from `1` to the first argument.
Run the script with `./sum.sh 10` to get the sum of the first 10 integers.

Using a `while` loop instead of a `for` loop:

```bash
#!/bin/bash
sum=0

i=1
while [ $i -le $1 ]
do
    sum=$((sum+i))
    i=$((i+1))
done

echo $sum
```

Usage: `./sum.sh 10`

### Example 2: Simple calculator

```bash
#!/bin/bash
if test $# = 3; then
    case $2 in
    +) z=$(echo $1+$3 | bc -l);;
    -) z=$(echo $1-$3 | bc -l);;
    /) z=$(echo $1/$3 | bc -l);;
    x) z=$(echo $1\*$3 | bc -l);;
    *) echo "$2 invalid operation"
    exit;;
    esac
    echo $z
else
    echo "usage: ./mycalc.bash <num> <op> <num>"
fi
```

Usage: `./mycalc.bash 1 + 2`

### Example 3: Trigonometric Values Generator with File I/O

```bash
#!/bin/bash

pi=$(echo "4*a(1)" | bc -l)

for k in 0 1 2; do
    file=ftrig$k.dat
    if [ -s $file ]; then
        rm $file # remove if file exists
    fi
    n=0
    while [ $n -lt 10 ]; do
        nn=$(($n+10*k))
        ang=$(echo "$pi*$nn/180" | bc -l)
        echo "$ang" >> $file
        n=$(($n+1))
    done
done

for file in ftrig*.dat; do
    echo; echo "for file $file" # append value of angle
    while read line; do
        x=$(echo "s($line)" | bc -l)
        y=$(echo "c($line)" | bc -l)
        echo $x $y
    done < $file
done
```
