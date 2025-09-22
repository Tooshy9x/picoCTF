# hashcrack
[link](https://play.picoctf.org/practice/challenge/475?category=2&originalEvent=74&page=1) 

## Description

A company stored a secret message on a server that got breached because the admin used weakly hashed passwords.
The goal: connect to the server, identify the hash type, crack it, and repeat until the final flag is revealed.

Connect to the challenge:
``` nc verbal-sleep.picoctf.net ???? ```
### Knowledge Required
-Hash algorithms: MD5, SHA-1, SHA-256.
-Hash identification (length, format, or tools like CyberChef).
-Hash cracking using tools such as John the Ripper.

## Solution
1. Connect to the server ``` nc verbal-sleep.picoctf.net ```
The server prints a hash, for example:  ``` We have identified a hash: 482c811da5d5b4bc6d497ffa98491e38
Enter the password for identified hash: ```
2. Identify the hash type
Check with CyberChef.com 
482c811da5d5b4bc6d497ffa98491e38 → 32 chars → MD5.
   
3. Save the hash and crack it ``` echo "482c811da5d5b4bc6d497ffa98491e38" > hash1.txt ```
4. use the john ripper to solvie his hash ``` sudo john --format=raw-md5 hash1.txt ```
5. Second hash
Example: b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3 → 40 chars → SHA-1.

Save and crack:   ``` echo "b7a875fc1ea228b9061041b7cec4bd3c52ab3ce3" > hash2.txt ```
use the john ripper to solvie his hash ``` sudo john --format=raw-sha1 hash2.txt ```
6. Third hash
Example:
916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745 → 64 chars → SHA-256.

Save and crack: ``` echo "916e8c4f79b25028c9e467f1eb8eee6d6bbdff965f9928310ad30a8d88697745" > hash3.txt ``` 
use the john ripper to solvie his hash ``` sudo john --format=raw-sha256 hash3.txt ```
7. Final flag
After submitting the last cracked password, the server prints the flag.

(Flag omitted here — run the challenge to retrieve it yourself.)

<img width="785" height="315" alt="Image" src="https://github.com/user-attachments/assets/6b69b45f-5665-456d-a7b1-2db8c04664f7" />

## Useful Notes

_Always verify the hash length to determine the correct algorithm.
If cracking is slow, specify a wordlist:
``` sudo john --wordlist=/usr/share/wordlists/rockyou.txt --format=raw-md5 hash1.txt ```
_You can view cracked results with: ``` sudo john --show hash1.txt ```
_CyberChef or hash-identifier can help quickly distinguish hash types.

## Commands Recap
```
nc verbal-sleep.picoctf.net 54538
echo "<hash>" > hashX.txt
sudo john --format=raw-md5 hash1.txt
sudo john --format=raw-sha1 hash2.txt
sudo john --format=raw-sha256 hash3.txt
```



