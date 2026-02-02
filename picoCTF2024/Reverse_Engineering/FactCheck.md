# FactCheck

<img width="955" height="683" alt="image" src="https://github.com/user-attachments/assets/32c6ca9c-f46a-4bf8-846d-00a92e56b5c5" />


## Objective
The objective of this challenge is to analyze a Linux binary, understand how it constructs the flag internally, and recover the full flag through reverse engineering.

## Description
The provided binary assembles the flag dynamically at runtime instead of storing it as a single string.  
By examining the program’s internal logic, it is possible to reconstruct the final flag without executing the program normally.

---

## Methodology

### 1. Initial Analysis

First, the binary is inspected using basic tools such as `file` and `strings` to understand its format and contents.  
The file is identified as a 64-bit ELF executable, dynamically linked and not stripped, which makes reverse engineering easier.

Running `strings` reveals partial flag-like content (`picoCTF{...}`), indicating that the flag is likely embedded in the binary but constructed dynamically.

<img width="886" height="456" alt="image" src="https://github.com/user-attachments/assets/f29cbb9f-c03c-4a48-a8be-49c8dd80d544" />

---

### 2. Static Analysis with Ghidra

Next, the binary is loaded into **Ghidra** to perform static analysis.  
Using Ghidra’s decompiler, the `main` function is examined to understand the program’s logic.

Below is the decompiled code obtained from Ghidra, which shows how the flag is assembled internally:

```c
undefined8 main(void)


{
  char cVar1;
  char *pcVar2;
  long in_FS_OFFSET;
  allocator local_249;
  string str_flag [32];
  string local_228 [32];
  string local_208 [32];
  string local_1e8 [32];
  string local_1c8 [32];
  string local_1a8 [32];
  string local_188 [32];
  string local_168 [32];
  string local_148 [32];
  string local_128 [32];
  string local_108 [32];
  string local_e8 [32];
  string local_c8 [32];
  string local_a8 [32];
  string local_88 [32];
  string local_68 [32];
  string local_48 [40];
  long local_20;
  
  local_20 = *(long *)(in_FS_OFFSET + 0x28);
  std::allocator<char>::allocator();
                    /* try { // try from 001012cf to 001012d3 has its CatchHandler @ 00101975 */
  std::__cxx11::string::string(str_flag,"picoCTF{wELF_d0N3_mate_",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 0010130a to 0010130e has its CatchHandler @ 00101996 */
  std::__cxx11::string::string(local_228,"7",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101345 to 00101349 has its CatchHandler @ 001019b1 */
  std::__cxx11::string::string(local_208,"5",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101380 to 00101384 has its CatchHandler @ 001019cc */
  std::__cxx11::string::string(local_1e8,"9",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001013bb to 001013bf has its CatchHandler @ 001019e7 */
  std::__cxx11::string::string(local_1c8,"3",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001013f6 to 001013fa has its CatchHandler @ 00101a02 */
  std::__cxx11::string::string(local_1a8,"0",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101431 to 00101435 has its CatchHandler @ 00101a1d */
  std::__cxx11::string::string(local_188,"4",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 0010146c to 00101470 has its CatchHandler @ 00101a38 */
  std::__cxx11::string::string(local_168,"a",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001014a7 to 001014ab has its CatchHandler @ 00101a53 */
  std::__cxx11::string::string(local_148,"e",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001014e2 to 001014e6 has its CatchHandler @ 00101a6e */
  std::__cxx11::string::string(local_128,"a",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 0010151d to 00101521 has its CatchHandler @ 00101a89 */
  std::__cxx11::string::string(local_108,"d",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101558 to 0010155c has its CatchHandler @ 00101aa4 */
  std::__cxx11::string::string(local_e8,"b",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101593 to 00101597 has its CatchHandler @ 00101abf */
  std::__cxx11::string::string(local_c8,"2",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 001015ce to 001015d2 has its CatchHandler @ 00101ada */
  std::__cxx11::string::string(local_a8,"6",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101606 to 0010160a has its CatchHandler @ 00101af5 */
  std::__cxx11::string::string(local_88,"4",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 0010163e to 00101642 has its CatchHandler @ 00101b0d */
  std::__cxx11::string::string(local_68,"3",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
  std::allocator<char>::allocator();
                    /* try { // try from 00101676 to 0010167a has its CatchHandler @ 00101b25 */
  std::__cxx11::string::string(local_48,"8",&local_249);
  std::allocator<char>::~allocator((allocator<char> *)&local_249);
                    /* try { // try from 00101699 to 0010185f has its CatchHandler @ 00101b3d */
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_208);
  if (*pcVar2 < 'B') {
    std::__cxx11::string::operator+=(str_flag,local_c8);
  }
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_a8);
  if (*pcVar2 != 'A') {
    std::__cxx11::string::operator+=(str_flag,local_68);
  }
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_1c8);
  cVar1 = *pcVar2;
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_148);
  if ((int)cVar1 - (int)*pcVar2 == 3) {
    std::__cxx11::string::operator+=(str_flag,local_1c8);
  }
  std::__cxx11::string::operator+=(str_flag,local_1e8);
  std::__cxx11::string::operator+=(str_flag,local_188);
  pcVar2 = (char *)std::__cxx11::string::operator[]((ulong)local_168);
  if (*pcVar2 == 'G') {
    std::__cxx11::string::operator+=(str_flag,local_168);
  }
  std::__cxx11::string::operator+=(str_flag,local_1a8);
  std::__cxx11::string::operator+=(str_flag,local_88);
  std::__cxx11::string::operator+=(str_flag,local_228);
  std::__cxx11::string::operator+=(str_flag,local_128);
  std::__cxx11::string::operator+=(str_flag,'}');
  std::__cxx11::string::~string(local_48);
  std::__cxx11::string::~string(local_68);
  std::__cxx11::string::~string(local_88);
  std::__cxx11::string::~string(local_a8);
  std::__cxx11::string::~string(local_c8);
  std::__cxx11::string::~string(local_e8);
  std::__cxx11::string::~string(local_108);
  std::__cxx11::string::~string(local_128);
  std::__cxx11::string::~string(local_148);
  std::__cxx11::string::~string(local_168);
  std::__cxx11::string::~string(local_188);
  std::__cxx11::string::~string(local_1a8);
  std::__cxx11::string::~string(local_1c8);
  std::__cxx11::string::~string(local_1e8);
  std::__cxx11::string::~string(local_208);
  std::__cxx11::string::~string(local_228);
  std::__cxx11::string::~string(str_flag);
  if (local_20 == *(long *)(in_FS_OFFSET + 0x28)) {
    return 0;
  }
                    /* WARNING: Subroutine does not return */
  __stack_chk_fail();
}

```


