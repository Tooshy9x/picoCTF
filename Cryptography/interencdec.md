# Description
```
Level: Easy
Tags: picoCTF 2024, Cryptography, base64, browser_webshell_solvable, caesar
Author: NGIRIMANA SCHADRACK
```
# cipher
Can you get the real meaning from this
```
YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclgya3lNRFJvYTJvMmZRPT0nCg==
 ```

Challenge link: https://play.picoctf.org/practice/challenge/418?category=2&page=1

# Solution

The first step :

<img width="597" height="132" alt="Image" src="https://github.com/user-attachments/assets/dcfe3ef0-1427-417e-9308-790738446543" />

commaned =  ``` cat enc_flag | base64 -d ```

cipher is = ```  d3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzg2a2wzMmsyfQ== ```

Step two : 

use this web : https://www.base64encode.org   to decode this cipher 

<img width="982" height="501" alt="Image" src="https://github.com/user-attachments/assets/f0e7c1d0-9a99-4598-9e6d-947d511d3b5f" />

this is new cipher ``` wpjvJAM{jhlzhy_k3jy9wa3k_86kl32k2} ```

step three : 

new cipher is ROT13 
use this web to decod the chipher https://rot13.com/ and use ROT19

<img width="667" height="666" alt="Image" src="https://github.com/user-attachments/assets/479eb3fc-9ce3-46e6-aed5-ca53f9d78a56" />

  The flags is ``` picoCTF{.....} ```
  
<img width="943" height="482" alt="Image" src="https://github.com/user-attachments/assets/2d06df3c-dba9-4ac6-bb1c-ae9a137467d4" />


##  Get the flag - python script solution

```
 #!/usr/bin/python

import string

alphabet = string.ascii_lowercase
alpha_len = len(alphabet)

def shift(cipher_text, key):
    result = ''
    for c in cipher_text:
        if c.islower():
            result += alphabet[(alphabet.index(c) + key) % alpha_len]
        elif c.isupper():
            result += alphabet[(alphabet.index(c.lower()) + key) % alpha_len].upper()
        else:
            result += c
    return result

# Encrypted data after base64-decoding (twice)
enc_data = 'wpjvJAM{jhlzhy_k3jy9wa3k_86kl32k2}'

for i in range(1, alpha_len+1):
    plain = shift(enc_data, i)
    if ('picoCTF' in plain):
        print("ROT-%02d: %s" % (i, plain))
 ```

<img width="369" height="64" alt="Image" src="https://github.com/user-attachments/assets/5c2461b2-93c4-433f-b93b-bd2a70df8040" />


