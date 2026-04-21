# ARP Analysis Lab

## Overview
In this lab, I analyzed a packet capture containing an **ARP Storm/Sweep**. The purpose was to identify the behavior of the Address Resolution Protocol when a device attempts to map multiple IP addresses on a local network.

## Key Findings
* **Traffic Pattern:** The capture consists of a rapid succession of **ARP Requests**.
* **Source Device:** A Cisco device (`00:07:0d:af:f4:54`) is the primary initiator.
* **Missing Replies:** Notably, no **ARP Replies** were found in this specific capture. This indicates that the target IP addresses were either inactive or located on a different network segment.

---

## 1. Network Traffic Overview (The Storm)
This image shows the sequential "Who has...?" requests. Note that all requests are sent to the **Broadcast** address, meaning every device on the segment receives them.

<img width="1328" height="800" alt="Skärmbild 2026-04-15 144301" src="https://github.com/user-attachments/assets/31daec8b-9e5d-48f8-8962-5d9e5cd1ecda" />

---

## 2. Anatomy of an ARP Request
By inspecting a single packet, we can see the technical details of the request. 

<img width="662" height="246" alt="Skärmbild 2026-04-15 144807" src="https://github.com/user-attachments/assets/b070a234-ac99-4eae-9953-9236b8b4a473" />

* **Opcode:** `request (1)` – Confirms the device is asking for information.
* **Target MAC Address:** `00:00:00:00:00:00` – This is a placeholder since the sender doesn't know the physical address yet.
* **Sender IP:** `24.166.172.1` – The device looking for answers.

---

## 3. Analysis of Missing Responses
In a healthy, one-to-one communication, each `request (1)` should be followed by a `reply (2)`. In this lab, the lack of replies suggests a network discovery phase or a potential reconnaissance scan.

> **Analogy:** This is like a postman knocking on 100 doors in a row. If no one opens, it doesn't mean the protocol is broken; it means the houses are currently empty.

---

## Security Perspective
From a security engineer's viewpoint, an ARP Storm like this is a "Signal". 
* **Incident Response:** If this occurred unexpectedly, it could indicate a compromised host performing internal reconnaissance (scanning for targets).
* **Network Health:** It could also be a misconfigured router or a "flapping" interface trying to rebuild its ARP cache.
