# rotation

 [link of CTF](https://play.picoctf.org/practice/challenge/373?category=2&originalEvent=72&page=1)

## challenge information :

```
medium , Cryptography , picoctf 2023 
Author: Loic Shema
Description
You will find the flag after decrypting this
The cipher is xqkwKBN{z0bib1wv_l3kzgxb3l_i4j7l759}
Hints : Sometimes rotation is right 
```
## Description
ROT13 is a simple letter substitution cipher that replaces a letter with the 13th letter after it in the Latin alphabet.
 It is a special case of the Caesar cipher.

## solution 1 

use  https://rot13.com  to solve this cypher and use Rot 18 and he give you the Flag 

<img width="400" height="400" alt="Image" src="https://github.com/user-attachments/assets/fabba741-8f6d-4de9-8635-24e177329015" />

## solution 2 , by python
``` 
root@DESKTOP-B0U1BDJ:~# echo xqkwKBN{z0bib1wv_l3kzgxb3l_i4j7l759} > encrypted.txt
root@DESKTOP-B0U1BDJ:~# ls
encrypted.txt
root@DESKTOP-B0U1BDJ:~# cat encrypted.txt
xqkwKBN{z0bib1wv_l3kzgxb3l_i4j7l759}
root@DESKTOP-B0U1BDJ:~# nano solve1.py
```
and put this code in solve1.py :

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

# Read the encoded flag
with open("encrypted.txt", 'r') as fh:
    enc_flag = fh.read().strip()

for i in range(1, alpha_len+1):
    plain = shift(enc_flag, i)
    if ('picoCTF' in plain):
        print("ROT-%02d: %s" % (i, plain))
```

and use this command for Give permission ``` chmod +x solve.py ```



<img width="450" height="146" alt="Image" src="https://github.com/user-attachments/assets/35b4f6ad-7574-4d3f-bf2e-d92291c58f7e" />



<img width="954" height="314" alt="Image" src="https://github.com/user-attachments/assets/3e4b0338-75c9-4d31-b5c6-31ca4877b57f" />
