# Pondering PATH

## Challenge 1: The PATH Variable (Summary/Learning): 
We have been introduced to the **PATH** Variable here , a special shell variable, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands. Without a PATH, bash cannot find the ls command.
### Solution
The following commands were executed to obtain the flag :
```bash
hacker@path~the-path-variable:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ PATH " "
bash: PATH: command not found
hacker@path~the-path-variable:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ export PATH=""
hacker@path~the-path-variable:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{Quog1j_-XQp4W5sMDgTvrEoklcC.dZzNwUDL2ATM2czW}
hacker@path~the-path-variable:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ 

```


## Challenge 2: Setting PATH (Summary/Learning): 
We must be aware of the fact that  PATH stores a list of directories to find commands in and, for commands in nonstandard places, we must typically execute them via their path to obtain the flag .
### Solution
The following commands were executed to obtain the flag :
```bash
hacker@path~setting-path:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ export PATH=/challenge/more_commands
hacker@path~setting-path:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run win
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
``` 


## Challenge 3: Adding Commands (Summary/Learning):  
This challenge teaches us how to introduce our own commands into the ~ , using bash we write a script and export it by setting the path to **~** which enables us to directly execute the shell script
### Solution
The following commands were executed to obtain the flag :
```bash
hacker@path~adding-commands:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cd ~
hacker@path~adding-commands:~$ nano win.sh
hacker@path~adding-commands:~$  export PATH=/home/hacker:/run/workspace/bin:$/home/hacker/challenge/run/win
hacker@path~adding-commands:~$ chmod +x win.sh
hacker@path~adding-commands:~$  export PATH=/home/hacker:/run/workspace/bin:$/home/hacker/win.sh
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
/challenge/run: line 4: win: command not found
It looks like that did not work... Did you set PATH correctly?
hacker@path~adding-commands:~$ nano win
bash: nano: command not found
hacker@path~adding-commands:~$ cd ~
hacker@path~adding-commands:~$ nano win
bash: nano: command not found
hacker@path~adding-commands:~$  echo $PATH
/home/hacker:/run/workspace/bin:$/home/hacker/win.sh
hacker@path~adding-commands:~$ PATH='/home/hacker'
hacker@path~adding-commands:~$ export PATH=/home/hacker:$PATHd
hacker@path~adding-commands:~$ export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
hacker@path~adding-commands:~$ mv win.sh win
hacker@path~adding-commands:~$ chmod +x win
hacker@path~adding-commands:~$ export PATH=/home/hacker:$PATH
hacker@path~adding-commands:~$ /challenge/run
```


## Challenge 4: Hijacking Commands (Summary/Learning):
In this challenge we were required to create a bash script that overwrote the **rm** command and then set its path to home directory and also alter its permissions to make it readable and executable .   
### Solution
The following commands were executed to obtain the flag :
```bash
hacker@path~hijacking-commands:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cd ~
hacker@path~hijacking-commands:~$ nano rm.sh
hacker@path~hijacking-commands:~$ mv rm.sh rm
hacker@path~hijacking-commands:~$ chmod +rx rm
hacker@path~hijacking-commands:~$ which rm 
/run/workspace/bin/rm
hacker@path~hijacking-commands:~$ mkdir ~/mybin
hacker@path~hijacking-commands:~$ mv ~/rm ~/mybin/
hacker@path~hijacking-commands:~$ export PATH=~/mybin:$PATH
hacker@path~hijacking-commands:~$ which rm 
/home/hacker/mybin/rm
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
Found 'rm' command at /home/hacker/mybin/rm. Executing!
pwn.college{o9R7OWieRrcLdnFEsTeLMlnxkCO.ddzNyUDL2ATM2czW}
hacker@path~hijacking-commands:~$ 
```
## <3