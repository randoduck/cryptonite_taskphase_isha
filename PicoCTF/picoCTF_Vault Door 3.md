# Vault Door 3 

## Challenge 
*This vault uses for-loops and byte arrays. The source code for this vault is here: https://jupiter.challenges.picoctf.org/static/a648ca6dd275b9454c5d0de6d0f6efd3/VaultDoor3.java*

## Thought Process 
The challenge itself is tagged under Reverse engineering which itself is a big giveaway on how to proceed . 
In the program given .The program will ask for the vault password. You need to input a password in the flag format.The program processes the password and checks if it matches a scrambled version of the string: jU5t_a_sna_3lpm18gb41_u_4_mfr340.

**Series of loops have been used to scramble the password :**

-First 8 Characters:
buffer[i] = password.charAt(i) // The first 8 characters are copied as-is.

-Next 8 Characters ( 8 to 15):
buffer[i] = password.charAt(23 - i) // Characters are reversed from indices 15 to 8.

Next 16 Characters (Even elemtns ):
buffer[i] = password.charAt(46 - i) // Characters are pulled in reverse order for even indices.

Remaining Odd Indices (17 to 31):
buffer[i] = password.charAt(i) // Characters are copied as-is in reverse order.

## Solution 

To solve this, I created a C program that takes the input "jU5t_a_sna_3lpm18gb41_u_4_mfr340" and reverses the logic from the original Java code. In the Java program, the password undergoes a series of transformations: parts of the string are copied in reverse order or with certain intervals. I replicated this behavior in the C program by breaking the input into sections and rearranging the characters according to the same rules. Once the string is transformed, I print it in the format picoCTF{...}, which gives the flag picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_7f35db}. This way, the program mimics the password check and outputs the flag directly.

```c
#include <stdio.h>
#include <string.h>

void rev(char *input) 
{   char buffer[32];
    int i;

    // Copy first 8 characters
    for (i = 0; i < 8; i++) 
    {buffer[i] = input[i];}

    //  Copy characters from position 23 to 16 in reverse
    for (; i < 16; i++) 
    {buffer[i] = input[23 - i];}

    // Copy characters from position 46 to 32 in reverse with step of 2
    for (; i < 32; i += 2) 
    {buffer[i] = input[46 - i];}

    // Copy characters from position 31 to 17 in reverse with step of 2
    for (i = 31; i >= 17; i -= 2) 
    {buffer[i] = input[i];}
 
    for (i = 0; i < 32; i++)
    {printf("%c", buffer[i]);}}

int main() 
{    // Input password to reverse the string
  char input[] = "jU5t_a_sna_3lpm18gb41_u_4_mfr340";
    rev(input);
    return 0;
}
```

## Flag 
On running the program i get the string *jU5t_a_s1mpl3_an4gr4m_4_u_1fb380*
which I enclosed in the flag format and submitted. 

## <3