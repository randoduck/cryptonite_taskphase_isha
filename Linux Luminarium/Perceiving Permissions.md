# Perceiving Permissions

## Challenge 1: Changing File Ownership (Summary/Learning):
Here we have been introduced to the concept of changin ownerships , typically only the root user can change ownerships . This can be done using **chown**. This challenge tests us on the same concept.
### Solution:
The following commands were executed to obtain the flag :
```bash
hacker@permissions~changing-file-ownership:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ ls -l
hacker@permissions~changing-file-ownership:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ chown hacker /flag
hacker@permissions~changing-file-ownership:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cat /flag

```


## Challenge 2: Groups and Files (Summary/Learning):
It's been stated that Files have both an owning user and group. A group can have multiple users in it, and a user can be a member of multiple groups. One can check which groups they are in using the **id** command.
group ownership can be changed with the **chgrp** command (change group).
### Solution:
The following commands were executed to obtain the flag :
```bash
hacker@permissions~groups-and-files:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ ls -l /flag
-r--r----- 1 root root 58 Oct 19 12:43 /flag
hacker@permissions~groups-and-files:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ chgrp hacker /flag
hacker@permissions~groups-and-files:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cat /flag

```


## Challenge 3: Fun with Group Names (Summary/Learning):
This challenge deals with similar concepts introduced to us in the previous challenge. We must make use of **chgrp** to obtain the flag. 
### Solution:
The following commands were executed to obtain the flag :
```bash
hacker@permissions~fun-with-groups-names:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ ls -l
hacker@permissions~fun-with-groups-names:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ id
uid=1000(hacker) gid=1000(grp2306) groups=1000(grp2306)
hacker@permissions~fun-with-groups-names:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ chgrp grp2306 /flag
hacker@permissions~fun-with-groups-names:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cat /flag
```


## Challenge 4: Changing Permissions (Summary/Learning):
We've been introduced to the concept of **chmod**.
The first 9 string of characters when you use the **ls -l** command indicate the permissions.  split into 3 characters denoting permissions for the owning user , 3 characters denoting the permissions for the owning group and 3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file. Where :
r - user/group/other can read the file (or list the directory)
w - user/group/other can modify the files (or create/delete files in the directory)
x - user/group/other can execute the file as a program (or can enter the directory, e.g., using `cd`)
- - nothing 
### Solution:
The following commands were executed to obtain the flag :
```bash
hacker@permissions~changing-permissions:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ chmod ugo+r /flag
hacker@permissions~changing-permissions:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cat /flag
pwn.college{QvfhrEWsQg9mkihTEJ6WmUBP-dn.dNzNyUDL2ATM2czW}

```


## Challenge 5: Executable Files (Summary/Learning):
Challenge tests us on the topics that have been introduced previously !
### Solution:
The following commands were executed to obtain the flag :
```bash
hacker@permissions~executable-files:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ chmod ugo+x /challenge/run
hacker@permissions~executable-files:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
Successful execution! Here is your flag:
pwn.college{U2tK5tBj-n_F49WCX0xpUXptQZG.dJTM2QDL2ATM2czW}
hacker@permissions~executable-files:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ 
```


## Challenge 6: Permission Tweaking Practice (Summary/Learning):
In this challenge we had to go through 8 rounds of testing on topics introduced to us in this module in order to capture the flag 


## Challenge 7: Permission Setting Practice (Summary/Learning):
Similar to the previous challenge, here also we were required to go through 8 rounds of testing to capture the flag , only difference being the **=** operator was introduced which is used to overwrite the read, write and execute with new permissions .


## Challenge 8: The SUID Bit (Summary/Learning):
Here we have been introduced to the concept of SUID ("Set User ID) which basically bit allows the user to run a program as the owner of that program's file. One can set a file's SUID using ** chmod** by 
**chmod u+s [program]**
### Solution:
The following commands were executed to obtain the flag :
```bash
hacker@permissions~the-suid-bit:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ ls -l
hacker@permissions~the-suid-bit:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ chmod u+s /challenge/getroot
hacker@permissions~the-suid-bit:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/getroot
SUCCESS! You have set the suid bit on this program, and it is running as root! 
Here is your shell...

```
## <3
