# OSI Model, Packets, and Frames

**OSI layers (7→1): Application, Presentation, Session, Transport, Network, Data Link, Physical.** Data is encapsulated going down, decapsulated going up.

| Layer | Function | Attacks |
|---|---|---|
| 7 Application | HTTP, DNS, FTP | XSS, SQLi |
| 6 Presentation | TLS/SSL, encryption | TLS downgrade |
| 5 Session | Session mgmt | Session hijacking |
| 4 Transport | TCP/UDP | Port scanning, DoS |
| 3 Network | Routing, IP | IP spoofing |
| 2 Data Link | MAC, switches | ARP spoofing, MITM |
| 1 Physical | Cables, signals | Physical access |

**Packet vs Frame:** a packet (Layer 3) has IP addresses; a frame (Layer 2) wraps it with MAC addresses. IP = packets, MAC = frames.

**Key IP headers:** TTL (expiration counter), checksum (integrity check), source/destination address.
