# TCP, UDP, and Ports

**TCP** — connection-oriented, reliable, ordered. Three-way handshake: SYN → SYN/ACK → ACK. Closed with FIN/ACK exchange; RST = abrupt termination. Slower but guarantees delivery.

**UDP** — connectionless, no handshake, no delivery guarantee. Much faster. Used for streaming, gaming, DNS, DHCP — where speed matters more than perfection.

**Common ports:**
| Port | Protocol |
|---|---|
| 21 | FTP |
| 22 | SSH |
| 80 | HTTP |
| 443 | HTTPS |
| 445 | SMB |
| 3389 | RDP |

**SOC tip:** services on non-standard ports (SSH on 2222, RDP on 3390) can indicate evasion attempts — worth flagging.
