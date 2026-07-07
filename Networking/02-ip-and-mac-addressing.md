# IP/MAC Addressing, ARP, DHCP, Subnetting

- **Public IP** — identifies a device on the internet. **Private IP** — identifies a device on a local network (e.g. `192.168.1.1`).
- **MAC address** — unique hardware ID (e.g. `a4:c3:f0:85:ac:2d`); first half = manufacturer, second half = device.
- **Ping/ICMP** — tests connectivity and latency between two devices.
- **ARP** — resolves IP → MAC within a local network (Request = broadcast "who has this IP?", Reply = "that's me, here's my MAC"). **ARP spoofing** = forging replies to redirect traffic (MITM setup) — a key SOC red flag.
- **DHCP (DORA)** — automatic IP assignment: Discover → Offer → Request → ACK.
- **Subnetting** — splitting one network into smaller segments for efficiency, security, and control. Key addresses: network address (e.g. `.0`), host address, default gateway.
