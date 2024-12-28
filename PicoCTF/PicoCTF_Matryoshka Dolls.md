# Matryoshka Dolls

## Challenge 
*Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one? Image: this*
*Hint 1: Wait, you can hide files inside files? But how do you find them?*

## Thought Process 
Initially I thought This could be solved using Steghide but I realised Passkeys weren't given. On referring the Hint it was pretty clear that the challenge dealt with File carving . For this I used the `Binwalk` which confirmed the presence of multiple files in it . I went ahead and used the `binwalk -e dolls.jpg` which extracted the files to the directory I was in. After this followed series of navigation and changing into the directories and opening and extracting multiple jpg format photos

![Screenshot (198)](https://github.com/user-attachments/assets/a9fed177-a885-41a8-b359-73e56d13dfe1)

 finally obtained the flag : picoCTF{4f11048e83ffc7d342a15bd2309b47de}

 ## <3
