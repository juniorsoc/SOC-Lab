# IP and MAC Addressing, ARP, DHCP, and Subnetting

## Public vs Private IP Addresses

Every device on a network requires an address to be identified and reachable. A public IP address identifies a device on the internet and is globally routable, typically assigned by an internet service provider. A private IP address identifies a device only within a local network and is not routable on the public internet — it exists purely for internal communication behind a router performing network address translation.

## MAC Addresses

A MAC address is a unique hardware identifier assigned to a device's network interface card. It operates at Layer 2 of the OSI model and is used to identify devices within a local network segment. The address is structured in two halves: the first half identifies the manufacturer of the network card, and the second half forms a unique identifier for that specific device.

## Ping and ICMP

Ping uses ICMP (Internet Control Message Protocol) packets to test connectivity between two devices and measure round-trip latency. It provides two pieces of information: whether a path to the target device currently exists, and how reliable and responsive that path is. It's typically the first diagnostic step taken before deeper investigation into a connectivity issue.

## ARP — Address Resolution Protocol

ARP maps an IP address to its corresponding MAC address within a local network. Every device maintains a local table of these mappings, known as the ARP cache, so that repeated lookups aren't necessary.

The resolution process happens in two steps. First, a device broadcasts an ARP request across the local network, essentially asking which device owns a particular IP address. The device that holds that IP address then responds directly with an ARP reply, providing its MAC address, which the requesting device stores in its ARP cache for future use.

Because ARP includes no built-in authentication, it's vulnerable to ARP spoofing (or poisoning), in which an attacker sends forged ARP replies to impersonate another device on the network — commonly the default gateway — in order to redirect traffic through themselves. This technique is foundational to many Man-in-the-Middle attacks and is a pattern worth recognizing when reviewing network activity.

## DHCP — Dynamic Host Configuration Protocol

IP addresses can be assigned manually (statically) or automatically through a DHCP server. The DHCP process follows a four-step exchange, commonly abbreviated as DORA: the client broadcasts a Discover message asking whether a DHCP server is present on the network; the server responds with an Offer, proposing a specific IP address; the client sends a Request, confirming it will accept that address; and the server finalizes the assignment with an Acknowledgment, after which the client can begin using the address.

## Subnetting

Subnetting is the practice of dividing one larger network into smaller, more manageable segments. Every subnet contains three key address types: a network address, which identifies the subnet as a whole rather than any individual device; a host address, which identifies a specific device within that subnet; and a default gateway, which is the router responsible for forwarding traffic to other networks.

Subnetting serves several purposes. It improves efficiency by reducing the volume of broadcast traffic confined within each smaller segment. It improves security by isolating networks from one another, limiting the blast radius of any compromise. And it improves administrative control by making it clearer which devices belong to which logical grouping.

## Practical Example — Checking Connectivity and the ARP Cache

```bash
$ ping -c 4 192.168.1.254
PING 192.168.1.254 (192.168.1.254) 56(84) bytes of data.
64 bytes from 192.168.1.254: icmp_seq=1 ttl=64 time=1.02 ms
64 bytes from 192.168.1.254: icmp_seq=2 ttl=64 time=0.98 ms
64 bytes from 192.168.1.254: icmp_seq=3 ttl=64 time=1.10 ms
64 bytes from 192.168.1.254: icmp_seq=4 ttl=64 time=1.01 ms

--- 192.168.1.254 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 0.980/1.027/1.100/0.045 ms

$ arp -a
gateway (192.168.1.254) at aa:bb:cc:77:88:99 [ether] on eth0
```

Zero packet loss and consistent round-trip times confirm a healthy path to the gateway. The `arp -a` output confirms which MAC address currently answers for that IP — if this value suddenly changes without explanation, it can indicate ARP spoofing in progress.
