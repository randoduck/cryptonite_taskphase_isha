# Shell Variables

## Challenge 1: Printing Variables  (Summary/Learning)
We have been introduced to the `echo` command which is used for printing things , we can make use of the `$` sign. prepend it to a variable to print out the variable . We can obtain the flag by printing out the variable `FLAG`

### Solution
 To obtain the flag , the following commands were executed :
 ```bash
cd ~
echo $FLAG
```

## Challenge 2: Setting Variables (Summary/Learning)
Another character is introduced here : `=`, which is used to set the value of a variable to something .
We can acess the variable again using the `$` sign . While assigning we must remember to not inlclude the `$` sign as its an access variable. 

### Solution
To obtain the flag the following command was executed :
```bash
PWN=COLLEGE
```
## Challenge 3: Multi Word Variables (Summary/Learning)
Here they introduce to the ` " "` which is used to simplify the process of assigning a value to a variable because generally only the immediate sequence of charcaters after the `=` are considered and the rest is considered as a command . Here were are supposed to assign `COLLEGE YEAH` to `PWN`.

### Solution
To obtain the flag the following commands were executed :
```bash
hacker@variables~multi-word-variables:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cd ~
hacker@variables~multi-word-variables:~$ PWN="COLLEGE YEAH"
```
## Challenge 4: Exporting Variables (Summary/Learning):
Here we have been introduced to the concept of exporting files from a local shell process . Any and all vraible assignment remain in the local shell unless they are exported (they get passed onto environment varibles of this new process thats been started using the `sh` command ) and this can be chcked by using the `$` prompt and passing `sh` command to start introduce another shell within the shell and checking for the variable assignment using `echo`. In this challenge we are asked to check using the `/challenge/run` command after setting the value of PWN to COLLEGE (and exporting it) and the value of COLLEGE to PWN.

### Solution
The flag can be obtained by executing the following commands:
```bash
PWN=COLLEGE
export PWN
COLLEGE=PWN
sh
/challenge/run PWN
```
## Challenge 5: Printing Exported Variables (Summary/Learning):
env command: it'll print out every exported variable set in the shell. The output holds the value of the FLAG
### Solution
The flag was obtained by executing the following commands 
```bash
cd ~
env

```
## Challenge 6 :  Storing Command Output (Summary/Learning)
We have been introduced to the concept of **Command Substitution** which basically is storing the value of a command inside a variable. The following format can be used :
->`variable=$(command output)`
->`variable=``command output`- making use of backticks 
we must  the output of the /challenge/run command directly into a variable called PWN to obtain the flag 
### Solution
To obtain the flag the following code must be executed 
```bash
hacker@variables~storing-command-output:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cd ~
hacker@variables~storing-command-output:~$ PWN=$(/challenge/run)
Congratulations! You have read the flag into the PWN variable. Now print it out 
and submit it!
hacker@variables~storing-command-output:~$ echo $PWN

```
## Challenge 7: Reading Input (Summary/Learning):
We've been introduced to the concept of reading input from the user that can be done using the `read` builtin. Which takes in -p argument, which lets you specify a prompt.
The format for reading would be :
`read -p "Give your input:" variable_where_it_is_stored`
we must use read to set the PWN variable to the value COLLEGE to obtain the flag
### Solution
The flag was obtained by executing the following commands 
```bash
 hacker@variables~reading-input:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cd ~
hacker@variables~reading-input:~$ read -p "Enter Input:" PWN
Enter Input:COLLEGE
```
## Challenge 8: Reading Files (Summary/Learning):
Combining the concepts of reading user input into a variable, redirecting files into command input we must read files with the shell.
### Solution
The flag was obtained by executing the following commands 
```bash
hacker@variables~reading-files:~$ read PWN < /challenge/read_me
```
## <3