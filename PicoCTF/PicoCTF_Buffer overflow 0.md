# PicoCTF - Buffer Overflow 0 
## Problem Statement 
Description
"Let's start off simple, can you overflow the correct buffer? The program is available here. You can view source here." We've been given a program in C to analyse .

After Launching the instance we get this command prompt:
```bash
nc saturn.picoctf.net 61223
```

## Thought Process 

Given that Buffer Overflow 0 is categorised under Binary Exploitation . It was important that i know what  the concept deals with , so after research found out that:
 Binary exploitation is a technique used in cybersecurity to manipulate or exploit vulnerabilities within compiled binary programs (executables) to gain unauthorized access, control, or escalate privileges within a system. It often targets flaws or weaknesses in the way a program handles data, memory, or specific instructions, allowing attackers to influence program execution in unintended ways. Buffer overflow the concept in question is classified under Memory corruption Vulnerabilities . Buffer Overflow Occurs when more data is written to a buffer (memory allocated for temporary data storage) than it can handle, leading to data overwriting adjacent memory, which can corrupt or manipulate program behavior. 

After careful inspection of the program , we seem to get an idea of where exactly there is a chance of a buffer overflow , here its specified that it can only take in 16 bytes of data safely .
```bash
void vuln(char *input){
  char buf2[16];
```
```bash 
  printf("Input: ");
  fflush(stdout);
  char buf1[100];
  gets(buf1); 
  vuln(buf1);
  printf("The program will exit now\n");
```
Hence the goal is to give an input that would trigger the buffer overflow , generate a segmentation fault and see how it goes from there. On our terminal we start off by executing the command prompt provided to connect to the netcat server . 

```bash
randoduck@DESKTOP-2PM3SNS:~$ nc saturn.picoctf.net 64790
g info: [u:697772 e: p: c:257 i:296078]Input: RANDODUCKLIKESBERRIESALOT
picoCTF{ov3rfl0ws_ar3nt_that_bad_ef01832d}
```
It's evident when the Input is asked we could overflow it by providing an input larger specified and easily obtain the flag . 

## <3
