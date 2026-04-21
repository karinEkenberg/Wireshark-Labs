# Protocol Analysis: ICMP (Ping)

## Overview
Analysis of ICMP Echo messages to verify network connectivity and path distance.

## Key Findings
* **Request:** Packet 75 (Type 8) 
* **Reply:** Packet 78 (Type 0) 
* **Response Time:** 0.348 ms (Extremely fast) 

## Evidence Captures

### 1. Echo Request/Reply Sequence

<img width="1328" height="800" alt="Skärmbild 2026-04-21 145931" src="https://github.com/user-attachments/assets/b8cd90d1-4b44-46f0-84a9-2e6b88b868c1" />

*Displays the successful ping from 86.64.145.29 to 10.251.23.139.* 

### 2. ICMP Header Details

<img width="646" height="234" alt="Skärmbild 2026-04-21 150208" src="https://github.com/user-attachments/assets/b554ec50-f466-4e18-ac14-610d54c5f942" />
<img width="663" height="241" alt="Skärmbild 2026-04-21 150143" src="https://github.com/user-attachments/assets/18898490-b8bc-4500-834d-637e4575aa11" />


*Identification of Type 8 for Echo Request.* 

### 3. TTL Analysis

<img width="663" height="301" alt="Skärmbild 2026-04-21 150542" src="https://github.com/user-attachments/assets/298dac37-aab0-4735-80a4-720c542e3c74" />


*The TTL of 59 indicates that the packet has traversed 5 hops before capture.*
