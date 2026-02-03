# rotation

<img width="960" height="500" alt="image" src="https://github.com/user-attachments/assets/2240d51f-ad3f-4b90-a0dc-b1cbdc90bc35" />


## Objective
The objective of this challenge is to decrypt an encrypted file that uses a rotation-based cipher in order to recover the hidden flag.

## Description
The challenge provides an encrypted text file containing the flag.  
Based on the hint *“Sometimes rotation is right”*, it can be inferred that the cipher used is a **ROT (Caesar rotation) cipher**.

The goal is to determine the correct rotation that reveals a readable flag.

---

## Methodology

### 1. Understanding the Cipher

A rotation (ROT) cipher shifts each alphabetical character by a fixed number of positions within the alphabet.  
Since the rotation value is unknown, all possible shifts (ROT0–ROT25) must be tested.

Non-alphabetic characters remain unchanged.

---

### 2. Brute-Forcing All Rotations

Instead of guessing the correct rotation manually, a small C program is used to **brute-force all possible rotations** and print their results.

This allows us to visually inspect each output and identify which one produces a readable picoCTF flag.

---

## Rotation Brute-Force Code (C)

The following C program applies all possible rotations (ROT0 to ROT25) to a given input string:

```c
#include <stdio.h>
#include <string.h>

int rotn(int c, int n) {
    if (c >= 'a' && c <= 'z')
        return (c - 'a' + n) % 26 + 'a';
    else if (c >= 'A' && c <= 'Z')
        return (c - 'A' + n) % 26 + 'A';
    else
        return c;
}

int main(int argc, char *argv[]) {

    if (argc < 2) {
        printf("Usage: %s text\n", argv[0]);
        return 1;
    }

    int len = strlen(argv[1]);

    for (int j = 0; j < 26; j++) {
        printf("ROT%d: ", j);
        for (int i = 0; i < len; i++) {
            printf("%c", rotn(argv[1][i], j));
        }
        printf("\n");
    }

    return 0;
}
```

The rotn function works by rotating alphabetical characters while leaving all other characters unchanged.
There are two possible cases for each character: lowercase letters and uppercase letters. These cases are handled separately because each one has a different ASCII reference point.

If the character is a lowercase letter (a–z), the function subtracts the ASCII value of 'a' (97).
If the character is an uppercase letter (A–Z), it subtracts the ASCII value of 'A' (65).

This normalization step converts the character into a value between 0 and 25, representing its position in the alphabet.

Next, the rotation value n is added. This value determines how many positions the character is shifted forward (or backward if negative).
To ensure the result stays within the 26-letter alphabet, a modulo 26 operation is applied.

Finally, the ASCII reference value ('a' or 'A') is added back to convert the result into a valid character.

Non-alphabetic characters are returned unchanged.
The ASCII base value is added back to transform the alphabet index into a valid character.

<img width="550" height="663" alt="image" src="https://github.com/user-attachments/assets/2a948e8f-7c29-46ae-9c91-2260a2d914fb" />

# Flag
picoCTF{r0tat1on_d3crypt3d_a4b7d759}


