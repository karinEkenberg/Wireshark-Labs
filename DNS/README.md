# Protocol Analysis: DNS (Domain Name System)

## Overview
This lab focuses on the analysis of **DNS** traffic captured in the `netlink-conntrack.pcap` file. The Domain Name System acts as the "phonebook of the internet," translating human-readable domain names (e.g., `www.example.com`) into machine-readable IP addresses.

## Key Findings
* **Transport Protocol:** DNS utilized **UDP** on port **53** for these queries.
* **Query Types:** The client requested both **Type A** (IPv4) and **Type AAAA** (IPv6) records.
* **Transaction Matching:** Successful matching of Queries and Responses was verified using Transaction IDs (e.g., `0x51ee`).
* **Recursion:** The client explicitly requested recursive lookups from the server.

---

## 1. DNS Query & Response Flow
The following image illustrates the communication flow between the client (`10.0.2.15`) and the DNS server (`10.0.2.3`). Each query is followed by a corresponding response, ensuring the client receives the necessary IP information to proceed with higher-layer protocols (like HTTP).

<img width="1328" height="800" alt="Skärmbild 2026-04-24 183441" src="https://github.com/user-attachments/assets/2bd20a4a-03d8-4359-8c3c-5c53aa61763c" />

---

## 2. DNS Flags: Recursion Desired
In the packet details of the Query, the `Recursion desired` flag is set to `1`. This indicates that the client expects the DNS server to fully resolve the domain name, even if the server has to contact other name servers to find the answer.

<img width="1328" height="800" alt="Skärmbild 2026-04-24 183919" src="https://github.com/user-attachments/assets/975cf4f7-8e25-4531-85e8-0c1ef5f901db" />

---

## 3. The DNS Answer (A-Record)
The response from the server provides the final mapping. In this specific capture, the server resolved the domain to an IPv4 address.
* **Queried Domain:** `www.example.com`
* **Resolved IP Address:** `93.184.216.34`
* **Reply Code:** `No error (0)`, indicating a successful lookup.

<img width="1328" height="800" alt="Skärmbild 2026-04-24 204719" src="https://github.com/user-attachments/assets/ecfb484d-5242-480b-b0bd-3ebdf1b9a018" />

---

## Security Perspective
Analyzing DNS is a fundamental skill for security investigations. 
* **Anomaly Detection:** If a client suddenly generates a high volume of failed queries (`NXDOMAIN`), it could indicate a Domain Generation Algorithm (DGA) used by malware.
* **Authoritative Answers:** In this lab, the `Authoritative` flag was `0`, meaning the response likely came from a cache rather than the primary owner of the domain. Identifying the source of DNS data is key to preventing DNS Spoofing.

## Green IT & Best Practices
* **UDP Efficiency:** By using UDP instead of TCP, DNS avoids the overhead of a 3-way handshake, reducing network congestion and energy consumption.
* **Caching (TTL):** The Time-To-Live (TTL) value found in the answers ensures that the client caches the result, preventing redundant network requests and saving bandwidth.
