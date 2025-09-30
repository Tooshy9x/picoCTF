# Custom encryption
[link](https://play.picoctf.org/practice/challenge/412?category=2&page=1)

## challenge information
```
medium , cryptography , picoctf2024 ,browser_shell_to_solve
ASCII-encoding , XOR
```
### Description
Can you get sense of this code file and write the function that will decode the given encrypted file content.

flag-info =>
```
a = 90
b = 26
cipher is: [61578, 109472,437888, 6842, 0, 20526, 129998, 526834, 478940, 287364, 0, 567886, 143682
, 34210, 465256, 0, 150524, 588412, 6842, 424204, 164208, 184734, 41052, 41052, 116314, 41052, 177892
, 348942, 218944, 335258, 177892, 47894, 82104, 116314]
```
code_file =>
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
## Solution
1. open code_file and enc_flag in vscode 
<img width="1200" height="700" alt="Image" src="https://github.com/user-attachments/assets/849a188d-985e-4f32-b71d-f3b39c5cbc06" />

2. add new python file and copy flag-info in file  and add  p = 97  g = 31 in file and
 add generator in file ``` def generator(g, x, p):
    return pow(g, x) % p  ```

3. We need to calculate v,u by ``` v = generator(g, b, p)
    key = generator(v, a, p) ```
4. and add
 ```
     print(key)
decipher = ""
for c in cipher:
    decipher += chr(c // 311 // key)
print(decipher)
```
print(key) → Prints the value of the decryption key.

decipher = "" → Prepares an empty string to collect the decrypted text.

for c in cipher: → Loops through each number in the encrypted list.

c // 311 // key → Decrypts the number by dividing it by 311, then by the key.

chr(...) → Converts the decrypted number to its ASCII character.

decipher += ... → Adds the character to the decrypted message.

print(decipher) → Prints the final decrypted text.

5. run this file

  ```
 def generator(g, x, p):
    return pow(g, x) % p
a = 90
b = 26
p = 97
g = 31
cipher = [61578, 109472,437888, 6842, 0, 20526, 129998, 526834, 478940, 287364, 0, 567886, 143682
, 34210, 465256, 0, 150524, 588412, 6842, 424204, 164208, 184734, 41052, 41052, 116314, 41052, 177892
, 348942, 218944, 335258, 177892, 47894, 82104, 116314]
v = generator(g, b, p)
key = generator(v, a, p)
print(key)
decipher = ""
for c in cipher:
   decipher += chr(c // 311 // key)
print(decipher)
 ```
<img width="1200" height="700" alt="Image" src="https://github.com/user-attachments/assets/291cf1d0-f035-4cb1-80fc-2737fac20605" />

6. use this code to solve this cipher
  ```
   #!/usr/bin/python

# Given in the enc_flag file
a = 94
b = 29
cipher = [260307, 491691, 491691, 2487378, 2516301, 0, 1966764, 1879995, 1995687, 1214766, 0, 2400609, 607383, 144615, 1966764, 0, 636306, 2487378, 28923, 1793226, 694152, 780921, 173538, 173538, 491691, 173538, 751998, 1475073, 925536, 1417227, 751998, 202461, 347076, 491691]

# Passed to test function from main
text_key = "trudeau"

# Unchanged function
def generator(g, x, p):
    return pow(g, x) % p

# Division instead of multiplication
def decrypt(ciphertext, key):
    plain = []
    for num in ciphertext:
        plain.append(chr(int(num / key / 311)))
    return plain

# No reversing of the order of the text chars
def dynamic_xor_decrypt(ciphertext, key):
    text = ""
    key_length = len(key)
    for i, char in enumerate(ciphertext):
        key_char = key[i % key_length]
        decrypted_char = chr(ord(char) ^ ord(key_char))
        text += decrypted_char
    return text

if __name__ == "__main__":

    # Unchanged code from test function
    p = 97
    g = 31
    u = generator(g, a, p)
    v = generator(g, b, p)
    key = generator(v, a, p)
    b_key = generator(u, b, p)
    shared_key = None
    if key == b_key:
        shared_key = key
    else:
        print("Invalid key")
        exit(1)  # Exit instead of return
    
    plain = decrypt(cipher, shared_key)
    flag = dynamic_xor_decrypt(plain, text_key)
    print(flag[::-1])
  ```

<img width="1613" height="740" alt="Image" src="https://github.com/user-attachments/assets/1a1cefff-ab22-404f-8648-fb2a10a26d75" />



