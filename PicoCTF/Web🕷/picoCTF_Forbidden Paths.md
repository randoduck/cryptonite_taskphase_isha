# Forbidden Paths 

## Challenge 
*Can you get the flag?
We know that the website files live in /usr/share/nginx/html/ and the flag is at /flag.txt but the website is filtering absolute file paths. Can you get past the filter to read the flag?
Additional details will be available after launching your challenge instance.*

## Thought Process / Solution 
This Challenge clearly makes use of the concept of paths which are of two types : absolute paths and relative paths . Absolute paths provide the full location of a file starting from the root directory, such as /home/user/file.txt, and are independent of the current directory. In contrast, relative paths specify a file’s location based on the current directory, using shortcuts like . (current) and .. (parent). For example, ../file.txt moves up one level to access a file. Absolute paths are fixed, while relative paths are flexible and depend on the user's location.After launching the website this is what it looked like :
![image](https://github.com/user-attachments/assets/6f723f22-0730-4915-bee9-a31b9a9a8a2b)

We've been given an input box to tamper with and we've also been given the path where the flag resides :
Attempt 1: /usr/share/nginx/html/flag.txt -> *not authorised*
Attempt 2: html/flag.txt -> *file does not exist*
Re- reading the challenge statement helped me realise that the website is filtering the absolute paths hence this was my next move :
Attempt 3: ../../../flag.txt -> *Redirected me to a webpage that displayed the flag*
The flag obtianed : picoCTF{7h3_p47h_70_5ucc355_e5a6fcbc}

## <3
