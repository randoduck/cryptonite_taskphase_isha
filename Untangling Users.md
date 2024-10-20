# Untangling Users 

## Challenge 1: Becoming Root with su (Summary/ Learning):
One can easily become root user or switch between users using the **su** command . This command will require you to input password as well. **su** is a setuid binary.Because it has the SUID bit set, su runs as root. Running as root, it can start a root shell! Of course, su is discerning: before allowing the user to elevate privileges to root, it checks to make sure that the user knows the root password.
### Solution 
The flag was obtained by executing the following commands :
```bash 
hacker@users~becoming-root-with-su:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ ls -l
total 12
hacker@users~becoming-root-with-su:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ su
Password: 
root@users~becoming-root-with-su:/usr/local/lib/python3.8/dist-packages/pwnlib/flag# cat /flag 
```


## Challenge 2: Other Users with su  (Summary/ Learning):
We have been introduced to arguments of **su** here , With no arguments, su will start a root shell (after authenticating with root's password). One also give a username as an argument to switch to that user instead of root.
### Solution 
The flag was obtained by executing the following commands :
```bash 
su zardus 
password : dont-hack-me
/challenge/run
```


## Challenge 3: Cracking Passwords (Summary/ Learning):
the /etc/shadow command used to previously store passwords . Now The cracking can be done via the famous John the Ripper command : john 
### Solution 
The flag was obtained by executing the following commands :
```bash 
hacker@users~cracking-passwords:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ su zardus
Password: 
su: Authentication failure
hacker@users~cracking-passwords:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ john /challenge/shadow-leak
Loaded 1 password hash (crypt, generic crypt(3) [?/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:10 99% 1/3 0g/s 282.9p/s 282.9c/s 282.9C/s zardus999991915..999991900
0g 0:00:00:14 0% 2/3 0g/s 283.2p/s 283.2c/s 283.2C/s serena..88888888
0g 0:00:00:19 1% 2/3 0g/s 285.2p/s 285.2c/s 285.2C/s ncc1701d..1022
aardvark         (zardus)
1g 0:00:00:20 100% 2/3 0.04897g/s 285.1p/s 285.1c/s 285.1C/s Johnson..buzz
Use the "--show" option to display all of the cracked passwords reliably
Session completed
2 password hashes cracked, 0 left
hacker@users~cracking-passwords:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ su zardus
Password: 
zardus@users~cracking-passwords:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ cat /flag
cat: /flag: Permission denied
zardus@users~cracking-passwords:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ su zardus 
Password: 
zardus@users~cracking-passwords:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ /challenge/run
``` 


## Challenge 4: Using sudo (Summary/ Learning):
We have been introduced to the more popular command **sudo** . The main difference being unlike su, which defaults to launching a shell as a specified user, sudo defaults to running a command as root.
### Solution
The flag was obtained by executing the following commands :
```bash 
hacker@users~using-sudo:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ sudo cat /flag
pwn.college{QCPealSnyoXaqh5adlL_wLM9Gbu.dhTN0UDL2ATM2czW}
hacker@users~using-sudo:/usr/local/lib/python3.8/dist-packages/pwnlib/flag$ 

```  
## <3