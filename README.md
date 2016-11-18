# bash-sensible

🍳 Frequently used bash syntax (for dotfiles, file system apis)


## Contents

* [String](#string)
* [Branch](#branching)
* [Loop](#looping)
* [Array](#array)


### String

#### length

```bash
len=${#str}
```

#### substring

```bash
sub=${str:pos:N}
```

#### iteration (for each char)

```bash
for (( i=0; i<${#str}; i++ )); do
    echo "${str:$i:1}"
done
```

OR

```bash
while test -n "$str"; do
    c=${str:0:1} # get first char
    echo $c
    str=${str:1} # trim first char
done
```

### Branch

#### Using `test` command

```bash
if test "<expression>" = "<result>"
then
    [ ... ]
elif test "<expression>" = "<result_alt>"
then
    [ ... ]
else
    [ ... ]
fi
```

#### Using `[]` command

```bash
if [ ...condition ]
then
    [ ... ]
fi
```

### Loop

#### for

```bash
for <expression>
do
    [ ... ]
done
```

#### while

```bash
while <expression>
do
    [ ... ]
done
```

### Array

#### Indexed(array)

> Declaration & Initialization

```bash
declare -a arr
arr[0]="foo"
arr[1]="bar"
```
or

```bash
arr=( "foo" "bar" )
```

#### Associative(array)

> Declaration & Initialization

```bash
declare -A hash
hash[FOO]="foo"
hash[BAR]="bar"
```

OR

```bash
declare -A hash=( [FOO]="foo" [BAR]="bar" )
```
