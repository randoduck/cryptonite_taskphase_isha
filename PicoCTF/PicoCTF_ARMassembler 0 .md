# ARM assembler 0

## Challenge :
What integer does this program print with arguments 1765227561 and 1830628817? File: chall.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})

## Solution
```bash 
randoduck@DESKTOP-2PM3SNS:~$ mv /mnt/c/Users/admin/Downloads/chall.S ~
randoduck@DESKTOP-2PM3SNS:~$ mv chall.S asemt 
randoduck@DESKTOP-2PM3SNS:~$ sudo apt install qemu-user 
randoduck@DESKTOP-2PM3SNS:~$ qemu-aarch64 ./trail 65 34
Result: 65 # After inspecting the code , it appears to be a max fucntion 
randoduck@DESKTOP-2PM3SNS:~$ python3
Python 3.12.3 (main, Nov  6 2024, 18:32:19) [GCC 13.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> hex(1830628817) # Max number hence this the desired result converted to hex to fit the flag format 
'0x6d1d2dd1'
>>>
randoduck@DESKTOP-2PM3SNS:~$ picoCTF{6d1d2dd1} # The flag 
```
## <3