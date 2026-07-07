# Firewalls, Port Forwarding, and VPNs

## Firewalls

A firewall is a network device responsible for deciding what traffic is permitted to enter or leave a network. It typically operates at Layer 3, evaluating source and destination IP addresses, and at Layer 4, evaluating port numbers and the transport protocol in use (TCP or UDP). To make these decisions, a firewall inspects the packets passing through it and compares them against a configured set of rules.

There are two broad categories of firewalls. A stateful firewall tracks the full context of an entire connection rather than evaluating packets in isolation, which makes it considerably more intelligent but also more resource-intensive — it can recognize when a device is behaving suspiciously over the course of a session and respond accordingly, including blocking that device outright. A stateless firewall, by contrast, evaluates each packet individually against a fixed rule set without any awareness of connection history. This makes it lighter on system resources but less capable of detecting patterns that only emerge across multiple packets, and packets that don't clearly violate a rule may simply be allowed through by default. Stateless firewalls tend to hold up better under high-volume conditions such as a distributed denial-of-service attack, precisely because they don't need to track per-connection state.

Firewalls can be implemented as dedicated hardware appliances, which is common in larger organizations, or as software running on a general-purpose system. In practice, firewall implementations are often grouped into several broad categories, though the stateful/stateless distinction remains the most fundamental one to understand.

## Port Forwarding

Port forwarding is what makes it possible to expose a service hosted on a local, private network to the wider internet. Without it, a service running on an internal device is only reachable from within that local network, since its private IP address has no meaning outside of it.

Port forwarding works by configuring a router to map incoming traffic on a specific port of its public IP address to a specific internal device and port. Traffic arriving at the router's public address is forwarded internally to the correct device, while the internal, private IP address of that device remains invisible to anyone connecting from outside.

It's worth distinguishing port forwarding from a firewall's function: port forwarding is what opens a specific pathway for traffic to reach an internal service in the first place, while a firewall separately governs whether that traffic is actually permitted through. The two mechanisms typically work together but serve distinct purposes, and port forwarding is generally configured directly on the router itself.

## VPN — Virtual Private Network

A VPN establishes an encrypted tunnel between devices communicating over the internet, effectively allowing them to behave as though they were connected to the same private network, even when they are physically located on entirely separate networks.

VPNs serve several distinct purposes. They allow geographically distributed offices to access the same internal company resources as though everyone were on a single local network. They provide privacy by encrypting traffic so that only the sender and intended recipient can read it, which is particularly valuable on untrusted or public networks. And they can provide a degree of anonymity by hiding browsing activity from an internet service provider — though this protection only holds if the VPN provider itself doesn't log the traffic passing through it.

Several underlying technologies are commonly used to build VPN connections. PPP provides the foundational layer of authentication and encryption but cannot, on its own, route traffic beyond a local link. PPTP extends PPP to support routing across the wider internet and is relatively simple to configure, though it relies on encryption that is considered weak by modern standards. IPSec encrypts traffic on top of the existing IP protocol, offering considerably stronger encryption at the cost of more complex configuration.
