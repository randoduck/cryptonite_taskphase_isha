# PicoCTF_GDB_BabyStep1

## Problem Statement:
"Can you figure out what is in the eax register at the end of the main function? Put your answer in the picoCTF flag format: picoCTF{n} where n is the contents of the eax register in the decimal number base. If the answer was 0x11 your flag would be picoCTF{17}.
Disassemble this."
HINT 1: gdb is a very good debugger to use for this problem and many others!
HINT 2: main is actually a recognized symbol that can be used with gdb commands.

## Thought Process
From the above Problem statement and the hints given , it was clear that the flag was hidden in the eax register . Which could be obtained by using the main function in gdb . gdb stands for GNU Debugger . It helps to Run your program with specific arguments or environment variables, pause the execution at specific points (breakpoints) or when certain conditions are met,Resume execution after pausing eyc. After finding out more about gdb using info, i was able to execute my commands properly . 

## Solution
Initially the file provided debugger0_a was only available on my os, so using commands like **mv** i was able to move them into my directories like this :
```bash
randoduck@DESKTOP-2PM3SNS:~$ mkdir -p ~/picoctf/workspace
randoduck@DESKTOP-2PM3SNS:~$ mv /mnt/c/Users/admin/Downloads/debugger0_a ~/picoctf/workspace
```
After certain Hit and trails and executing the following commands I was able to obtian the flag :
```bash
randoduck@DESKTOP-2PM3SNS:~$ cd picoctf
randoduck@DESKTOP-2PM3SNS:~/picoctf$ ls
workspace
randoduck@DESKTOP-2PM3SNS:~/picoctf$ cd workspace
randoduck@DESKTOP-2PM3SNS:~/picoctf/workspace$ ls
debugger0_a
randoduck@DESKTOP-2PM3SNS:~/picoctf/workspace$ file debugger0_a
debugger0_a: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=15a10290db2cd2ec0c123cf80b88ed7d7f5cf9ff, for GNU/Linux 3.2.0, not stripped
randoduck@DESKTOP-2PM3SNS:~/picoctf/workspace$ gdb debugger0_a
Command 'gdb' not found, but can be installed with:
sudo apt install gdb
randoduck@DESKTOP-2PM3SNS:~/picoctf/workspace$ sudo apt install gdb
[sudo] password for randoduck:

randoduck@DESKTOP-2PM3SNS:~/picoctf/workspace$ gdb debugger0_a
GNU gdb (Ubuntu 15.0.50.20240403-0ubuntu1) 15.0.50.20240403-git
Copyright (C) 2024 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from debugger0_a...
(No debugging symbols found in debugger0_a)
(gdb)
(gdb)
(gdb) set disassembly flavour intel
Undefined item: "flavour".
(gdb) disassemble main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   %rbp
   0x000000000000112e <+5>:     mov    %rsp,%rbp
   0x0000000000001131 <+8>:     mov    %edi,-0x4(%rbp)
   0x0000000000001134 <+11>:    mov    %rsi,-0x10(%rbp)
   0x0000000000001138 <+15>:    mov    $0x86342,%eax
   0x000000000000113d <+20>:    pop    %rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
(gdb) print 0x86342
$1 = 549698
(gdb)
```
hence the flag captured is : picoCTF{549698}
## <3