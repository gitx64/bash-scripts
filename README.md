# Fundamental introduction (seemed important to know)


- grep '^ly' <file name>  -->  starts with 'ly'
- grep 'ly$ <file name>  -->  ends with 'ly'
- grep -i   -->   case insensitive pattern search
- grep -o '^d.'  --> print ONLY the part matches with pattern. (starts with d and any 1 character after d) 

- multi pipelining -> cat /usr/share/dict/words | grep -i dave | grep ly



------------------------------------------------------------------

# Pagination: less command for paginate a big file.

- less is more.

- type cp -> tells the type of cp if its external or internal command.

- man man -> for better info

- help echo -> the man command for bash internals is help.

- compgen -b -> lists all the built-ins of shell.

-----------------------------------------------------------------
# File Command

- file <filename> -> shows the type of content it contains.

- $PATH -> builtin variables.

- tr : '\n' -> translate all ':' to '\n' here means colon seperated lines to new line like C

* Use ' ' whenever you can for echoing anything or in other commands for variables or inputs I guess. Because without that thing it will just ignore any unneccessary things which it thinks. 

- unset foo -> to unset a temporary variable

- thing=$(...) -> syntax to store a command output.

-----------------------------------------------------------------
# SCripting:

.sh is posix compliant, which is not featurefull as bash. so no extention is needed cause proper shebang is there for the shell #!/usr/bin/env bash

for thing in foo bar baz bat; do 
	echo "thing is $thing"
done --> for loop which treats all after in as list.

bash -n -> for syntax checking of a bash script.

# USER INPUT

read -p 'Enter your name: ' name
yes -> dangerus yes command in loop.

------------------------------------------------------------------
# IF ELSE

-n : True if string is set. if [[ -n $1 ]] -> if string is set to first argument.

$@ : Get all the arguments passed without pre-declaration.

functions : greet (){
                        name=$1
                        echo "Hello $name" 
                    }
here it means when we will call the greet function we have to provide the $1 argument to store it inside the name variable.

we can also put the function execution to a file, store them in a variable and much more.

-f <filename> --> this means if the file exists and if its a file.

while [[ -f file.txt ]]; do
    echo 'file does exist'
do
  --> while loop is a for loop with the conditions like if. will run until a certain condition is true.

in if conditions only true false is not the limitation '[['. But we can also do simple bash commands or shell commands.

    if pacman -Sy; then
            echo "Update Successful"
    else
            echo "Update unsuccessfull:
    fi

TIP* scripts are just the bunch of bash scripts. which can be done in bare terminal also if indentation is good.

-----------------------------------------------------------------

# FOR_LOOPS

for thing in {a..f}; do
    echo "Thing is $thing"
done

    -> most interesting thing for loop through a to f including both. 

-----------------------------------------------------------------

# INPUT/OUTPUT

read -r -> for raw input which prevents read command to tinker with backslashes.

read by default reads only one line. To make it read all lines then put it inside while loop.

------------------------------------------------------------------
# CASE STATEMENT

case "$s" in
    d*) echo "Matched d*";;
    dave) echo "Matched dave";;
    a*) echo "Matched a*";;
    foo) echo "Matched foo";;
    *) echo "Matched *";;
esac

;; -> will check the first case and exit
;& -> will check the first case and executes all the remaining without checking

;;& -> will check every condition and check all then falls to default

------------------------------------------------------------------
TIP* Dont forget to double quote variable values in bash.

# INDEXED ARRAYS

array=(foo bar baz) -> syntax of array in bash

${array[index]} -> getting the indexed value of array
${array[*]} -> getting all the values in a single iteration
${array[@]} -> getting all the values in a multiple iterations

copied_array=( "${orig_array[@]}" ) -> create an array () inside that copy all of the previous array "${array[@]}" 

copied_array+=(buddy guy joe) -> push extra elements into that array

example_array=("hey there using bash here" foo bar baz)

for item in ${example_array[@]}; do 
    echo "item is :$item"
done

    -> here it will take the string as seperate items in the item without quotes

for item in "${example_array[@]}"; do 
    echo "item is :$item"
done

    --> here it will take the string as a single item in the array

------------------------------------------------------------------
# ASSOSIATIVE ARRAYS


- declare -A <arrayname> --> declares associative arrays.
- echo "${arr[@]}" --> as usual for values.
- echo "${!arr[@]}" --> for iterating over the keys not values.

TIP* prefer '@' for iterating over one by one value. and * for instant iteration.

-------------------------------------------------------------------
# IFS Variable

- IFS=, -> output will be IFS value seperated.
- can be declared inside a subshell which is safer.
- IFS can only work with one single complete iteration with * as array index

TIP* remember for iterating over keys in associative arrays: "${!array[@]}"

-------------------------------------------------------------------
# Command Substitution

- echo `whoami` -> prints the current user

- for notations the prefered syntax is dollar-paranthesis which works flawlessly all the time without any error $().

- if we use command substitution then local variable can not modify global variable. otherwise can.

- still want to modify globals and run funcs faster? while command-substitution??? alright, dunnow about vim syn-highlies but bash got you :)  thing=$(my-func) instead of this, this: thing=${ my-func;  }


------------------------------------------------------------------
# Arithmatic Expressions

- echo $(( 2+2 ))
- echo $(( $a + $b ))
- echo $(( 57 * 2  ))
- echo $(( 57 ** 2  )) '**' denotes the power
- when something can't be converted to integer bash will treat it as 0.
- (( c = a + b )) can also be done
- (( i++ ))
- >> - right bitwise operator (quick divition with 2**n where n is the number of positions shifted).
- << - left bitwise operator (quick multiplication with 2**n where n is the number of positions shifted).

- Most funny part is: Arithmatic expressions treats 0 as err. and bash treats non-zeros as err. So ((0)) will lead to an error for bash (1 non-zero). 

- if a=05 or 06 then its good to go because whenever bash sees zero infront of any values it assumes it as a octal value. but if we a=08 then it will show the error. to prevent it we have to do either in octal form of 08 (010) or echo $((10#$a)).

------------------------------------------------------------------
# PROCESS SUBSTITUTION

TIP* In for loop, "$variable" will treat the $variable to only 1. Which can be helpful forints, but not with strings.

- shift -> command to shift an entire array by one index so first index will be lost

${#args[@]} -> shows the index nums of values.
${!args[@]} -> think it shows the keys of args.

- more specifically if speaking, ${args[@]} is useful for input and ${args[*]} for output.

TIP* For functions never add $ for @. And for arguments never 

- in for loops if we dont give 'in' parameter it will iterate over all arguments ($@).
