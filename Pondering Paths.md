# Pondering Paths

## Challenge 1 : The Root : Summary/Learnings:
In this challenge they introduce the concept of an absolute path.
An **absolute path** which starts from the root directory (`/`) and specifies the complete location of a file or program.
The Flag could be obtained by invoking **pwn** program using absolute path .
### Solution
The following command was executed to recieve the flag 
```bash
/pwn
```
## Challenge 2 : Program and Absolute Paths: Summary/Learnings:

We were required to invoke the program `run` which lives  in the `/challenge` directory,which is the  **absolute path**. Which is just a more advanced version of the challenge before 
### Solution
The following command was executed to obtain the flag :
```bash
/challenge/run
```

## Challenge 3 : Position Thy Self : Summary/Learnings:
Here they introduce the concept of `cd`which is used for navigating around the directories and changing into them. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument
we were required to collect the flag  by executing the `/challenge/run` program from a specific path

### Solution 
 we were required to change to a certain directory to run the commands .
 The following commands were executed to obtain the flag :
```bash 
cd usr/share/build-essential
 /challenge/run 
```
##  Challenge 4: Position Elsewhere : Summary/Learnings:
The path before the $ sign shows where you are currently loacted at .
we were required to obtain the flag by executing the `/challenge/run` program from a specific path . This required changing directories.

### Solution
we were required to change to a certain directory by running the commands :
```bash
cd /var
/challenge/run
```

## Challenge 5 : Position yet elsewhere : Summary/Learnings:

Again, another exercise similar to the previous one which requires changing directories to obtain the flag 

### Solution:
The following commands were executed to obtain the flag :
```bash 
/challenge/run
cd /etc
/challenge/run
```

## Challenge 6 : Implicit Relative Paths from /: Summary/Learnings:
Here they introduced the concept of **Relative Paths **for us  by defining it as 
A relative path is any path that does not start at root (/ is a root ).
A relative path is interpreted relative to your current working directory (cwd).
Your cwd is the directory that your prompt is currently located at.
we had to collect the flag by running `/challenge/run` using a relative path while having a current working directory of `/`
### Solution
To obtain the flag the following commands had to be executed :
```bash
cd /
challenge/run
```
## Challenge 7 : Explicit Relative Paths from /: Summary/Learnings:
This challenge made use of **.** as relative paths 
Every directory has two implicit entries that you can reference in paths: . and ... The first, ., refers right to the same directory.
To collect the flag by running `challenge/run` using `.` in the relative path while having a current working directory of `/` which is what the challenge tested us on .

### Solution
To obtain the flag the following commands were executed :
```bash
cd /
./challenge/run
```

## Challenge 8 : Implicit Relative Paths : Summary/Learnings:
 it was explained that Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. Here we tell Linux that we explicitly want to execute a program in the current directory, using . like in the previous levels.

### Solution

The flag was obtained after executing the following commands :
```bash
cd /challenge
./run
```
## Challenge 9 : Home Sweet Home : Summary/Learnings:
 It was told that the  `~` is shorthand for `/home/hacker`, which is home directory. 
To collect the flag by executing `/challenge/run` command by specifying a file path as an argument with the following constraints:
1. Your argument must be an absolute path.
2. The path must be inside your home directory.
3. Before expansion, your argument must be three characters or less in this case ( `~/` itself  )

### Solution
The following command was executed to obtain the flag 
```bash
/challenge/run ~/f
```

## <3