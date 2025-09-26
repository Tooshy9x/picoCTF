# EVEN RSA CAN BE BROKEN???
 [link](https://play.picoctf.org/practice/challenge/470?category=2&originalEvent=74&page=1)

## Challenge information
```
Easy , Cryptography , picoCTF , browser_webshell_solvable
Author: Michael Crotty
This service provides you an encrypted flag. Can you decrypt it with just N & e?
Hints:
1- How much do we trust randomness?
2- Notice anything interesting about N?
3- Try comparing N across multiple requests
```
The program's source code is :
```
from sys import exit
from Crypto.Util.number import bytes_to_long, inverse
from setup import get_primes

e = 65537

def gen_key(k):
    """
    Generates RSA key with k bits
    """
    p,q = get_primes(k//2)
    N = p*q
    d = inverse(e, (p-1)*(q-1))

    return ((N,e), d)

def encrypt(pubkey, m):
    N,e = pubkey
    return pow(bytes_to_long(m.encode('utf-8')), e, N)

def main(flag):
    pubkey, _privkey = gen_key(1024)
    encrypted = encrypt(pubkey, flag) 
    return (pubkey[0], encrypted)

if __name__ == "__main__":
    flag = open('flag.txt', 'r').read()
    flag = flag.strip()
    N, cypher  = main(flag)
    print("N:", N)
    print("e:", e)
    print("cyphertext:", cypher)
    exit()
```

## The solution
1. connect : ``` $ nc verbal-sleep.picoctf.net 62291  ```
   
