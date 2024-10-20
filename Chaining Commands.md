## Chaining Commands 


## Challenge 1: Chaining with Semicolons (Summary/Learning):
We have been introduced tp the concept of chaining commands here, The easiest way to chain commands is **;**. In most contexts, **;** separates commands in a similar way to how Enter separates lines.
### Solution 
The following commands were executed to obtain the flag :
```bash 
hacker@chaining~chaining-with-semicolons:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/pwn ; /challenge/college
```


## Challenge 2: Your First Shell Script (Summary/Learning):  
shell scripts are frequently named with a sh suffix. 
we can write the commands to be executed within and then use *ctrl+o*, and *ctrl+x* to exit . This shell script can again be run by using the **bash** command . 
### Solution 
The following commands were executed to obtain the flag :
```bash 
hacker@chaining~your-first-shell-script:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ nano x.sh
hacker@chaining~your-first-shell-script:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cd ~
hacker@chaining~your-first-shell-script:~$ bash x.sh
```


## Challenge 3: Redirecting Script Output (Summary/Learning): 
One can redirect the output of a shell script by using **bash** command followed by All of the various redirection methods : > for stdout, 2> for stderr, < for stdin, >> and 2>> for append-mode redirection, >& for redirecting to other file descriptors, and | for piping to another command.
### Solution 
The following commands were executed to obtain the flag :
```bash 
hacker@chaining~redirecting-script-output:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cd ~
hacker@chaining~redirecting-script-output:~$ nano script.sh
hacker@chaining~redirecting-script-output:~$ bash x.sh | /challenge/solve
x.sh: line 3: syntax error near unexpected token `|'
x.sh: line 3: `|'
``` 


## Challenge 4: Executable Shell Scripts (Summary/Learning):  
We can use permissions learnt in the previous module to make your shell script file is executable and one can simply invoke it via its relative or absolute path.
### Solution 
The following commands were executed to obtain the flag :
```bash 
hacker@chaining~executable-shell-scripts:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cd ~
hacker@chaining~executable-shell-scripts:~$ nano x.sh
hacker@chaining~executable-shell-scripts:~$ chmod u+x /home/hacker/x.sh
hacker@chaining~executable-shell-scripts:~$ ~/x.sh
hacker@chaining~executable-shell-scripts:~$ cat x.sh
hacker@chaining~executable-shell-scripts:~$ ./x.sh
```
## <3