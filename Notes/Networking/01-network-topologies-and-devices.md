# Network Topologies and Core Devices

## Topologies

| Topology | Layout | Pros | Cons |
|----------|--------|------|------|
| Star | All devices → central switch/hub | Reliable, easy to extend | Single point of failure (central device) |
| Bus | All devices on one shared cable | Cheap, simple | Shared bandwidth, one break = whole segment down |
| Ring | Closed loop, data flows one direction | Less cabling, easier fault detection | Every packet crosses every device, one broken link disrupts the loop |

## Switch vs Router

| | Switch | Router |
|---|--------|--------|
| Connects | Devices on the *same* network | *Separate* networks |
| Uses | MAC address / port table | IP addressing, routing logic |
| Sits at | Inside a LAN | Boundary between LAN and other networks/internet |

## Switch vs Hub

| | Hub | Switch |
|---|-----|--------|
| Behavior | Forwards every packet to every device | Learns MAC-to-port mapping, forwards only to the right port |
| Result | More traffic/congestion | Efficient |

## VLANs

Logically separates devices on the same physical switch, via configuration only (no extra hardware). Devices in different VLANs can share resources (e.g. internet) but can't talk to each other directly — common way to isolate departments/systems for security without separate physical infrastructure.

## Router / Switch / VLAN together

- Router — Layer 3, has a config interface (port forwarding, firewall rules), picks paths via routing protocols (OSPF, RIP) based on hop count, reliability, speed.
- Switch — forwards Ethernet frames by MAC address.
  - Layer 2 switch: MAC only, can't route between IP networks.
  - Layer 3 switch: can also forward by IP, handles multiple networks — absorbs part of a router's job.
