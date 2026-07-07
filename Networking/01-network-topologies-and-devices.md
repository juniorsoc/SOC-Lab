# Network Topologies and Core Devices

**Topologies:**
- **Star** — all devices connect to a central switch. Reliable, easy to expand, but the switch is a single point of failure.
- **Bus** — all devices share one backbone cable. Cheap, but one break kills the segment.
- **Ring** — devices form a loop, data travels one direction. Efficient cabling, but one broken link disrupts everything.

**Switch vs Router:**
- **Switch** connects devices *within* the same network — forwards traffic based on MAC address.
- **Router** connects *different* networks and routes traffic between them (Layer 3).

**Switch vs Hub:** a hub broadcasts every packet to all devices (inefficient). A switch learns MAC-to-port mappings and forwards only to the correct port.

**VLAN:** logically segments devices on the same physical switch — e.g. Sales and Accounting share a switch but can't reach each other, for security.

**SOC relevance:** knowing topology tells you where to look when diagnosing traffic issues or interpreting packet captures.
