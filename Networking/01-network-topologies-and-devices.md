# Network Topologies and Core Devices

## Network Topologies

A network topology defines how devices are arranged and interconnected, which in turn shapes how traffic flows and where failures propagate.

**Star topology** connects every device to a central switch or hub. It's reliable and simple to extend, since adding a device just means plugging it into the central point, but it introduces a single point of failure: if the central device fails, the entire segment goes down with it.

**Bus topology** connects all devices along one shared backbone cable. It's inexpensive and simple to deploy, but all devices compete for the same bandwidth, so performance degrades as more devices join, and a single break in the cable takes the whole segment offline.

**Ring topology** connects devices in a closed loop, with data traveling in a single direction around the ring. It requires less cabling and makes fault detection more straightforward, but every packet has to traverse every device on the ring to reach its destination, and a single broken link disrupts the entire loop.

## Switch vs Router

A switch and a router solve fundamentally different problems. A switch connects multiple devices that belong to the *same* network. It maintains awareness of which device is reachable through which physical port, and forwards traffic only to that port rather than broadcasting to every connected device.

A router, by contrast, connects *separate* networks and moves traffic between them. It operates using IP addressing and routing logic to determine the best path for data to reach a different network — this is the device that sits at the boundary between a local network and the wider internet.

Understanding this distinction shapes how you interpret network traffic: intra-network communication is switch territory, while communication crossing network boundaries is router territory.

## Switch vs Hub

A hub is an older, unintelligent device. When a packet arrives, it forwards that packet to every device connected to it, regardless of the intended recipient, forcing each device to inspect it and discard it if it wasn't the target. This creates unnecessary traffic and congestion across the network.

A switch avoids this by learning. It builds and continuously updates a MAC address table, recording which device is reachable through which port. Once it has learned these mappings, it forwards each frame only to the port where the destination device actually resides, rather than flooding the entire network.

## VLANs

A VLAN (Virtual Local Area Network) allows devices to be logically separated from one another even when they are physically connected to the same switch. This segmentation is achieved purely through configuration, without any additional hardware.

Devices assigned to different VLANs on the same switch can each retain access to shared resources such as the internet, while remaining unable to communicate directly with devices in other VLANs — the switch enforces this separation according to configured rules, which is a common way organizations isolate departments or systems from one another for security purposes without the cost of separate physical infrastructure.

## Router, Switch, and VLAN Together

A router operates at Layer 3 of the OSI model and typically exposes a configuration interface through which an administrator sets rules such as port forwarding or firewall policies. Routing itself is a process, carried out with the help of routing protocols such as OSPF or RIP, which determine the optimal path for data between networks based on factors like hop count, path reliability, and the speed of the underlying medium.

A switch operates by forwarding Ethernet frames — encapsulated IP packets — based on MAC addresses. There is an important distinction between switch types: a Layer 2 switch forwards purely by MAC address and cannot route between separate IP networks, while a Layer 3 switch can also forward based on IP addressing and handle multiple networks simultaneously, effectively absorbing part of a router's function.

## Practical Example — Viewing the Local MAC Address Table

On a Linux system, the ARP/neighbor table shows the MAC-to-IP mappings the machine has already learned for devices on its local network segment:

```bash
$ ip neigh show
192.168.1.1     dev eth0 lladdr aa:bb:cc:11:22:33 REACHABLE
192.168.1.15    dev eth0 lladdr aa:bb:cc:44:55:66 STALE
192.168.1.254   dev eth0 lladdr aa:bb:cc:77:88:99 REACHABLE
```

`REACHABLE` means the entry was recently confirmed; `STALE` means it hasn't been re-verified recently but is still cached. Reviewing this table is a quick first step when investigating unfamiliar devices on a local segment — an unrecognized MAC address showing up here means a new device joined the network.
