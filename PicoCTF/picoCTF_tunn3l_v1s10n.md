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

![image](https://github.com/user-attachments/assets/fe2d7ff7-cb5b-4928-b7af-39d351c9a57d)

There clearly seems to be more to the image, hence after referring to https://trailofbits.github.io/ctf/forensics/ . Had a brief Idea that indicated we maight have to tamper with the hexdump. 

## Solution
I went ahead with the `hexdump` command on Linux but the output wasnt controlled, so i started using https://hexed.it/ uploaded the initial Image 

![Screenshot (151)](https://github.com/user-attachments/assets/c1d32b51-9985-405a-b426-27ddfd193cde)

After observing the previous output, and tampering with the size of the image, specifically height (01->03) I made the following changes:

![Screenshot (153)](https://github.com/user-attachments/assets/44c8f825-3540-4ba1-a664-fa92b2a1e57e)

and uploading it to the Image viewer, we get :

![image-3](https://github.com/user-attachments/assets/7a69a660-e916-4b5a-aef3-6090d62dce6c)

where the flag is clearly visible as picoCTF{qu1t3_a_v13w_2020}
## <3
