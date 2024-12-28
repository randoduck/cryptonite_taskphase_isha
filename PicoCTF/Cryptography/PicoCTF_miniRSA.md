# PicoCTF- miniRSA
## Problem Statement
"What happens if you have a small exponent? There is a twist though, we padded the plaintext so that (M ** e) is just barely larger than N. Let's decrypt this" Given to us in the attached file are the following values :
N: 
e: 3
ciphertext (c): 
## Thought Process 
One must understand what RSA is to solve this challenge . RSA (Rivest–Shamir–Adleman) is a popular encryption method named after its creators, Ron Rivest, Adi Shamir, and Leonard Adleman. It's a form of public-key cryptography, meaning it uses two keys for secure communication: a public key and a private key. RSA is fundamental to many online security systems, allowing secure data exchanges for things like secure websites, emails, and other online communications.
How RSA Encryption Works

*Key Generation:*
Choose two large prime numbers (let’s call them p and q) and multiply them to get 𝑛=𝑝×𝑞
n=p×q. This number 𝑛n will be part of both the public and private keys.
Next, calculate a value ϕ(n), which is (p−1)(q−1).
Pick a number e that has no common factors with ϕ(n), and then calculate d, the modular inverse of e. This ensures e⋅d=1 mod ϕ(n).
Now, the public key is (e,n) and the private key is (d,n).

*Encryption:*
To encrypt a message 
M, the sender uses the public key (e,n) and calculates C=M^e  mod n. Here, C is the encrypted version of the message, or ciphertext.

*Decryption:*
The receiver, using their private key (d,n), decrypts the ciphertextC by calculating M=C^d mod n, which retrieves the original message.
For the simplicity and accuracy we'll use an RSA encoder 

## Solution 
The following Text was provided to us :
```
N: 1615765684321463054078226051959887884233678317734892901740763321135213636796075462401950274602405095138589898087428337758445013281488966866073355710771864671726991918706558071231266976427184673800225254531695928541272546385146495736420261815693810544589811104967829354461491178200126099661909654163542661541699404839644035177445092988952614918424317082380174383819025585076206641993479326576180793544321194357018916215113009742654408597083724508169216182008449693917227497813165444372201517541788989925461711067825681947947471001390843774746442699739386923285801022685451221261010798837646928092277556198145662924691803032880040492762442561497760689933601781401617086600593482127465655390841361154025890679757514060456103104199255917164678161972735858939464790960448345988941481499050248673128656508055285037090026439683847266536283160142071643015434813473463469733112182328678706702116054036618277506997666534567846763938692335069955755244438415377933440029498378955355877502743215305768814857864433151287
e: 3

ciphertext (c): 1220012318588871886132524757898884422174534558055593713309088304910273991073554732659977133980685370899257850121970812405700793710546674062154237544840177616746805668666317481140872605653768484867292138139949076102907399831998827567645230986345455915692863094364797526497302082734955903755050638155202890599808146956044568639690002921620304969196755223769438221859424275683828638207433071955615349052424040706261639770492033970498727183446507482899334169592311953247661557664109356372049286283480939368007035616954029177541731719684026988849403756133033533171081378815289443019437298879607294287249591634702823432448559878065453908423094452047188125358790554039587941488937855941604809869090304206028751113018999782990033393577325766685647733181521675994939066814158759362046052998582186178682593597175186539419118605277037256659707217066953121398700583644564201414551200278389319378027058801216150663695102005048597466358061508725332471930736629781191567057009302022382219283560795941554288119544255055962
```
One of the hints being the Value of e is very small which is a vulnerability that could be exploited .
This is because we know : ciphertext(c) = plaintext^e mod N . Since the value of e is very small. 
When the public exponent 𝑒 is small (like 𝑒=3), and the plaintext m is small enough such that  the modulo operation has no effect. This is because the plaintext's cube is already much smaller than N.
This simply means our new approach would be :
ciphertext(c) = plaintext^e
rearranging the terms we get :
*plaintext = ciphertext(c)^(1/e)*
which is simply... finding the cube root of c . Now this can be done using a Python program that performs Binaray search and finds the cube root since the number is big and theres a scope for error otherwise . Further research shows that one can gmpy2 module which finds the nth root and is much faster. Im gonna go ahead with Binary search , here is the python script for it :
```python
def find_cubic_root(n):
    """
    Finds the integer cube root of a number.
    """
    a = 1
    b = n
    while b - a > 1:
        mid = (a + b) // 2
        if mid**3 > n:
            b = mid
        else:
            a = mid

    # Check for exact cube root
    if a ** 3 == n:
        return a
    elif b ** 3 == n:
        return b
    else:
        return 0

# Challenge inputs
c = 2205316413931134031074603746928247799030155221252519872649594750678791181631768977116979076832403970846785672184300449694813635798586699205901153799059293422365185314044451205091048294412538673475392478762390753946407342073522966852394341

# Find the plaintext
m = find_cubic_root(c)
print(m)
```
The Value of m obtianed : 13016382529449106065894479374027604750406953699090365388202767087888130179936381
Converting this into its Hexadecimal Representation we get : 7069636F4354467B6E3333645F615F6C41726733725F655F30613431656635307D
Making pairs of two and turning them into their decimal equivalent 
and finding out the respective ascii characters we get the flag as :
picoCTF{n33d_a_lArg3r_e_0a41eff50}

## <3















