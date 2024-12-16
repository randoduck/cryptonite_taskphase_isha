
# CTF Challenge: Gaining Admin Access to the Chat System

## Challenge Description
The prompt was: 
*"Someone has taken over my chat system and is preventing me from logging in. Can you try to log in as me and gain access back to admin mode?"*

## Initial Thought Process
When I first saw the challenge, my initial thought was to try and exploit the system by performing a **buffer overflow**. A buffer overflow is a common vulnerability where writing more data than the allocated memory can lead to unexpected behavior, such as overwriting critical memory areas. 

I began by examining the binary and testing the first input field that uses `fgets`. However, the input length was restricted to 11 bytes (`fgets(local_38, 0xb, stdin)`), making a buffer overflow here unlikely. 

Next, I analyzed the admin access mechanism in the code. It seemed like the program compares the first input with the string `"spiderdrive"`. If this comparison succeeds, admin privileges are granted via the `strncmp` function. However, simply entering `"spiderdrive"` directly wouldn't work, as the program exits with a "HAha cant let you in" message.

I realized I needed a more sophisticated approach to exploit the system and seize admin control.

---

## Solution Walkthrough

### Step 1: Understanding the Program Structure
From analyzing the binary, I identified the following key functionality:
1. **New Message** (Option 1): Allocates memory using `malloc`.
2. **Delete Message** (Option 2): Frees memory using `free`.
3. **Write Message** (Option 3): Writes user input to an allocated chunk.
4. **Admin Mode** (Option 4): Grants admin privileges if the input string matches `"spiderdrive"`.
5. **Exit** (Option 5): Exits the program.

---

#### *Why Buffer Overflow Doesn't Work**
A **buffer overflow** occurs when you input more data than a buffer can hold, allowing you to overwrite adjacent memory. Here's why it doesn't work in this case.
Input Restrictions:
The vulnerable buffer (`local_38`) is allocated with a size of 12 bytes (`char local_38[12]`), and `fgets` is used to read input:
```c
fgets(local_38, 0xb, stdin);
```
- The `0xb` (11 in decimal) restricts input to **11 characters**, leaving no room to overflow into adjacent memory.
- and`fgets` appends a null terminator (`\0`), which further limits overflow attempts.
 
Moreover , Even if a buffer overflow was possible, there’s no critical memory (e.g., return addresses or function pointers) adjacent to `local_38` in this program. Overwriting it wouldn’t help achieve admin access or gain shell access.
**format string exploit**
works by crafting malicious input for functions like `printf` to manipulate memory. In this case there is a format string vulnerability in this challenge (`printf(local_38)`) but we can only use it for **leaking addresses**, not directly overwriting memory.
After further Research I discovered this was beacuse of Limited Write Capabilities in format string, 
The format string vulnerability in `printf` can read memory (e.g., `%p` to leak pointers), but it cannot directly write to arbitrary memory. This is because the program does not use functions like `fprintf` or `%n` (which could be used to write values to memory).
The stack layout is not exploitable because the vulnerable buffer (`local_38`) is too small and far from critical elements like the return address or saved registers. Specifically:  The return address is stored in `local_20`, which is 0x20 bytes (32 bytes) away from the start of `local_38`. Even if the buffer could overflow, the gap is too large to overwrite the return address. One could figure this out using  `gdb`, I inspected the stack layout, hence confirmed that the stack layout is safe from exploitation in this context.
---

#### **Why Heap Exploitation is the Best Option**
The Learning comes here `heap exploitation` is what needs to be executed to capture that , here is the what , how and why :
A Stack is used for storing local variables and function information, the heap is used for memory that is allocated at runtime and used for fucntions like `malloc`, `calloc` or `new` in C.
attackers exploit weaknesses in how memory is managed to overwrite data, control the program's behavior, or access restricted areas. Common methods include heap overflow (writing too much data into a chunk), use-after-free (accessing memory after it's been freed), and tcache poisoning (tricking the memory allocator into giving the attacker control over memory).
Instead of targeting the stack or using a format string exploit directly, the **heap** is a better target due to the program's reliance on dynamic memory allocation (`malloc` and `free`). Here's why heap exploitation works:
- The program uses a **tcache** (a memory allocator optimization) that is vulnerable to poisoning.
- By carefully freeing and reallocating chunks, we can manipulate the heap to redirect allocations to a specific memory address (e.g., the stack buffer).
- This allows us to bypass the admin check by writing `"spiderdrive"` directly to the buffer .

### Step 2: Finding Stack and Heap Addresses:
1. **Stack Leak**: The first input is printed back to us using `printf(local_38)`. By exploiting a  format string vulnerability, one can leak a stack address.
   - Payload: `"%p"` (prints a pointer from the stack).
   - The leaked address gives us a stack pointer (`stack_addr`).

2. **Heap Leak**: After freeing a chunk, one can the write message function (Option 3) with another format string payload to leak a heap address.
   - Payload: `"%p %p %p"` (leaks multiple pointers, with the third being the heap address of the freed chunk).
   - This gives us the heap pointer (`heap_leak`).

### Step 3: Calculating the Buffer Address
The `stack_addr` we leaked is used to calculate the address of the target buffer. From debugging the binary, determined that the buffer is located at an offset of `0x2130` from the leaked stack address:
```c
buffer_addr = stack_addr - 0x2130;
```
### Step 4: Setting Up Tcache Poisoning
With both the stack and heap addresses in hand, one can proceed to poison the tcache. This involved the following steps:

Create Two Chunks: Use Option 1 (malloc) to allocate two chunks.
Free Both Chunks: Use Option 2 (free) to deallocate the chunks, placing them into the tcache.
Step 5: Poisoning the Tcache
To redirect allocations, one must write a crafted payload to overwrite the pointer in the tcache. This payload forces the next allocation to point to the target buffer address:

```python
payload = p64(stack_addr ^ (heap_leak >> 12))
```
The XOR operation ensures the addresses align correctly with glibc's security checks.

### Step 6: Redirecting Allocation to the Buffer
After poisoning the tcache, create two new chunks using Option 1. Due to the poisoned tcache entry, the second allocation now pointed to the buffer address on the stack.

### Step 7: Writing "spiderdrive" to the Buffer
With the pointer redirected to the buffer, we can use Option 3 to write the string "spiderdrive" directly to the buffer. This bypassed the strncmp check for admin access.

### Step 8: Gaining Admin Access
Finally, select Option 4 (Admin Mode). Since the buffer now contained "spiderdrive", the program granted admin access and opened a shell.

### Final Step: Capturing the Flag
With shell access,execute the command:
```bash
cat flag.txt
```
This reveals the flag and completes the challenge!
## <3