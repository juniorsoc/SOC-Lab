# IP and MAC Addressing, ARP, DHCP, Subnetting

## Public vs Private IP

| | Public | Private |
|---|--------|---------|
| Identifies | Device on the internet | Device on local network |
| Routable on internet | Yes | No |
| Assigned by | ISP | Router (via NAT) |

## MAC address

Unique hardware ID on a device's network card, Layer 2. First half = manufacturer, second half = unique device ID.

## Ping / ICMP

Uses ICMP packets to test connectivity + measure round-trip latency. Tells you: does a path exist, and how reliable/responsive is it. Usually the first diagnostic step for a connectivity issue.

## ARP — Address Resolution Protocol

Maps IP → MAC on a local network. Each device caches these mappings (ARP cache).

Process: device broadcasts an ARP request ("who has this IP?") → owner replies with its MAC → requester caches it.

No built-in authentication → vulnerable to **ARP spoofing**: attacker sends forged replies to impersonate another device (often the default gateway) and redirect traffic through themselves. Foundation of many MITM attacks.

## DHCP — Dynamic Host Configuration Protocol

Assigns IPs automatically via a 4-step exchange (DORA):

| Step | What happens |
|------|--------------|
| Discover | Client broadcasts: "is a DHCP server here?" |
| Offer | Server proposes an IP |
| Request | Client confirms it'll take that IP |
| Acknowledgment | Server finalizes the assignment |

## Subnetting

Splits one large network into smaller segments. Each subnet has:
- Network address — identifies the subnet itself
- Host address — identifies a specific device
- Default gateway — router forwarding traffic elsewhere

Benefits: less broadcast traffic, better isolation/security (limits blast radius of a compromise), clearer logical grouping.
