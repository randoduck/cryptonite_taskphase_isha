# File Globbing

## Challenge 1: Matching With * (Summary/Learning)
We have been introduced to the `*` character which is a glob.
we obtainthe flag by running `/challenge/run` after changing your directory to `/challenge`, using `*` glob to keep the argument you pass to `cd` to at most four characters

### Solution
 To obtain the flag , the following commands were executed :
 ```bash
cd /ch*
/challenge/run
```

## Challenge 2: Matching With ? (Summary/Learning)
Another character is introduced here : `?`, which is used in any argument and actas as a single-character wildcard , and tries to replace it with any files that contain the single character specified 
we obtain the flag by  running `/challenge/run` after using `cd` to change directory to `/challenge` , using `?` glob instead of c and l in the argument to `cd` 

### Solution
To obtain the flag the following commands were executed :
```bash
cd /?ha??enge
/challenge/run
```
## Challenge 3: Matching With [ ] (Summary/Learning)
Here they introduce us to the `[]` glob ,`[ ]` is a wildcard for a subset of potential characters, specified within the brackets. Thus if I specify "bash" within `[ ]` I'll be able to meet the requirements of the challenge since one character of all the mentioned files is present in "bash"
To obtain the flag we change our directory to `/challenge/files` and run `/challenge/run` with a single argument that bracket-globs into `file_b`, `file_a`, `file_s`, and `file_h`

### Solution
To obtain the flag the following commands were executed :
```bash
cd /challenge/files
/challenge/run file_[bash]
```
## Challenge 4:  Matching Paths With [ ] (Summary/Learning)
This is another exercise using the similar learnings from the previous one 
we must obtain the flag by running `/challenge/run` from home directory with a single argument that bracket-globs into the absolute paths to the `file_b`, `file_a`, `file_s`, and `file_h` files placed in `/challenge/files` which can be made possible by directly using `[bash]`

### Solution
The flag can be obtained by executing the following command :
```bash
/challenge/run /challenge/files/file_[bash]
```
## Challenge 5: Mixing Globs (Summary/Learning):
To obtain the flag we must change the  directory to `/challenge/files` and write a
- single
- (6 characters or less) glob 
- must match the files "challenging", "educational", and "pwning"
using  `[ ]` and `*` globs . Which can be done by using [cep]* as an argument as it containts the first letters of all and satisfies the conditions

### Solution
The flag was obtained by executing the following commands 
```bash
cd /challenge/files
/challenge/run [cep]*
```

## Challenge 6 :  Exclusionary Globbing (Summary/Learning)
Exclusionary globbing refers to find the files that dont match with the characters that aren't listed .This can be exprssed as `!` or (in newer versions of bash) a `^`. In this challenge we'll have to use `!` or `^` to match with the files that don't start with "p", "w", or "n" by first changing the directory to ` /challenge/files` and then running it 

### Solution
To obtain the flag the following code must be executed 
```bash
 cd /challenge/files
/challenge/run [!pwn]*
```
## <3
