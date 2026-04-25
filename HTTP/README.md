# Protocol Analysis: HTTP (Hypertext Transfer Protocol)

## Overview
This lab analyzes the **HTTP** layer within the `netlink-conntrack.pcap` file. HTTP is the fundamental protocol for data exchange on the World Wide Web, operating on a client-server request-response model.

## Key Findings
* **Workflow:** The client (`10.0.2.15`) initiates a request, and the server (`93.184.216.34`) responds with the requested data.
* **Method:** A **GET** request was used to retrieve the root document of `www.example.com`.
* **Status Code:** The server returned **200 OK**, confirming a successful transaction.
* **Data Type:** The payload was successfully identified as `text/html`.

---

## 1. The HTTP GET Request
The client initiates communication by sending a GET request. This message includes headers that describe the client's capabilities (using `curl/7.50.1` as the User-Agent) and the specific host it wants to reach.

<img width="1327" height="800" alt="Skärmbild 2026-04-25 123138" src="https://github.com/user-attachments/assets/8e21f09c-7465-41fc-aaee-3cc596b29ab3" />
*This shows the expanded GET request details in the packet details pane.*

---

## 2. The HTTP Response (200 OK)
After processing the request, the server sends back a response. The status code **200** is the most critical part, signaling that the resource was found and is being delivered. We can also see the server software identified as `ECS (iad/182A)`.

**Image source:**
<img width="1327" height="800" alt="Skärmbild 2026-04-25 123229" src="https://github.com/user-attachments/assets/f30f0dee-7f19-4308-8d21-8b17e687aadc" />

(Status Code) & (Server Info)
<img width="1327" height="800" alt="Skärmbild 2026-04-25 123306" src="https://github.com/user-attachments/assets/f56126d3-bb79-4cd8-b435-115622d05ad7" />

---

## 3. HTML Payload (The Result)
The body of the HTTP response contains the actual data. In this capture, we can see the raw HTML code, including the `<!doctype html>` declaration and CSS styles. This is the code that the browser eventually renders for the user.

<img width="1327" height="800" alt="Skärmbild 2026-04-25 123410" src="https://github.com/user-attachments/assets/cc5f9af1-82d8-4625-b6f9-dfe4f754ab16" />
*This clearly displays the "Line-based text data" section containing the HTML source code.*

---

## Security Perspective
* **Cleartext Exposure:** As seen in these captures, standard **HTTP** transmits everything in cleartext. A network analyst (or an attacker) can see the exact HTML being delivered and the headers being sent. This is why **HTTPS** (TLS) is mandatory for modern security.
* **Information Leakage:** The `Server` header identified in the response helps an attacker perform "Fingerprinting" to find specific vulnerabilities associated with that server version.

## Green IT & Best Practices
* **Header Efficiency:** This request is very small (179 bytes) and the response is 271 bytes. By keeping headers concise, the network uses less energy to transmit the same information.
* **Caching:** Headers like `Cache-Control` (seen in the response) tell the browser to save the file locally for a certain amount of time, preventing redundant downloads and saving global bandwidth.
