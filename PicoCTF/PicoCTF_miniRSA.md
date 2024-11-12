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
