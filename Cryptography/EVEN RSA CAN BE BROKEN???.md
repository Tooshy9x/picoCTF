# EVEN RSA CAN BE BROKEN???
 [link](https://play.picoctf.org/practice/challenge/470?category=2&originalEvent=74&page=1)

## Challenge information
```
(use RSI cipher)
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

## The solution 1
1. connect : ``` $ nc verbal-sleep.picoctf.net ??  ```
   and he give me the code :
```
   root@DESKTOP-B0U1BDJ:~#  nc verbal-sleep.picoctf.net 58854
N:20147790425666438327440390504560280158805834787628365807474444987321518212534465492163291154972532409933054374787745017438438121937145788004409387542870246
e: 65537
cyphertext: 13474024218076029057296464231674421215159005842399798083665278661287842146443907321109335984684872602107647348553219050944624270082319009725155878336957085
```
2. use this web [RSI cipher](https://www.dcode.fr/rsa-cipher) and enter cipher
   
   <img width="1696" height="555" alt="Image" src="https://github.com/user-attachments/assets/dffde4c0-c9ab-4824-9c3c-897083a0c111" />
   
--------------

## The solution 2
1. connect : ``` $ nc verbal-sleep.picoctf.net ??  ```
   and he give me the code :
```
   root@DESKTOP-B0U1BDJ:~#  nc verbal-sleep.picoctf.net 58854
N:20147790425666438327440390504560280158805834787628365807474444987321518212534465492163291154972532409933054374787745017438438121937145788004409387542870246
e: 65537
cyphertext: 13474024218076029057296464231674421215159005842399798083665278661287842146443907321109335984684872602107647348553219050944624270082319009725155878336957085
```
2. We analyze the value of n by [factordb](https://factordb.com/) and we make sure we have even number after more connect in  ``` nc verbal-sleep.picoctf.net 58854 ``` 
    <img width="945" height="199" alt="Image" src="https://github.com/user-attachments/assets/422fab05-89a8-45af-8fda-8fbbc6610858" />

    <img width="939" height="191" alt="Image" src="https://github.com/user-attachments/assets/16acce1d-80d8-46f7-a008-003532b34b4d" />

    and pest in p   ,  and q is 2 becouse N is even nember


``` d = inverse(e, (p-1)*(q-1)) #the private key  ```

note :
```
P = prime number 1
Q = prime number 2
N = encryption exponent ( part of public key )
D = privite key 
```

### The script to solution cipher :
```
from Crypto.Util.number import long_to_bytes, inverse
p = 10073895212833219163720195252280140079402917393814182903737222493660759106267232746081645577486266204966527187393872508719219060968572894002204693771435123
q = 2
e = 65537
d = inverse(e, (p - 1) * (q - 1))  # the private key
encrypted_message = 13474024218076029057296464231674421215159005842399798083665278661287842146443907321109335984684872602107647348553219050944624270082319009725155878336957085
decripted_message = pow(encrypted_message,d,p*q) # (encrypted message ^ private key ) mod N , N is product of q and p
print (long_to_bytes(decripted_message).decode())
```

<img width="1904" height="551" alt="Image" src="https://github.com/user-attachments/assets/b0f0293f-56c0-421c-aa46-64c87ddd0a46" />

<img width="690" height="465" alt="Image" src="https://github.com/user-attachments/assets/802766f8-392c-48f4-a872-336d315e8a52" />
