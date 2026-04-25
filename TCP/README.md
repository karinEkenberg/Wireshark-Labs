# TCP (Transmission Control Protocol) Analysis

## Overview
This lab focuses on the lifecycle of a **TCP** connection within the `tfp_capture.pcap` file. Unlike UDP, TCP is a connection-oriented protocol that ensures reliable, ordered, and error-checked delivery of data.

## Key Findings
* **Protocol:** TCP (Transmission Control Protocol)
* **Handshake:** Verified a successful 3-way handshake at the start of the stream.
* **Reliability:** Observed sequential **Sequence Numbers** and **Acknowledgment Numbers** managing the data flow.
* **Termination:** Captured a graceful connection teardown using **FIN** flags.

---

## 1. The 3-Way Handshake (Connection Establishment)
Before any data is sent, TCP establishes a connection. This process ensures both the client and server are ready to communicate.
* **SYN:** "Let's synchronize sequence numbers."
* **SYN-ACK:** "I acknowledge your request, let's synchronize mine too."
* **ACK:** "Connection established."

<img width="1327" height="800" alt="Skärmbild 2026-04-25 065637" src="https://github.com/user-attachments/assets/2bd967a0-ac91-4ba5-8795-54fece9bd596" />


---

## 2. Sequence & Acknowledgment Numbers
TCP uses these numbers to track how much data has been sent and received. It ensures that if a packet is lost, the receiver knows exactly what is missing and can ask for a retransmission.

<img width="1327" height="800" alt="Skärmbild 2026-04-25 065807" src="https://github.com/user-attachments/assets/8ca2907d-d429-42a0-a9f8-fcb834d815bb" />

---

## 3. Connection Termination (The FIN Flag)
When the communication is finished, the devices perform a "graceful teardown" using the **FIN** (Finish) flag. This informs the other party that no more data will be sent.

<img width="1327" height="800" alt="Skärmbild 2026-04-25 070253" src="https://github.com/user-attachments/assets/da03028e-3872-480b-bdc8-89b7ba3732c5" />

---

## Security Perspective
Understanding TCP flags is vital for network security:
* **TCP Scanning:** Attackers use different flag combinations (like Stealth/SYN scans) to see which ports are open without completing a full handshake.
* **RST Attacks:** If an attacker can guess the sequence numbers, they could inject a **RST (Reset)** packet to kill a legitimate connection between two users.

## Green IT & Best Practices
TCP's "Selective Acknowledgment" (SACK) feature is a great example of Green IT. Instead of resending everything when one packet gets lost, TCP can resend *only* the missing piece. This minimizes unnecessary data retransmissions, saving both bandwidth and electrical energy in data centers.
