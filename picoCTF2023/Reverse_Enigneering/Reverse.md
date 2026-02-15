# Reverse – picoCTF 2023 Writeup

<img width="886" height="462" alt="image" src="https://github.com/user-attachments/assets/15371187-ff26-45de-a468-c177b4ae3f9f" />


---

## Challenge Description

The challenge provides us with:

- A compiled binary file: `ret`
- No hints available

The scenario states that the author forgot the password to the file and needs help finding it.

---

## Solution

### Step 1: Initial File Analysis

First, I examined the file type to understand what we're working with:

```bash
file ret
```
This revealed it's a 64-bit Linux ELF executable compiled with GCC.

Step 2: Using Strings Command
The simplest approach for basic reverse engineering challenges is to extract readable strings from the binary using the strings command:

```bash
strings ret
```
Step 3: Analyzing the Output
The strings command revealed several interesting pieces of information embedded in the binary:

<img width="679" height="533" alt="image" src="https://github.com/user-attachments/assets/fb270661-baa9-4832-9b5f-4d94e4cfb7b2" />

# Flag 
picoCTF{3lf_r3v3r5ing_succe55ful_1de05085}
