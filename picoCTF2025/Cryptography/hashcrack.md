# hashcrack

<img width="953" height="569" alt="image" src="https://github.com/user-attachments/assets/36debc6f-a7d7-4919-b492-61fc426505c6" />

## Objective
The objective of this challenge is to recover a secret message stored on a server by exploiting **weakly hashed passwords** used by the administrator.

## Description
A company stored a secret message on a server that was compromised due to the use of weak password hashing.  
By analyzing the provided information after launching the challenge instance, it is possible to crack the hashes and gain access to the secret.

The challenge can be solved directly from the browser or by interacting with the provided shell environment.

## Methodology
After launching the instance, hashed passwords are provided.  
These hashes are analyzed using **online hash identification tools**, which determine the hashing algorithm based on the hash format.

Once the algorithm is identified, **online hash decryption databases** are used to search for the original plaintext values.  
Since the passwords are weak and commonly used, the hashes can be successfully reversed.

After recovering the correct credentials, they are used to access the server and retrieve the secret message.


<img width="567" height="231" alt="image" src="https://github.com/user-attachments/assets/9f14eab4-2385-4c1a-ae74-056cff48582d" />


## Tools Used

- Browser-based brute-force decrypters
- Online hash identification tools

## Result
After successfully cracking the weak hashes and authenticating with the recovered credentials, the secret message is revealed, yielding the flag for the challenge.

## Flag
picoCTF{UseStr0nG_h@shEs_&PaSswDs!_6965e43b}
