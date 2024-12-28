# HEAP 0

## Challenge
*Are overflows just a stack concern?*
*Download the binary and source here*

## Thought Process 
So clearly from the Title of challenge, we could figure out it has to do something with Heaps and thus I began to do a little bit of Ground work on Heaps. Here are the sources I referred to: 
https://youtu.be/5OJRqkYbK-4?si=m64ajAbA-pSn6ygd

one of the key take aways was just like how can one perform Stack Overflow or Buffer Overflow we can also execute Heap Overflow which shares quite a few similarities with the former .

Here after going through the code carefully we find 'scanf' taking in Data without checking it's size and only stopping after enter is pressed. So this could be our location of exploit . But to construct a payload we must be aware of the Location we are at as well as the Location we want to overwrite with the Buffer and input data that *just* exceeds the size . 
Luckily we have been given Both the Memory Locations at the Input. The source also tells us flag can only be obtained If the modification of `safe_var` takes place . 
We'll get into some Calculations now 

0x63c3882552d0-> 109,691,453,919,952
0x63c3882552b0-> 109,691,453,919,920

On subtracting we get that The current memory Location and the desired memory location are 
32 bytes away . Hence, we need 33 bytes of Input through scanf to overflow the Heap.

A 33-byte string would consist of 33 characters, where each character is represented by 1 byte. In hexadecimal notation, each byte is represented by 2 characters (since 1 byte = 8 bits = 2 hex digits). Thus, a 33-byte string in hexadecimal would contain 66 hex digits.

So an Example Payload would be : 
`0x11223344556677889900aabbccddeeff00112233445566778899aabbccddeeff00`.

After injecting this Payload and going with Option 4 as the Menu Choice we get the flag as : 

picoCTF{my_first_heap_overflow_749119de}

## <3
