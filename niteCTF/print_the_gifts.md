# Print The Gifts 

## Challenge
*Santa has come with a lot of gifts, do not exploit his kindess unless you want to end up on the naughty list...* 
In this challenge we were provided with the following files:
Dockerfile
Dockerfile.selinux
chall

## Thought Process
After Inpecting the Binary file using GDB and using ncat link and connecting to the server was able to understand the flow of the program . Since we had string input it's seemed a favourable scenario for a Format String Vulnerability. I tried inputting a bunch of format strings, most were in vain but some leaked addresses. After further Tinkering it was found that:
- Read Memory: %p prints out values stored in the memory.
- Write to Memory: %n changes values in the  memory.

I got stuck here for a bit and searched up what one must do in this scenario one of the things I stumbled upon was `Return to Libc` attack . Considering we had the files required I gave it a shot, This was the resource I used:
https://www.youtube.com/watch?v=Gu_JGaWpcn4

Return to Libc attack : A **return-to-libc (ret2libc) attack** is a hacking technique where instead of writing new code, you make a program reuse its existing code in a library called **libc**. This library contains useful functions like `system`, which can run commands. The attacker tricks the program into "returning" to one of these functions (like `system("/bin/sh")`) by overwriting its return address in memory. This allows the attacker to execute commands, like opening a shell, without injecting new code.

We needed the stack addresses of `system` and `system("/bin/sh")`, for this I 
used `%p` and `gdb`. I believe this is where I made the Mistake because there were some difficulties in obtaining the address as well as crafting the payload which is where this hit a dead end . 

## Solution
After examining the right solution , Several new concepts have been used like ROP(Return Oriented Programming). The overall summary of the actual solution being :

**ROP (Return-Oriented Programming)** is a hacking technique where an attacker controls the flow of a program by chaining together small pieces of code, called **gadgets**, that already exist in the program or its libraries. Each gadget ends with a `ret` instruction, allowing the attacker to "return" to the next gadget in their chain. By carefully arranging these gadgets, the attacker can perform complex tasks, like executing functions or bypassing security measures, without injecting new code. It's commonly used to exploit programs with protections like non-executable memory (DEP/NX).

- The program uses a library called libc, which has a lot of useful tools like system (a function that runs commands) and the string /bin/sh (used to open a shell).

We need to find where libc is located in the robot's memory. To do this we used gdb and fromat strings to find the address and offset . 

- Leak Stack Address
Next, we need to figure out where the robot stores its return address (the place it goes back to after finishing a task). To do this:
We send %p to leak an address from the robot's stack (a part of memory where it keeps temporary data).
We add an offset (0x21a8) to find the exact place where we need to insert our instructions.

- Build a Plan (ROP Chain)
Now we need to tell the robot what to do. We want it to:

- Run the system function from libc.
Pass /bin/sh as the command to open a shell.
To do this:
We create a ROP chain (a list of instructions for the robot).
We include a "ret" gadget to align the robot's thinking (technical detail) before calling system.

- Overwrite the Robot’s Memory
The robot’s memory is like a long list of boxes. The return address is in one of these boxes. To take control:
We split our ROP chain into small chunks (2 bytes each).
Using %n, we overwrite the return address box by box with our ROP chain.
This step is like sneaking instructions into the robot’s brain one tiny piece at a time.

- Trigger the Shell
Once all the instructions are in place:
We send a harmless input (like a) to make the robot finish its current task.
The robot’s brain follows our instructions and opens a shell where we can run any command. 
*cat flag.txt*

I'll need to dive deeper into ROP - ROP chains but this was overall a Great Learning curve. And my approach Return to Libc wasn't too far from the actual Solution . 

## <3