# Firewalls, Port Forwarding, VPNs

## Firewalls

Decides what traffic can enter/leave a network. Operates at Layer 3 (source/destination IP) and Layer 4 (ports, TCP/UDP), inspecting packets against configured rules.

| | Stateful | Stateless |
|---|----------|-----------|
| Tracks | Full connection context | Each packet individually |
| Smarter about | Suspicious behavior over a session | — |
| Cost | More resource-intensive | Lighter |
| Holds up better under | Normal load | High volume (e.g. DDoS) |

Can be dedicated hardware or software. Stateful vs stateless is the key distinction to know.

## Port forwarding

Exposes a service on a private/internal network to the internet. Router maps incoming traffic on a public port → a specific internal device + port. Internal private IP stays hidden from outside.

Different from a firewall: port forwarding opens the pathway, firewall decides if traffic is allowed through it. Usually work together, configured on the router.

## VPN

Encrypted tunnel between devices over the internet — makes separate networks behave like one private network.

Uses: connect distributed offices to shared internal resources, encrypt traffic on untrusted/public networks, hide browsing from an ISP (only holds if the VPN provider itself doesn't log traffic).

| Protocol | Notes |
|----------|-------|
| PPP | Base auth/encryption layer, can't route beyond a local link alone |
| PPTP | Extends PPP for internet routing, simple, weak encryption by modern standards |
| IPSec | Encrypts on top of IP, stronger encryption, more complex config |
