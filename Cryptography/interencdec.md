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

<img width="712" height="713" alt="Image" src="https://github.com/user-attachments/assets/60bd809a-bb7c-4dc5-8503-9d66f1bbfa48" />

  The flags is ``` picoCTF{caesar_d3cr9pt3d_86de32d2} ```
  
<img width="947" height="488" alt="Image" src="https://github.com/user-attachments/assets/7dec5fde-1828-4943-b4e4-63fbd774ef15" />


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
<img width="371" height="64" alt="Image" src="https://github.com/user-attachments/assets/1155b5cd-8805-4092-9c06-b2966c8146a0" />



