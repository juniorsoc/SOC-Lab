# TCP/IP Basics for SOC Analyst

## What is TCP/IP?

TCP/IP is a communication model used by computers to exchange data over networks.

SOC analysts need TCP/IP knowledge to understand:
- network traffic
- attacks
- suspicious connections
- firewall logs

---

# TCP/IP Layers

## 1. Application Layer

Protocols:
- HTTP/HTTPS
- DNS
- SSH
- FTP
- SMTP

Example:
User opens a website using HTTPS.

---

## 2. Transport Layer

Main protocols:

### TCP
- connection-oriented
- reliable communication
- uses handshake

TCP three-way handshake:

1. SYN
2. SYN-ACK
3. ACK


### UDP
- faster
- no connection
- used for DNS, streaming, VoIP

---

## 3. Internet Layer

Responsible for addressing and routing.

Protocols:
- IP
- ICMP

Example:
192.168.1.10 communicates with another host.

---

## 4. Network Access Layer

Responsible for:
- Ethernet
- MAC addresses
- physical transmission

---

# Important SOC Concepts

## IP Address

Identifies a device on a network.

Example:

192.168.1.50

---

## Port

Identifies a service.

Common ports:

22 - SSH

80 - HTTP

443 - HTTPS

53 - DNS

3389 - RDP

---

## Routing

Routing decides where packets go.

Routers use routing tables to forward traffic.

---

## Useful Linux Commands

Show IP address:

ip addr


Show routes:

ip route


Show active connections:

ss -tulpn


Test connectivity:

ping google.com
