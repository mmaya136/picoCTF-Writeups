# packer

<img width="952" height="498" alt="image" src="https://github.com/user-attachments/assets/4792fc99-0923-47c8-9aa4-2cbbd1a38f19" />


## Objective
The objective of this challenge is to reverse a Linux executable and recover the hidden flag.

## Description
The challenge provides a Linux binary that has been packed to prevent straightforward analysis.  
The goal is to identify the packing method, unpack the binary, and analyze its contents to extract the flag.

---

## Methodology

### 1. Initial Binary Analysis

First, the binary is inspected to identify its format and potential protections.  
Using the `file` command, it is confirmed that the binary is a Linux ELF executable.

To quickly check the content of the file we use the command cat.
The output reveals a large amount of compressed or obfuscated data, suggesting that the binary is packed.

<img width="1294" height="298" alt="image" src="https://github.com/user-attachments/assets/638718a7-e165-4efb-b683-1f582dbac632" />


---

### 2. Identifying the Packer

To determine the packing method, additional indicators are checked.  
The presence of UPX-related signatures and compressed sections strongly suggests that the binary is packed using **UPX (Ultimate Packer for eXecutables)**.

UPX is a common executable packer used to compress binaries and make static analysis more difficult.
<img width="899" height="511" alt="image" src="https://github.com/user-attachments/assets/04567b29-7da2-454a-bf55-c957cd83f2d0" />

---

### 3. Unpacking the Binary

Once UPX is identified, the binary is unpacked using the `upx` tool with the decompression flag:
<img width="903" height="345" alt="image" src="https://github.com/user-attachments/assets/9ba2c10b-1665-4b17-be10-1d6af19c5610" />





The unpacked binary is then loaded into **Ghidra** to perform disassembly and analyze the program’s control flow and functions.

Below is the decompiled code obtained after analyzing the binary with **Ghidra**, which allows us to inspect the program logic in a C-like representation:


```c
undefined8 main(void)

{
  size_t sVar1;
  char *pcVar2;
  int iVar3;
  undefined1 *puVar4;
  long in_FS_OFFSET;
  undefined1 auStack_a8 [8];
  size_t local_a0;
  undefined8 local_98;
  char *local_90;
  char local_88 [104];
  long local_20;
  
  local_20 = *(long *)(in_FS_OFFSET + 0x28);
  local_a0 = 100;
  local_98 = 99;
  for (puVar4 = auStack_a8; puVar4 != auStack_a8; puVar4 = puVar4 + -0x1000) {
    *(undefined8 *)(puVar4 + -8) = *(undefined8 *)(puVar4 + -8);
  }
  *(undefined8 *)(puVar4 + -8) = *(undefined8 *)(puVar4 + -8);
  builtin_strncpy(local_88,
                  "7069636f4354467b5539585f556e5034636b314e365f42316e34526933535f31613561336633397d"
                  ,0x51);
  local_88[0x51] = '\0';
  local_88[0x52] = '\0';
  local_88[0x53] = '\0';
  local_88[0x54] = '\0';
  local_88[0x55] = '\0';
  local_88[0x56] = '\0';
  local_88[0x57] = '\0';
  local_88[0x58] = '\0';
  local_88[0x59] = '\0';
  local_88[0x5a] = '\0';
  local_88[0x5b] = '\0';
  local_88[0x5c] = '\0';
  local_88[0x5d] = '\0';
  local_88[0x5e] = '\0';
  local_88[0x5f] = '\0';
  local_88[0x60] = '\0';
  local_88[0x61] = '\0';
  local_88[0x62] = '\0';
  local_88[99] = '\0';
  local_90 = puVar4 + -0x70;
  *(undefined8 *)(puVar4 + -0x78) = 0x401eee;
  printf("Enter the password to unlock this file: ");
  pcVar2 = local_90;
  sVar1 = local_a0;
  *(undefined8 *)(puVar4 + -0x78) = 0x401f0f;
  fgets(pcVar2,(int)sVar1,(FILE *)stdin);
  pcVar2 = local_90;
  *(undefined8 *)(puVar4 + -0x78) = 0x401f2a;
  printf("You entered: %s\n",pcVar2);
  pcVar2 = local_90;
  sVar1 = local_a0;
  *(undefined8 *)(puVar4 + -0x78) = 0x401f47;
  iVar3 = strncmp(pcVar2,local_88,sVar1);
  if (iVar3 == 0) {
    *(undefined8 *)(puVar4 + -0x78) = 0x401f57;
    puts(
        "Password correct, please see flag: 7069636f4354467b5539585f556e5034636b314e365f42316e345269 33535f31613561336633397d"
        );
    *(undefined8 *)(puVar4 + -0x78) = 0x401f63;
    puts(local_88);
  }
  else {
    *(undefined8 *)(puVar4 + -0x78) = 0x401f71;
    puts("Access denied");
  }
  if (local_20 == *(long *)(in_FS_OFFSET + 0x28)) {
    return 0;
  }
                    /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}


```

