# tunn3l_v1s10n

## Challenge
*We found this file. Recover the flag.* 
Hint : *Weird that it won't display right...*

## Thought Process
First instict should be, and was to examine the file type but it wasnt very helpful as it just displayed `data`. So then i tried to print out the contents of the flag as there is a possibility of file carving, the file was too long hence i went with `head` command to print out the first 10 lines of the file .

```bash
randoduck@DESKTOP-2PM3SNS:~$ head tunnel
BM&,n2X&,%%#'1(%5,)3*'8/,/&#3*&-$ ;2.2)%0'#3*&8,(6+'9-+/&##)U=1vffRmVpXoToT~cmiȗq��q��t��s��r��onkjdtUwZoVvR:qR=lO@mRDnSIw^TS93pXRvaYs_T~k^t4$M6'J3$F, H."F."D."<& 02#6'<+">+$B,&^D>fLF63?0-)P:/K5*?)B.#K7,E1&?+ C/$C/$@*H2'K2(G.$@'E,"L4(L4(K3'J2&L2$N4
```
The first two letters clearly indicate its a Bitmap file, i.e it contains an image. Hence attempts were made to upload it to a image viewer (https://image-viewer.com/)


There clearly seems to be more to the image, hence after referring to https://trailofbits.github.io/ctf/forensics/ . Had a brief Idea that indicated we maight have to tamper with the hexdump. 

## Solution
I went ahead with the `hexdump` command on Linux but the output wasnt controlled, so i started using https://hexed.it/ uploaded the initial Image 


After observing the previous output, and tampering with the size of the image, specifically height (01->03) I made the following changes:


and uploading it to the Image viewer, we get :

where the flag is clearly visible as picoCTF{qu1t3_a_v13w_2020}
## <3