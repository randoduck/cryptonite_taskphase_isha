# Digesting Documentation

## Challenge 1: Learning From Documentation (Summary/Learning)
This challenge was held to calrify the documentaion and navigation process in the terminal 
To obtain the flag we must  run`/challenge/challenge` with athe argument `--giveflag`. 
### Solution
To Obtain the flag, the following command was executed :
```bash
/challenge/challenge --giveflag
```
## Challenge 2 : Learning Complex Usage (Summary/Learning)
A few more Arguments have been introduced for example `--printfile` which prints the file on the terminal , it accepts the path of the flag as the argument .
We were required to obtain the flag by invoking the `/challenge/challenge` program with the argument `--printfile`

### Solution
The flag was obtained using the following commands :

```bash
/challenge/challenge --printfile /flag
```
## Challenge 3: Reading Manuals (Summary/Learning):
Here a new command `man` was introduced , this command is short for manual, and will display (if available) the manual of the command you pass as an argument . 
To collect the flag by using a secret option which will be displayed through the man page for `challenge`

### Solution
To Obtain the flag the following commands were executed :
```bash
man challenge
```
The manual will be displayed which contianed the argument that must be passed to `/challenge/challenge` obtian the flag

```bash
/challenge/challenge --vhjuka 591
```
## Challenge 4: Searching Manuals (Summary/Learning):
Requires us to use the `man` command and then navigate through the manual displayed using the key *n* to go to the next result and *N* to go to the previous result
to obtian the flag we pass `challenge` as an argument to man page and navigate through it.

### Solution
To obtain the Flag the following commands were executed 
```bash
man challenge
```
After some navigation , we find the argument that needs to be passed to find the flag 
```bash
/challenge/challenge --tg
```
## Challenge 5:  Searching For Manuals (Summary/Learning)
We are now introduced to the `man man ` command which is an advanced usage of the man command itself, and you must use this knowledge to figure out how to search for the hidden manpage that will redirect you on how to use the /challenge/challenge

### Solution
To obtain the flag the following commands were executed :
```bash
man man
```
Navigating through the manual we find that flag can be obtained by passing  `man -k` with `challenge` as the argument.
```bash
man -k challenge
man czgpyodedy
/challenge/challenge --czgpyo 263
```

## Challenge 6: Helpful Programs (Summary/Programs):

### Challenge
Here we have been introduced to a new command `--help`, used to pass those commands as arguments that don't have a man page  often used as `-h` or, in rare cases, `-?`, `help`, or other esoteric values like `/?` 
we must make use of the `--help` to obtain the flag 

### Solution
To obtain the flag the following commands have been executed :
```bash
/challenge/challenge --help
```
we get the manual giving the list of arguments directing us to the flag 
```bash
/challenge/challenge -p
The secret value is: 981
/challenge/challenge -g 981
```

## Challenge 7: Help For Builtins (Summary/Learning)
We are here ntroduced to the concept of **builtins**.
Some commands, rather than being programs with man pages and help options, are built into the shell itself. These are called builtins. Builtins are invoked just like commands, but the shell handles them internally instead of launching other programs. You can get a list of shell builtins by running the builtin `help`.
we were required to use `help` on the builtin called `/challenge`

### Solution
Thw following commands have been executed to obtain the flag
```bash
help challenge
```
Based on the output given that specifies arguments that must be passed to `/challenge` we get the flag
```bash
challenge --secret AaeG6NiH
```

## <3