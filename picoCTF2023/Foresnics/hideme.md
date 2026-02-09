# hideme

<img width="886" height="520" alt="image" src="https://github.com/user-attachments/assets/faddd81a-d64a-4471-8a37-76d2ded5c4fd" />

- --

## Objective
The objective of this challenge is to analyze an image file and recover a hidden
flag using forensic and steganography techniques.

- --

## Description
The challenge states that an image was sent back and forth between two
individuals and may contain hidden information. The goal is to investigate the
file and determine if additional data is embedded inside the image.

- --

## Methodology

### 1. Initial File Inspection

First, the provided image file is analyzed to determine whether it contains
hidden or embedded files. Since steganography challenges often hide additional
data inside images, forensic tools are used to inspect the file structure.

The tool **binwalk** is used to scan the image for embedded files and compressed
data.

```bash
binwalk flag.png
```
<img width="886" height="351" alt="image" src="https://github.com/user-attachments/assets/eabad339-4e41-4cf8-bae7-701d3a06a327" />

The output reveals that the PNG file contains additional embedded data, including compressed and archived content.

### 2. Extracting Embedded Files
Since binwalk detects hidden data structures, the automatic extraction option is used:
```bash
binwalk -e flag.png
```
This command extracts all embedded files and creates a new directory named:

_flag.png.extracted

### 3. Exploring Extracted Content
Next, the extracted directory is explored:

```bash
cd _flag.png.extracted
ls
```
<img width="886" height="386" alt="image" src="https://github.com/user-attachments/assets/b877871b-5057-4011-afe1-4ac6207c5843" />



Inside the directory, multiple elements are found, including:

A ZIP archive

A directory named secret

The investigation continues by navigating into the secret folder:

```bash
cd secret
ls
```
Inside this directory, another image file named flag.png is discovered.

### 4. Inspecting the Hidden Image
The discovered flag.png is opened using an image viewer. Upon inspection, the hidden message becomes visible within the image.
<img width="886" height="664" alt="image" src="https://github.com/user-attachments/assets/1805d1f7-194d-4e4a-bb8f-3b415798b6f2" />

### 5.Result
By analyzing the image using forensic tools and extracting hidden archives, the embedded image containing the flag was successfully recovered.

Flag
picoCTF{Hiddinng_An_imag3_within_@n_ima9e_ad9f6587}
