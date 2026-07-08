# OSI Model, Packets & Frames

`Networking`

## OSI Model

7-layer model describing how devices send/receive/interpret data. Lets equipment from different vendors talk to each other.

Sending: data goes layer 7 → 1, each layer adds a header (encapsulation).
Receiving: reverse — each layer strips its header on the way up (decapsulation).

Mnemonic (7→1): All People Seem To Need Data Processing
Application, Presentation, Session, Transport, Network, Data Link, Physical

| # | Layer | What it does | Examples | Attacks here |
|---|-------|--------------|----------|--------------|
| 7 | Application | UI for using the network (browser, email) | HTTP, HTTPS, DNS, FTP | XSS, SQLi |
| 6 | Presentation | Translates formats, encrypts/compresses | TLS/SSL | Cert issues, TLS downgrade |
| 5 | Session | Opens/holds/closes the connection | NetBIOS, RPC, SMB | Session hijacking |
| 4 | Transport | TCP or UDP — how reliably data moves | TCP, UDP | Port scanning, DoS |
| 3 | Network | Routes packets, uses IP | IP, OSPF, RIP | IP spoofing, TTL tricks |
| 2 | Data Link | Adds MAC address for local delivery | MAC, Ethernet, switches | ARP spoofing, MAC flooding, MITM |
| 1 | Physical | Actual bits on the wire/air | Ethernet, Wi-Fi, fiber | Physical access, cable tap |

Rule of thumb: layers 1-4 = network-level attacks, layers 5-7 = application-level attacks.

### Layer 4 — TCP vs UDP

| | TCP | UDP |
|---|-----|-----|
| Reliable | Guarantees delivery + order | No guarantee |
| Speed | Slower, more overhead | Faster |
| Connection | 3-way handshake | None |
| Used for | Web, email, file transfer | Streaming, calls, games |

### Layer 3 — routing

Packet gets tagged with destination IP. Router checks hop count, path reliability, path speed, then picks best route. Decided by routing protocols, not the router guessing.

## Packets vs Frames

Quick rule: IP addresses = packet (Layer 3). MAC addresses = frame (Layer 2).

| | Packet | Frame |
|---|--------|-------|
| Layer | 3 | 2 |
| Contains | IP addresses + payload | Wraps packet, adds MAC addresses |

Why split data into chunks: one big transfer could overload the network, and if something fails mid-way you only resend a small piece.

Key IP header fields:
- TTL — expiration counter, drops packet after N hops
- Checksum — lets receiver verify data wasn't corrupted
- Source/destination address — so a reply can find its way back
