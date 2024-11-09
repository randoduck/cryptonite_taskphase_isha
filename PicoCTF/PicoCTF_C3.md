# PicoCTF - C3

## Problem Statement
"This is the Custom Cyclical Cipher!
Download the ciphertext here.
Download the encoder here.
Enclose the flag in our wrapper for submission. If the flag was "example" you would submit "picoCTF{example}"."
The given Cipher test was 
```bash
:DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIl
```
With the encoder as :
```bash
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup1.index(char)
  out += lookup2[(cur - prev) % 40]
  prev = cur

sys.stdout.write(out)
```
## Thought Process & Solution

Its pretty clear that we must create a decoder from the script assigned to us and then feed the cipher text as input . We first save the given file in a directory using **wget** to obtain it through the link and  in order to turn the text into a decoder and see how it proceeds from there .

```bash
randoduck@DESKTOP-2PM3SNS:~$ wget https://artifacts.picoctf.net/c_titan/47/ciphertext
--2024-11-04 12:41:25--  https://artifacts.picoctf.net/c_titan/47/ciphertext
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 18.67.161.8, 18.67.161.51, 18.67.161.65, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|18.67.161.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 237 [application/octet-stream]
Saving to: ‘ciphertext’

ciphertext                           100%[======================================================================>]     237  --.-KB/s    in 0s

2024-11-04 12:41:28 (1.60 MB/s) - ‘ciphertext’ saved [237/237]

randoduck@DESKTOP-2PM3SNS:~$ cat ciphertext
DLSeGAGDgBNJDQJDCFSFnRBIDjgHoDFCFtHDgJpiHtGDmMAQFnRBJKkBAsTMrsPSDDnEFCFtIbEDtDCIbFCFtHTJDKerFldbFObFCFtLBFkBAAAPFnRBJGEkerFlcPgKkImHnIlATJDKbTbFOkdNnsgbnJRMFnRBNAFkBAAAbrcbTKAkOgFpOgFpOpkBAAAAAAAiClFGIPFnRBaKliCgClFGtIBAAAAAAAOgGEkImHnIlrandoduck@DESKTOP-2PM3SNS:~$ wget https://artifacts.picoctf.net/c_titan/47/convert.py
--2024-11-04 12:41:51--  https://artifacts.picoctf.net/c_titan/47/convert.py
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 18.67.161.8, 18.67.161.51, 18.67.161.65, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|18.67.161.8|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 335 [application/octet-stream]
Saving to: ‘convert.py’

convert.py                           100%[======================================================================>]     335  --.-KB/s    in 0s

2024-11-04 12:41:52 (12.4 MB/s) - ‘convert.py’ saved [335/335]

randoduck@DESKTOP-2PM3SNS:~$ cat convert.py
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup1.index(char)
  out += lookup2[(cur - prev) % 40]
  prev = cur

sys.stdout.write(out)
randoduck@DESKTOP-2PM3SNS:~$ cp convert.py convert2.py
randoduck@DESKTOP-2PM3SNS:~$ cat convert2.py
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

out = ""

prev = 0
for char in chars:
  cur = lookup1.index(char)
  out += lookup2[(cur - prev) % 40]
  prev = cur

sys.stdout.write(out)
randoduck@DESKTOP-2PM3SNS:~$ vi convert2.py
randoduck@DESKTOP-2PM3SNS:~$ python3 convert2.py
``` 
To turn this into a decoder we had to make certain changes like swapping lookup 1 and lookup 2 and changing the - to + and a few more variables. It took alot of trail and error and almost 4 modified python scripts to get the decoder to work. I verified it by inputting abcd into the encoder and made sure the decoder gave me abcd back for the given value . 

```bash 
randoduck@DESKTOP-2PM3SNS:~$ cp convert.py convert5.py
randoduck@DESKTOP-2PM3SNS:~$ vi convert5.py
```
Here is the final modified script in convert5.py 

```bash
import sys
chars = ""
from fileinput import input
for line in input():
  chars += line

lookup1 = "\n \"#()*+/1:=[]abcdefghijklmnopqrstuvwxyz"
lookup2 = "ABCDEFGHIJKLMNOPQRSTabcdefghijklmnopqrst"

with open('ciphertext','r') as f:
        ciphertext = f.read()


        prev = 0
        out=""
        for letter in ciphertext:
                ind = lookup2.index(letter)
                for x in range(100000):
                                if (x - prev) % 40 == ind:
                                     out += lookup1[x]
                                     prev = x
                                     break
        print(out)
```
After verifing and running the script we get a python3 code :
```bash 
randoduck@DESKTOP-2PM3SNS:~$ echo -n "OBBBd" | python3 convert5.py
#asciiorder
#fortychars
#selfinput
#pythontwo

chars = ""
from fileinput import input
for line in input():
    chars += line
b = 1 / 1

for i in range(len(chars)):
    if i == b * b * b:
        print chars[i] #prints
        b += 1 / 1

randoduck@DESKTOP-2PM3SNS:~$ vi pyscript.py
randoduck@DESKTOP-2PM3SNS:~$ vi newscript.py
```
Here pyscript contains the above code where as newscript contains the modified version of it which took pyscript.py as an input 
here is the modified script :
```bash
with open('pyscript.py') as f:
        ciphertext = f.read()
        asciichars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmn"
        b = 1
        for i in range(len(ciphertext)):
                if i == b*b*b:
                            print(ciphertext[i])
                            b += 1
```
After Running this we obtian the flag 
```bash 
randoduck@DESKTOP-2PM3SNS:~$ python3 newscript.py
a
d
l
i
b
```
# <3
