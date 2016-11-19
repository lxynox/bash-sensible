# bash-sensible

🍳 Frequently used bash syntax (for dotfiles, file system apis)


## Contents

* [Arithmetic](#arithmetic)
* [String](#string)
* [Conditional](#conditional)
* [Loop](#looping)
* [Array](#array)


### Arithmetic

#### arithmetic expansion

```bash
(( 1 + 2 + 3 ))
```

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

### Conditionals 

#### conditional expression

```bash
[[ -f $file ]] && echo $file is a file
```

#### `test` command

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

#### `[]` command

```bash
if [ -d $dir ]
then
    echo $dir is a directory
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

#### pattern-based branching

```bash
 case "$action" in
 o )
     overwrite=true;;
 O )
     overwrite_all=true;;
 b )
     backup=true;;
 B )
     backup_all=true;;
 s )
     skip=true;;
 S )
     skip_all=true;;
 * )
     ;;
esac
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

> Destruction(whole array)

```bash
unset -v arr/arr[@]/arr[*]
```

> Destruction(by index)

```bash
unset -v arr[N]
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

> Destruction

```bash
unset -v arr[STRING]
```

> Store(values)

append

```bash
arr+=(E1 E2)
``` 

> Retrieve(values)

iteration

```bash
for key in "${arr[@]}
do
    echo "key: " $key
    echo "value: " ${arr[$key]"
done
```
   
