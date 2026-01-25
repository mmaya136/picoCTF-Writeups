# interencdec

<img width="954" height="502" alt="image" src="https://github.com/user-attachments/assets/14aefeae-b5ad-44ae-9184-31e342e95914" />


## Objective
The objective of this challenge is to recover the original message hidden inside a file by applying multiple decoding techniques.

## Description
The challenge provides a file containing an encoded message.  
The hint suggests that multiple decoding processes are required to reveal the real meaning of the content.

By analyzing the encoded text and applying different decoding methods, the original message and flag can be recovered.

## Methodology
First, the provided file is downloaded and its contents are displayed using the `cat` command. 
The output is identified as a Base64-encoded string, which is then decoded using Base64. The resulting output remains encoded and appears to be another Base64 string, so a second Base64 decoding step is applied.


<img width="567" height="204" alt="image" src="https://github.com/user-attachments/assets/f1a2c08d-547d-4e7e-9b5c-8bd0681b69d8" />


After the second Base64 decoding, the output becomes readable text but does not form a meaningful message. This indicates the use of a Caesar cipher. By analyzing the text with a Caesar cipher decoder and testing different shift values, the correct shift is identified, revealing the original plaintext and the flag.

<img width="510" height="431" alt="image" src="https://github.com/user-attachments/assets/e413a6af-ee4a-4b3a-a2a2-551ec8c25552" />


## Flag
picoCTF{caesar_d3cr9pt3d_ea60e00b}
