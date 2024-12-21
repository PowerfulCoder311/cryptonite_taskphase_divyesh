# Custom Encryption
challenge: Can you get sense of this code file and write the function that will decode the given encrypted file content.
It looks like we have to study the custom_encryption.py file, make a decoder and retrieve the flag.
the file
```
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def encrypt(plaintext, key):
    cipher = []
    for char in plaintext:
        cipher.append(((ord(char) * key*311)))
    return cipher


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


def test(plain_text, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = randint(p-10, p)
    b = randint(g-10, g)
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


if __name__ == "__main__":
    message = sys.argv[1]
    test(message, "trudeau")
```
the if statement calls the test function. In the test function, p and q are fixed while a and b are random integers. However, in the encrypted file, a and b are given so it doesnt matter.
Creating the decoding algorithms for dynamic_xor_encrypt and encrypt functions should be enough for retrieving the flag because I dont see any use of the generator function in retrieving the flag.

The script for decoding:
```
from random import randint
import sys


def generator(g, x, p):
    return pow(g, x) % p


def decrypt(encoded, key):
    decoded=""
    for char in encoded:
        decoded+=chr(int(char / key/ 311))
    return decoded


def is_prime(p):
    v = 0
    for i in range(2, p + 1):
        if p % i == 0:
            v = v + 1
    if v > 1:
        return False
    else:
        return True


def dynamic_xor_decrypt(encoded, text_key):
    decoded = ""
    key_length = len(text_key)
    for i, char in enumerate(encoded):
        key_char = text_key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        decoded += decrypted_char
    return decoded


def test(encoded, text_key):
    p = 97
    g = 31
    if not is_prime(p) and not is_prime(g):
        print("Enter prime numbers")
        return
    a = 94
    b = 29
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
    semi_decoded = decrypt(encoded, shared_key)
    decoded = dynamic_xor_decrypt(semi_decoded, text_key)
    
    print(f'flag is: {decoded[::-1]}')


if __name__ == "__main__":
    #message = sys.argv[1]
    test([260307, 491691, 491691, 2487378, 2516301, 0, 1966764, 1879995, 1995687, 1214766, 0, 2400609, 607383, 144615, 1966764, 0, 636306, 2487378, 28923, 1793226, 694152, 780921, 173538, 173538, 491691, 173538, 751998, 1475073, 925536, 1417227, 751998, 202461, 347076, 491691], "trudeau")
```
Explanation:
