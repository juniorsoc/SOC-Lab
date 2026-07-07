# Firewalls, Port Forwarding, VPN

**Firewall** — controls what traffic enters/exits a network based on source/destination IP (L3) and port/protocol (L4).
- **Stateful** — tracks whole connections, smarter, more resource-intensive.
- **Stateless** — checks each packet against fixed rules, lighter but less intelligent; better under DDoS load.

**Port forwarding** — exposes a local service to the internet by mapping a router's public IP:port to an internal device. Different from a firewall: port forwarding opens the door, the firewall decides who passes through.

**VPN** — creates an encrypted tunnel between devices over the internet. Used for connecting offices, privacy (encryption on public Wi-Fi), and anonymity from an ISP.
- **PPP** — base authentication/encryption, not routable alone.
- **PPTP** — adds internet routing, easy setup, weak encryption.
- **IPSec** — strong encryption, more complex setup.
