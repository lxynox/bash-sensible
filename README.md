# bash-sensible

🍳 Frequently used bash syntax (for dotfiles, file system apis)


## Contents

* [Arithmetic](#arithmetic)
* [String](#string)
* [Conditional](#conditional)
* [Loop](#loop)
* [Array](#array)
* [Built-in](#built-in)


### Arithmetic

#### arithmetic expansion

```bash
echo $(( 1 + 2 + 3 )) # output: 6
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

### Conditional

#### conditional expression

```bash
[[ -f $file ]] && echo $file is a file
```

#### `test` command

```bash
num=2
if test $(( num % 2 )) = 1
then
    echo $num is odd
elif test $(( num % 2 )) = 0
then
    echo $num is even
else
    echo $num is neither even nor odd
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
# list all **files** in $HOME directory

for doc in $HOME/*
do
    [ -f $doc ] && echo $doc is a file
done
```

#### while

```bash
# print out: 0 ... 9

x=0
while [ $x -lt 10 ]
do
    echo $x is less than 10
    (( x++ ))
done
```

#### pattern-based branching

```bash
# set the right option for bootstrapping dotfiles according to the `$action`

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
for key in "${arr[@]}"
do
    echo "key: $key"
    echo "value: ${arr[$key]}"
done
```

### Built-in

#### declaration commands

```bash
export name=value
```

> `export` makes the variable available to sub-process(not parent)

Read inputs

> read

```bash
# read name from command prompt(flag 'p' denotes prompt)
read -p name
```

> HERE doc

```bash
cat <<EOF > $HOME/.bash_profile
PATH=/usr/local/bin:$PATH
EOF
```

> HERE string

```bash
# split $PATH into an array of paths
arr_path=( $(grep -o '[^:]\+' <<< $(echo $PATH)) )
for path in ${arr_path[*]}
do
    echo $path
done
```

#### control flow and data processing

```bash
source $HOME/.bash_profile
```

> * `./script` runs the script as an excutable file, launching a **new shell** to run it

> * `source script` reads and executes commands from filename in the **current shell** env