Below is a cleaned-up version of the decompiled code, where variable names have been renamed for clarity and unnecessary low-level artifacts have been removed within the Ghidra environment to better reflect the program’s actual logic.


### Code Analysis

The program stores a hardcoded password inside the binary, which is copied into the `password` buffer at runtime.  
This password is a long hexadecimal string that directly corresponds to the picoCTF flag.

The program then prompts the user to enter a password and reads the input using `fgets`.  
The entered input is compared against the stored password using `strncmp`.

If the comparison returns zero, the input matches the stored password and the program prints a success message along with the flag.  
Otherwise, an access denied message is displayed.

Because the password is stored in plaintext within the binary, no real cryptographic protection is applied.  
This allows the flag to be recovered directly by analyzing the binary without needing to guess or brute-force the password.


```c

undefined8 main(void)

{
  int valid_password;
  undefined1 *puVar1;
  long in_FS_OFFSET;
  undefined1 auStack_a8 [8];
  size_t local_a0;
  undefined8 local_98;
  char *local_90;
  char password [104];
  long local_20;
  char *input;
  size_t size_input;
  
  local_20 = *(long *)(in_FS_OFFSET + 0x28);
  local_a0 = 100;
  local_98 = 99;

  builtin_strncpy(password,
                  "7069636f4354467b5539585f556e5034636b314e365f42316e34526933535f31613561336633397d"
                  ,0x51);
  password[0x51] = '\0';
  password[0x52] = '\0';
  password[0x53] = '\0';
  password[0x54] = '\0';
  password[0x55] = '\0';
  password[0x56] = '\0';
  password[0x57] = '\0';
  password[0x58] = '\0';
  password[0x59] = '\0';
  password[0x5a] = '\0';
  password[0x5b] = '\0';
  password[0x5c] = '\0';
  password[0x5d] = '\0';
  password[0x5e] = '\0';
  password[0x5f] = '\0';
  password[0x60] = '\0';
  password[0x61] = '\0';
  password[0x62] = '\0';
  password[99] = '\0';
  local_90 = puVar1 + -0x70;
  *(undefined8 *)(puVar1 + -0x78) = 0x401eee;
  printf("Enter the password to unlock this file: ");
  input = local_90;
  size_input = local_a0;
  *(undefined8 *)(puVar1 + -0x78) = 0x401f0f;
  fgets(input,(int)size_input,(FILE *)stdin);
  input = local_90;
  *(undefined8 *)(puVar1 + -0x78) = 0x401f2a;
  printf("You entered: %s\n",input);
  input = local_90;
  size_input = local_a0;
  *(undefined8 *)(puVar1 + -0x78) = 0x401f47;
  valid_password = strncmp(input,password,size_input);
  if (valid_password == 0) {
    *(undefined8 *)(puVar1 + -0x78) = 0x401f57;
    puts(
        "Password correct, please see flag: 7069636f4354467b5539585f556e5034636b314e365f42316e345269 33535f31613561336633397d"
        );
    *(undefined8 *)(puVar1 + -0x78) = 0x401f63;
    puts(password);
  }
  else {
    *(undefined8 *)(puVar1 + -0x78) = 0x401f71;
    puts("Access denied");
  }
```


This is a cleaned and simplified C version of the program logic, without memory addresses or low-level details.


```c
int main(void) {
    char password[104];
    char input[100];

    strncpy(password,
        "7069636f4354467b5539585f556e5034636b314e365f42316e34526933535f31613561336633397d",
        0x51
    );

    printf("Enter the password to unlock this file: ");
    fgets(input, 100, stdin);

    printf("You entered: %s\n", input);

    if (strncmp(input, password, 100) == 0) {
        puts("Password correct, please see flag: 7069636f4354467b5539585f556e5034636b314e365f42316e34526933535f31613561336633397d");
        puts(password);
    } else {
        puts("Access denied");
    }

    return 0;
}
```

## Flag
picoCTF{U9X_UnP4ck1N6_B1n4Ri3S_1a5a3f39}



