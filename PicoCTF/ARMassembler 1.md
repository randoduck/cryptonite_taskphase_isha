# ARM Assembler 1 

## Challenge Statement :
*For what argument does this program print `win` with variables 58, 2 and 3? File: chall_1.S Flag format: picoCTF{XXXXXXXX} -> (hex, lowercase, no 0x, and 32 bits. ex. 5614267 would be picoCTF{0055aabb})*
## Thought Process:
Here its clear that we'll be tinkering with assembly language. The problem statment says the variables 58, 2, 3, were used in the assembly program and are the variables to certain functions that seek an input from the user and print *"You win!"* for the right input. After examination of the file using the following commands:
```bash 
randoduck@DESKTOP-2PM3SNS:~$ wget https://mercury.picoctf.net/static/1c8d50e39cf00d144e6a72119f68c16c/chall_1.S
randoduck@DESKTOP-2PM3SNS:~$ aarch64-linux-gnu-gcc -o trail1 ./chall_1.S -static
randoduck@DESKTOP-2PM3SNS:~$ cat chall_1.S
```
On executing this we get the program in assembly langauge , i have commented all the lines describing thier execution which are crucial for understanding the flow.
```bash 
        .arch armv8-a # The target architecture ARMv8-A.
        .file   "chall_1.c"
        .text
        .align  2
        .global func
        .type   func, %function
func:
        sub     sp, sp, #32 - allocates 32 bytes on the stack 
        str     w0, [sp, 12] # stores the argument passed to func 
        mov     w0, 58
        str     w0, [sp, 16] # stores the value '58' at a stack offset of 16 
        mov     w0, 2
        str     w0, [sp, 20] # stores the value '2' at a stack offset of 20 
        mov     w0, 3
        str     w0, [sp, 24] # stores the value '3' at a stack offset of 24 
        ldr     w0, [sp, 20]
        ldr     w1, [sp, 16] # loads the values of '2' and '3' in w0 and w1 
        lsl     w0, w1, w0   # Performs a logical shift left (lsl) on w1 by w0 bits and stores the result at stack offset 28.
        str     w0, [sp, 28]
        ldr     w1, [sp, 28] # Loads values from stack offsets 28 and 24 into w1 and w0.
        ldr     w0, [sp, 24]
        sdiv    w0, w1, w0  # Performs signed division (sdiv) of w1 by w0 stores the result back at stack offset 28.
        str     w0, [sp, 28] # stores the result back at stack offset 28.
        ldr     w1, [sp, 28]
        ldr     w0, [sp, 12]
        sub     w0, w1, w0  # Subtracts w0 from w1 and stores the result back at stack offset 28.
        str     w0, [sp, 28]
        ldr     w0, [sp, 28]
        add     sp, sp, 32
        ret
        .size   func, .-func
        .section        .rodata
        .align  3
.LC0:
        .string "You win!" # This is the desired outcome , which would be printed if the Result of the function is 0 <3
        .align  3
.LC1:
        .string "You Lose :("
        .text
        .align  2
        .global main
        .type   main, %function
main:
        stp     x29, x30, [sp, -48]!
        add     x29, sp, 0
        str     w0, [x29, 28]
        str     x1, [x29, 16]
        ldr     x0, [x29, 16] 
        add     x0, x0, 8
        ldr     x0, [x0] # Loads argv[1] (the first command-line argument) into x0.
        bl      atoi #  atoi to convert the string to an integer.
assembly
Copy code 

        str     w0, [x29, 44]
        ldr     w0, [x29, 44]
        bl      func # Stores the integer result in the stack and passes it to func.
        cmp     w0, 0 # Compares the return value of func with 0 
        bne     .L4 # Branches to .L4 if not equal.
assembly
Copy code

        adrp    x0, .LC0 # continues execution and prints *You win!*
        add     x0, x0, :lo12:.LC0
        bl      puts
        b       .L6
.L4:
        adrp    x0, .LC1 #Loads the address of the string "You Lose :(" into x0 and calls puts.
        add     x0, x0, :lo12:.LC1
        bl      puts
.L6:
        nop
        ldp     x29, x30, [sp], 48
        ret
        .size   main, .-main
        .ident  "GCC: (Ubuntu/Linaro 7.5.0-3ubuntu1~18.04) 7.5.0"
        .section        .note.GNU-stack,"",@progbits
cat: 77: No such file or directory
```
## Solution :

After inspecting the structure of the assembly is clear and follows these steps;
- Logical Left Shift (constant value obtained )
- Division Operation 
- Subtraction ( the function argument comes to use here , the result of this fucntion is compared to 0)
### Logical Left Shift :
`
ldr w0, [sp, 20]  ; w0 = 2
ldr w1, [sp, 16]  ; w1 = 58
lsl w0, w1, w0    ; w0 = w1 << w0
`
58≪2=58×2^2=58×4=232
The result 232 is stored at stack offset 28.

### Division :
`ldr w1, [sp, 28]  ; w1 = 232 *its important to keep track of the values in w0, w1*
ldr w0, [sp, 24]  ; w0 = 3
sdiv w0, w1, w0   ; w0 = w1 / w0`
232÷3=77 as it is integer division 
The result 77 is stored back at stack offset 28.

### Subtraction :
`ldr w1, [sp, 28]  ; w1 = 77
ldr w0, [sp, 12]  ; w0 = input
sub w0, w1, w0    ; w0 = w1 - w0`

w0=77−X **Here X is the input we give and it must match with 0 for the program to print *You win!* and hence our X must be 77**

### Flag crafting : 

The ideal input i.e 77 must be converted into hex and then into 32 bit for which we use a python program. 
```python
>>> hex(77)
'0x4d'
```
following the flag protocol the flag obtained is picoCTF{0000004d}.

## <3
