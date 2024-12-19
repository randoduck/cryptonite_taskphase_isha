# Custom Encryption 

## Challenge 
*Can you get sense of this code file and write the function that will decode the given encrypted file content.*
*Find the encrypted file here flag_info and code file might be good to analyze and get the flag.*
The information in the text:
a = 97
b = 22
cipher is: [151146, 1158786, 1276344, 1360314, 1427490, 1377108, 1074816, 1074816, 386262, 705348, 0, 1393902, 352674, 83970, 1141992, 0, 369468, 1444284, 16794, 1041228, 403056, 453438, 100764, 100764, 285498, 100764, 436644, 856494, 537408, 822906, 436644, 117558, 201528, 285498]

## Thought Process 
Looking at the Hint:*Understanding encryption algorithm to come up with decryption algorithm.*
Hence the next obvious step had to be to come up with a decryption program for the encryption program provided to us, after few tweaks
here and there and since I needed a better grip over python, hence took the help of multiple resources to come up with a decryption algorithm and substitute the information. 

```python
from random import randint
import sys

def generator(g, x, p):
    return pow(g, x) % p

def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key * 311)))
    return cipher

def decrypt(cipher, key):
    plaintext = ""
    for num in cipher:
        if num == 0:
            plaintext += "\x00"
        else:
            decrypted_char = num // (key * 311)  
            plaintext += chr(decrypted_char)
    return plaintext

def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True

def dynamic_xor_encrypt(plaintext, text_key):
    cipher_text = ""
    key_length = len(text_key)
    for i, char in enumerate(plaintext[::-1]):
        key_char = text_key[i % key_length]
        encrypted_char = chr(ord(char) ^ ord(key_char))
        cipher_text += encrypted_char
    return cipher_text

def dynamic_xor_decrypt(ciphertext, text_key):
    plaintext = ""
    key_length = len(text_key)
    for i, char in enumerate(ciphertext):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))  
        plaintext = decrypted_char + plaintext 
    return plaintext

def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p - 10, p)
    b = randint(g - 10, g)
    print(f"a = {a}")
    print(f"b = {b}")
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        return
    semi_cipher = dynamic_xor_encrypt(plain_text, text_key)
    cipher = encrypt(semi_cipher, shared_key)
    print(f'cipher is: {cipher}')

def decode_flag(cipher, text_key, g, p, a, b):

    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)

    if key != b_key:
        raise ValueError("Key mismatch during decryption.")

    semi_cipher = decrypt(cipher, key)
    plaintext = dynamic_xor_decrypt(semi_cipher, text_key)

    return plaintext


if __name__ == "__main__":
    if len(sys.argv) > 1:
        message = sys.argv[1]
        text_key = "trudeau"
        test(message, text_key)
    else:
        
        cipher = [151146, 1158786, 1276344, 1360314, 1427490, 1377108, 1074816, 1074816, 386262, 705348, 0, 1393902, 352674, 83970, 1141992, 0, 369468, 1444284, 16794, 1041228, 403056, 453438, 100764, 100764, 285498, 100764, 436644, 856494, 537408, 822906, 436644, 117558, 201528, 285498]

        text_key = "trudeau"
        g = 31
        p = 97
        a = 97
        b = 22  # Value from flag_info

        flag = decode_flag(cipher, text_key, g, p, a, b)
        print(f"{flag}")
```
hence the flag obtained after running this decryption algorithm  we get :
*picoCTF{custom_d2cr0pt6d_e4530597}*

## <3