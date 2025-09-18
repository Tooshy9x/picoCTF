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
  
