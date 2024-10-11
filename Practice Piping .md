# Practising Piping

## Challenge 1: Redirecting Output (Summary/Learning)

we have been introduced to a new character `>`, which is used to redirect stdout to files. Thus if I use `>` between `echo PWN` and `COLLEGE`, I'll be able to complete the challenge where to obtain the flag 
we must write the word PWN to the filename COLLEGE using `>`
### Solution
The following commands were executed to obtain the flag :
```bash
echo PWN > COLLEGE
```
## Challenge 2 : Redirecting More Output (Summary/Learning)

 We again make use of `>` as learnt in the previous challenge and here we redirecting the output of `/challenge/run` to the file `myflag`, to obtain the flag

### Solution

The following commands were executed to obtain the flag :
```bash
/challenge/run > myflag
cat myflag
```

## Challenge 3: Appending Output (Summary/Learning):

Here we are introduced to the concept of `>>` which goves the output of a bunch of commands to keep appending to the same file since `>` will create a new output file every time, deleting the old contents.
we obtain the flag by running `/challenge/run` with an append-mode redirect of the output to the file /home/hacker/the-flag

### Solution

The following commands were executed to obtain the flag :
```bash
 /challenge/run >> /home/hacker/the-flag
cat /home/hacker/the-flag
```

## Challenge 4 : Redirecting Error (Summary/Learning):

 Here we've been introduced to a new  File Descriptor numbers .
 A File Descriptor (FD) is a number the describes a communication channel in Linux. You've already been using them, even though you didn't realize it. We're already familiar with three:

FD 0: Standard Input
FD 1: Standard Output
FD 2: Standard Error
When you redirect process communication, you do it by FD number, though some FD numbers are implicit. For example, a > without a number implies 1>, which redirects FD 1 (Standard Output). Thus, the following two commands are equivalent:
we must obtain the flag  by redirecting the output of `/challenge/run`, to `myflag` and the errors  to `instructions`

### Solution

The following commands were executed to obtain the flag :
```bash
/challenge/run > myflag 2> instructions
cat myflag
```
## Challenge 5 :Redirecting Input (Summary/Learning):

Here we are introduced to a new character `<` which is used to redirect input into programs .
To collect the flag by redirecting the PWN file to `/challenge/run` and have the PWN file contain the value COLLEGE and then redirect its value to `/challenge/run`

### Solution

The following commands were executed to obtain the flag :
```bash
echo COLLEGE > PWN
/challenge/run < PWN
```

## Challenge 6: Grepping Stored Results (Summary/Learning)

Here we use the `>` once again .  redirecting of the output can be done using `>` and searching through the resulting file using `grep`
To collect the flag by following the given instructions:
1. Redirect the output of `/challenge/run` to `/tmp/data.txt`
2. This will result in a hundred thousand lines of text, with one of them being the flag, in `/tmp/data.txt`
3. Grep that for the flag!

### Solution

The following commands were executed to obtain the flag :

```bash
/challenge/run > /tmp/data.txt
grep "pwn.college" /tmp/data.txt
```
## Challenge 7 : Grepping Live Output (Summary/Learning)

Here we have been introduced to pipe operator `|` where standard output from the command to the left of the pipe operator will be connected to (piped into) the standard input of the command to the right of the pipe.   To obtain the flag we must use  use `|` (pipe) operator between `/challenge/run` and `grep` and we know we grep pwn.college

### Solution

The following commands were executed to obtain the flag :
```bash
/challenge/run | grep pwn.college 
```
## CHallenge 8 : Grepping Errors (Summary/Learning)
There is a convenient way to use the pipe operator and also grep the errors of a a file this can be done by 
 redirecting  standard error to standard output ` (2>& 1)` and then pipe the now-combined stderr and stdout as normal (`|`)

### Solution
The following commands were executed to obtain the flag :
```bash
/challenge/run 2>&1 | grep "pwn.college"
```
## Challenge 9: Duplicating Piped Data With Tee (Summary/Learning)
We have been introduced to the `tee ` command . `tee` command duplicates data flowing through your pipes to the files specified o the command line . we cna use `tee` to intercpet data to store the values before any changes are made . To Obtain the flag we must pipe  `/challenge/pwn` into `/challenge/college` after intercepting the data to see what pwn needs from you.

### Solution
The following commands were executed to obtain the flag :
```bash
/challenge/pwn | tee code | /challenge/college
cat code
Usage: /challenge/pwn-secret [SECRET_ARG]
SECRET_ARG should be "kNkC3zyg"
/challenge/pwn--secret kNkC3zyg | /challenge/college
```

## Challenge 10 : Writing To Multiple Programs (Summary/Learning)

we make use of process substituion along with the command tee to dublipcate the output of a file . Here to obtain the flag we must run  `/challenge/hack` and duplicating its output as input to both the `/challenge/the` and the `/challenge/planet` commands

### Solution
The following commands were executed to obtain the flag :

```bash
/challenge/hack | tee >( /challenge/the ) >( /challenge/planet )
```
## Challenge 11:  Split - Piping Stderr And Stdout (Summary/Learning)

To collect the flag by combining the usage of `>()`, `2>`, and `|` with the following:
- `/challenge/hack`: this produces data on stdout and stderr
- `/challenge/the`: you must redirect hack's stderr to this program
- `/challenge/planet`: you must redirect hack's stdout to this program

In order to redirect stderr of `/challenge/hack` using  `2>` using  `>()` to feed the `stderr` output into `/challenge/the`. After that `|` operator should be used to pipe stdout of `/challenge/hack` into `/challenge/planet`

### Solution
The following commands were executed to obtain the flag :
```bash
/challenge/hack 2> >( /challenge/the ) | /challenge/planet
```
## <3