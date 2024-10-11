 # Comprehending Commands

## Challenge 1:  Cat: Not The Pet, But The Command! (Summary/ Learning):
We have been introduced to the 'cat' command which reads the contents from the file given as an argument 
We must use the `cat` command to read the myflag file and obtain the flag from it .
### Solution
To obtain the flag we use the following command :
```bash
cat flag
```
## Challenge 2: Catting Absolute Paths (Summary/Learning):
To collect the flag by reading the flag file by its absolute path `/flag` using `cat` command 
`/flag` is where usually one can find flags in pwn.college
### Solution

To Obtain the flag the following command was used :
```bash
cat /flag
```

## Challenge 3:  More Catting Practice (Summary/Learning):
we could use the `cat` command to directly read what is in the flag file by specifying its path entirely 
hence we can collect the flag without using the `cd` command . 
### Solution
To Obtain the flag we must use the following command :
```bash
cat /usr/include/bsd/flag
```
## Challenge 4: Grepping For A Needle In A Haystack (Summary/Learning):
Certain files when you `cat`are too big, we then use the  grep command to search for the contents we need
we had to  collect the flag by reading the file `/challenge/data.txt` using `grep` command
we are aware of the fact that the flag will always start with the text pwm.college which shall now be used as an argument .
### Solution
To Obtain the Flag the following command must be entered :
```bash
grep pwn.college /challenge/data.txt
```

## Challenge 5 : Listing Files (Summary/Learning)
 we have now been introduced to the `ls` command, that will list all the files in the directory provided to it as argument. 
 In this challenge they have named ` /challenge/run` with some random name, and we must List the files in
  `/challenge` to find it.
### Solution
To Obtain the flag we must execute the following command :
```bash
ls /challenge
hacker@commands-listing-files:~$ ls /challenge
15153-renamed-run-4699 DESCRIPTION.md
/challenge/15153-renamed-run-4699 
```
## Challenge 6 : Touching Files (Summary/Learning):
We have now been introduced to the `touch` command which will be used to create files in specified directories , one can change directories using `cd`.
Here flag can be obtained by creating two files `/tmp/pwn` and `/tmp/college`, and running `/challenge/run`

### Solution
The following commands were executed to obtain the flag .
```bash
touch /tmp/pwn
touch /tmp/college
/challenge/run
```
## Challenge 7: Removing Files (Summary/Learning):
We have now been introduced to the `rm` command that is used to remove / delete the files from the directory .
We were supposed to obtain the flag  by deleting `delete_me` file from home directory and then run `/challenge/check`

### Solution
To obtain the flag the following commands have been executed:
```bash
rm delete_me
/challenge/check
```

## Challenge 8:  Hidden Files (Summary/Learning):
### Challenge
We have now been introduced to the ls argument `-a`. Since  files that start with a `.` don't show up by default in `ls` and to view them with ls, one can invoke ls with the `-a` flag
The flag can be obtained by accessing the  dot-prepended file in /.

### Solution
To Obtain the file , the following commands were executed ;
```bash
cd /
ls -a
cat .flag-184822641918524
```
## Challenge 9 : An Epic File System Quest (Summary/Learning):
To collect the flag which is hidden using the following instructions:
1. Your first clue is in /. Head on over there.
2. Look around with ls. There'll be a file named HINT or CLUE or something along those lines!
3. cat that file to read the clue!
4. Depending on what the clue says, head on over to the next directory (or don't!).
5. Follow the clues to the flag!

### Solution
 To obtain the flag the following commands were executed using `cd`, `ls` ,`ls -a`, `cat`

## Challenge 10 : Making Directories (Summary/Learning)
We have now been introduced to the `mkdir` command which is used for creating new directories . We are also aware that `touch` command can be used to make files . following the combination of these two the challenge can be handled by running `/challenge/run` after creating a `/tmp/pwn` directory and making a `college` file within the directory after changing into it .

### Solution
To obtain the flag , the following commands were executed :
```bash
mkdir /tmp/pwn
touch /tmp/pwn/college
/challenge/run
```
## Challenge 1: Finding Files (Summary/Learning):
We have now been introduced to the `find / -name` command which is used for searching a specific file or text within the file provided the path is given . We were supposed to find the flag hidden in the filesystem 

### Solution
The following commands were executed to obtain the flag and further `cat` command was used to check each file for the flag .
```bash
find / -name flag
```

## Challenge 12: Linking Files (Summary/Learning)
Here we've been introduced to concept of hard and soft links 
Links come in two flavors: hard and soft (also known as symbolic) links. We'll differentiate the two with an analogy:
->A hard link is when you address your appartment using multiple addresses that all lead directly to the same place 
-> soft link is when you move appartments and have the postal service automatically forward your mail from your old place to your new place.
symbolic links are created with the `ln` command with the `-s` argument .
We obtain the flag  which is in `/flag`, but `/challenge/catflag` will instead read out `/home/hacker/not-the-flag` so we make use of the `-s` argument 
### Solution
To obtain the flag , the follwoing commands have been passed: 
```bash
ln -s /flag /home/hacker/not-the-flag
/challenge/catflag
```
## <3