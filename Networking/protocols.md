# Network Protocols for SOC Analyst

## TCP vs UDP

| | TCP | UDP |
|---|-----|-----|
| Connection | Connection-oriented | Connectionless |
| Reliability | Guarantees delivery | No guarantee |
| Speed | Slower | Faster |
| Handshake | SYN → SYN-ACK → ACK | None |
| Used for | Web browsing, SSH, HTTPS | DNS, VoIP, streaming |

## DNS

Converts domain names into IP addresses (e.g. `google.com → 142.250.x.x`).

SOC relevance — attackers use DNS for: malicious domains, data exfiltration, C2 (command and control) communication.

Command: `nslookup example.com`

## Common ports

| Port | Service |
|------|---------|
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 3389 | RDP |
| 445 | SMB |

Unexpected open ports or unusual traffic = worth investigating.

## RDP (3389)

SOC checks: brute force attempts, unusual login locations.

## SMB (445)

SOC checks: lateral movement, suspicious file access.

## Firewall

Controls traffic — allow, block, log. SOC analysts use firewall logs to investigate suspicious IPs, blocked connections, unusual traffic.
