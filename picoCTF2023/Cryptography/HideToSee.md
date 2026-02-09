# HideToSee

<img width="962" height="504" alt="image" src="https://github.com/user-attachments/assets/6cf17cb5-0751-426b-b2f3-f0a7c62b4259" />


- --

## Objective
The objective of this challenge is to extract hidden data from an image file and
decrypt the recovered message to obtain the flag.

- --

## Description
The challenge provides an image file that appears normal at first glance.
However, the title and description strongly suggest that hidden data is embedded
inside the image using steganography techniques.

The goal is to extract this hidden data, analyze it, identify the encryption
method used, and recover the original flag.

- --

## Methodology

### 1. Identifying Hidden Data in the Image

Since the challenge suggests the presence of hidden information, the image file
is analyzed using steganography tools. One of the most common tools for
extracting embedded data from images is **steghide**.

The following command is used to attempt data extraction:

```bash
steghide --extract -sf atbash.jpg
```
The tool prompts for a passphrase. After entering the correct passphrase and confirming overwrite, a new file is generated:

encrypted.txt
This indicates that the image contained hidden data successfully extracted using steganography.


### 2. Inspecting the Extracted File
The next step is to analyze the contents of the extracted file. This is done using:

```bash
cat encrypted.txt
```

<img width="886" height="641" alt="image" src="https://github.com/user-attachments/assets/c1d9eaaa-008f-484c-b4e3-4206d4af8457" />


The file contains the following encrypted string:


krxlXGU{zgyzhs_xizxp_7142uwv9}

The string resembles the format of a picoCTF flag but appears encrypted using a substitution cipher.

### 3. Identifying the Encryption Algorithm
By analyzing the encrypted text, several observations can be made:


Letters appear transformed but maintain structure

Numbers and symbols remain unchanged

These characteristics strongly suggest the use of the Atbash Cipher.

Atbash Cipher Explanation
The Atbash cipher is a classical monoalphabetic substitution cipher.
It works by reversing the alphabet so that each letter is replaced with its mirrored counterpart.

Example mapping:

a ↔ z  
b ↔ y  
c ↔ x  
d ↔ w  
...
This means:

The first letter becomes the last letter

The second letter becomes the second-to-last letter

The transformation is symmetrical, meaning encryption and decryption use the same algorithm

### 4. Implementing Atbash Decryption
To automate the decoding process, a custom C program is written.


Atbash Decryption Code

```c
#include <stdio.h>
#include <string.h>

void atbash(char *text) {
    int len = strlen(text);

    for (int i = 0; i < len; i++) {
        if (text[i] >= 'a' && text[i] <= 'z') {
            text[i] = 'z' - (text[i] - 'a');
        } else if (text[i] >= 'A' && text[i] <= 'Z') {
            text[i] = 'Z' - (text[i] - 'A');
        }
    }
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        printf("Error: usage %s <text>\n", argv[0]);
        return 1;
    }

    atbash(argv[1]);
    printf("%s\n", argv[1]);

    return 0;
}

```
### 5. Code Explanation
Alphabet Mirroring Logic
The key part of the algorithm is:

'z' - (text[i] - 'a')
This works as follows:

text[i] - 'a'
Converts the character into its position in the alphabet
Example:

'c' - 'a' = 2
'z' - position
Mirrors the character across the alphabet
Example:

'z' - 2 = 'x'
The same logic applies to uppercase letters using 'A' and 'Z'.

Handling Non-Alphabet Characters
Characters such as:

Numbers

Brackets

Underscores

are left unchanged because they are not part of the alphabet range.

### 6. Running the Decryption Program
After compiling the program:

gcc atbash.c -o atbash
The encrypted text is passed as an argument:
```bash
./atbash "krxlXGU{zgyzhs_xizxp_7142uwv9}"
```
The program outputs the decrypted message.

<img width="769" height="189" alt="image" src="https://github.com/user-attachments/assets/41f52d07-87cb-4b96-abe1-6d30de71fa61" />



After applying the Atbash cipher, the encrypted string is successfully decoded and reveals the original flag.

### Flag
picoCTF{atbash_crack_7142fde9}

