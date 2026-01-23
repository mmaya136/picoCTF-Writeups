# Ph4nt0m 1ntrud3r

<img width="953" height="683" alt="image" src="https://github.com/user-attachments/assets/932eddf8-9ebd-40f3-b5a5-a043ad34ed5b" />

## Objective
The objective of this challenge is to recover a hidden flag by analyzing a **PCAP file** and identifying how an attacker exfiltrated data using abnormal TCP behavior.

---

## Description
The challenge provides a **network traffic capture (PCAP)** containing evidence of a system compromise.  
The attacker has hidden sensitive data within TCP traffic in a subtle and well-timed manner.

By inspecting the packets and understanding how TCP is being misused, we can extract the concealed data and reconstruct the flag.

---

## Provided Data
The challenge provides a single artifact:

- **Network Traffic PCAP file**

Upon inspection, the following characteristics are observed:

- Multiple **TCP packets marked as retransmissions**
- **TCP SYN packets containing payload data**
- Traffic consistently targeting **destination port 80**
- Small payload sizes repeated across several packets

This behavior is highly unusual in normal TCP communication.

---

## Vulnerability Explanation
In standard TCP operation, **SYN packets are used only to initiate a connection** and do **not carry application data**.

However, in this PCAP:
- Several **SYN packets include payload bytes**
- These packets are repeatedly retransmitted
- The payload is fragmented across multiple packets

This reveals a **covert data exfiltration technique**, where the attacker abuses TCP behavior to hide data inside retransmitted SYN packets.

Because retransmissions and SYN packets are common on real networks, this technique allows data to be exfiltrated **without triggering simple detection mechanisms**.
By extracting and reassembling the TCP payloads in chronological order, it becomes evident that the recovered data forms a Base64-encoded string, which can then be decoded to reveal the hidden message (the flag)

<img width="1913" height="958" alt="image" src="https://github.com/user-attachments/assets/5591f816-0773-4791-a2c2-fcce26f5667b" />

<img width="565" height="209" alt="image" src="https://github.com/user-attachments/assets/93b4f0a0-9b86-4266-83e6-a4629dff0847" />

We then remove the extraneous characters and fragments that do not belong to the encoding
<img width="582" height="72" alt="image" src="https://github.com/user-attachments/assets/29ad9aea-5321-473b-8e18-98f2c6dee60c" />


## Flag
picoCTF{1t_w4nt_th4_34sy_bh_4r_4b5790}
