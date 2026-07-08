# TCP/IP Basics for SOC Analyst

Communication model computers use to exchange data over networks. SOC analysts need this to understand network traffic, attacks, suspicious connections, and firewall logs.

## TCP/IP layers

| Layer | Responsible for | Protocols/examples |
|-------|-------------------|----------------------|
| Application | User-facing services | HTTP/HTTPS, DNS, SSH, FTP, SMTP |
| Transport | How data moves (TCP/UDP) | TCP (handshake: SYN → SYN-ACK → ACK), UDP (fast, no connection — DNS, streaming, VoIP) |
| Internet | Addressing + routing | IP, ICMP |
| Network Access | Physical transmission | Ethernet, MAC addresses |

## Key concepts

- **IP address** — identifies a device on a network (e.g. `192.168.1.50`)
- **Port** — identifies a service (22 SSH, 80 HTTP, 443 HTTPS, 53 DNS, 3389 RDP)
- **Routing** — routers use routing tables to decide where packets go

## Useful Linux commands

| Command | Shows |
|---------|-------|
| `ip addr` | IP address |
| `ip route` | Routing table |
| `ss -tulpn` | Active connections |
| `ping google.com` | Connectivity test |
