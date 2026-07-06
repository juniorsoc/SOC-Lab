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
```

## Common Ports

22 - SSH  
23 - Telnet  
25 - SMTP  
53 - DNS  
80 - HTTP  
443 - HTTPS  
3389 - RDP  
445 - SMB

SOC relevance:
Unexpected open ports or unusual traffic can indicate suspicious activity.

## RDP

Remote Desktop Protocol.

Port:
3389

SOC checks:
- brute force attempts
- unusual login locations

## SMB

Server Message Block.

Port:
445

SOC checks:
- lateral movement
- suspicious file access

## Firewall

Firewall controls network traffic.

It can:
- allow connections
- block connections
- log activity

SOC analysts use firewall logs to investigate:
- suspicious IP addresses
- blocked connections
- unusual traffic
