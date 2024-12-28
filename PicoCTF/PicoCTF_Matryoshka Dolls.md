# Matryoshka Dolls

## Challenge 

## Thought Process 
Initially I thought This could be solved using Steghide but I realised Passkeys weren't given. On referring the Hint it was pretty clear that the challenge dealt with File carving . For this I used the `Binwalk` which confirmed the presence of multiple files in it . I went ahead and used the `binwalk -e dolls.jpg` which extracted the files to the directory I was in. After this followed series of navigation and changing into the directories and opening and extracting multiple jpg format photos






 finally obtained the flag : picoCTF{4f11048e83ffc7d342a15bd2309b47de}

 ## <3