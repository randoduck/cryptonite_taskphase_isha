# HEAP 1

## Challenge 
Similar to Heap 0, this also demands the execution of Heap overflow 

## Thought Process 
This time we have been provided with a new memory address called bico. On inspection of the source it is found that the flag is only revealed to us if `safe_var` is modified from bico to pico. My first thought was to replicate what I did previously and calculated the bytes . On subtracting it is found that they are indeed 32 bytes away . keeping this in mind i Created a 32 bytes payload with the word 'pico' appended in the end . 

```bash 
abcdefghijklmnopqrstuvwxyz1234pico
```
On entering option 4 , it did not give me the flag like it usually should . Hence I checked in with the `print the safe_var` option 3. which printed just `co` in Return .

## Solution 

The next immediate step I executed was to increase the Payload size by the deficient amount.

```bash
abcdefghijklmnopqrstuvwxyz123456pico
```
cross checked the overwritten value, which turned out to be pico and then went ahead to get the flag.

picoCTF{starting_to_get_the_hang_21306688}

## <3