The code has been modified and simplified to make the program logic easier to understand.

```c
undefined8 main(void)
{
  allocator local_variable;
  string str_flag [32];
  string char1 [32];
  string char2 [32];
  string char3 [32];
  string char4 [32];
  string char5 [32];
  string char6 [32];
  string char7 [32];
  string char8 [32];
  string char9 [32];
  string char10 [32];
  string char11 [32];
  string char12 [32];
  string char13 [32];
  string char14 [32];
  string char15 [32];
  string char16 [40];

  std::string::string(str_flag,"picoCTF{wELF_d0N3_mate_",&local_variable);

  std::string::string(char1,"7",&local_variable);
  std::string::string(char2,"5",&local_variable);
  std::string::string(char3,"9",&local_variable);
  std::string::string(char4,"3",&local_variable);
  std::string::string(char5,"0",&local_variable);
  std::string::string(char6,"4",&local_variable);
  std::string::string(char7,"a",&local_variable);
  std::string::string(char8,"e",&local_variable);
  std::string::string(char9,"a",&local_variable);
  std::string::string(char10,"d",&local_variable);
  std::string::string(char11,"b",&local_variable);
  std::string::string(char12,"2",&local_variable);
  std::string::string(char13,"6",&local_variable);
  std::string::string(char14,"4",&local_variable);
  std::string::string(char15,"3",&local_variable);
  std::string::string(char16,"8",&local_variable);

  // Conditional logic appending characters to the flag
  if (char2[0] < 'B') {
    str_flag += char12;
  }
  if (char13[0] != 'A') {
    str_flag += char15;
  }
  if ((char4[0] - char8[0]) == 3) {
    str_flag += char4;
  }

  str_flag += char3;
  str_flag += char6;
  str_flag += char5;
  str_flag += char14;
  str_flag += char1;
  str_flag += char9;
  str_flag += '}';

  return 0;
}

```

### 3. Code Explanation

The program starts by initializing a base string:

picoCTF{wELF_d0N3_mate_


Then, multiple single-character strings (char1 to char16) are created, each containing a single digit or letter.

Instead of appending all characters directly, the program uses conditional checks on specific characters to decide whether to append them to the flag string.
These conditions are simple comparisons between ASCII values or equality checks.

By following the logic line by line, the exact sequence of appended characters can be reconstructed manually.

Finally, the closing brace } is appended, completing the flag.

# Flag
picoCTF{wELF_d0N3_mate_2394047a}
