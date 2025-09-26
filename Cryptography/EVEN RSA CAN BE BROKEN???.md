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
   and he give me the code :
```
   root@DESKTOP-B0U1BDJ:~#  nc verbal-sleep.picoctf.net 58854
N:20147790425666438327440390504560280158805834787628365807474444987321518212534465492163291154972532409933054374787745017438438121937145788004409387542870246
e: 65537
cyphertext: 13474024218076029057296464231674421215159005842399798083665278661287842146443907321109335984684872602107647348553219050944624270082319009725155878336957085
```

   



