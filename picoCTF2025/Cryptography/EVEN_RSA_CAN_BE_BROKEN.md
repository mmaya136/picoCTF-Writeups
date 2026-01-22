# EVEN RSA CAN BE BROKEN???

<img width="945" height="591" alt="image" src="https://github.com/user-attachments/assets/8c35617c-ac55-412c-9a32-c6bad6d730be" />


## Objective
The objective of this challenge is to decrypt an RSA-encrypted flag using only the public values **N** and **e** provided by the service.

## Description
The service generates an RSA key pair and encrypts the flag using the public key.  
By connecting multiple times, different RSA moduli (**N**) are generated.

<img width="1281" height="75" alt="image" src="https://github.com/user-attachments/assets/c5d961bc-d404-4d6e-89c6-b3b8968e3ba8" />

---
## Provided Source Code (`encrypt.py`)

Below is the source code used by the challenge to generate and encrypt the flag.

```python
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
## Vulnerability Explanation

In this challenge, the RSA modulus `N` provided by the service is **even**.  
This immediately reveals a critical flaw in the key generation process.

Since the only even prime number is **2**, an even modulus implies that one of the RSA primes is equal to 2.  
As a result, the modulus can be trivially factored by dividing it by 2.

Once the factorization is obtained, the private key can be reconstructed and the ciphertext decrypted.  
This breaks RSA instantly and demonstrates a severe implementation error.

<img width="1284" height="212" alt="image" src="https://github.com/user-attachments/assets/24ecf265-9d12-4184-a487-88c4970608d6" />


<img width="1122" height="644" alt="image" src="https://github.com/user-attachments/assets/08aaf350-9795-4fa3-a2d6-659195cb8d69" />


## Flag
picoCTF{tw0_1$_pr!m3de643ad5}






