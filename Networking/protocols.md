# Network Protocols for SOC Analyst

## TCP

Transmission Control Protocol.

Features:
- connection-oriented
- reliable communication
- guarantees packet delivery
- uses three-way handshake

Example:
Web browsing, SSH, HTTPS

TCP handshake:

1. SYN
2. SYN-ACK
3. ACK


---

## UDP

User Datagram Protocol.

Features:
- connectionless
- faster than TCP
- no delivery guarantee

Used for:
- DNS
- VoIP
- streaming


---

# DNS

Domain Name System.

Purpose:
Converts domain names into IP addresses.

Example:

google.com → 142.250.x.x


SOC importance:
Attackers can use DNS for:
- malicious domains
- data exfiltration
- command and control communication


Useful command:

```bash
nslookup example.com
