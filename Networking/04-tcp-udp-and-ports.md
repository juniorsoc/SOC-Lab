# TCP, UDP, and Network Ports

## TCP — Transmission Control Protocol

TCP is defined by the fact that it establishes a connection before any data is transmitted, and this upfront negotiation is precisely what allows it to guarantee reliable delivery. It ensures that data arrives in full, in the correct order, and verifies that it hasn't been corrupted along the way. These guarantees come at a cost: if any single segment is lost, the affected data often needs to be retransmitted, and the overhead of these checks makes TCP inherently slower than protocols without such guarantees.

Each TCP segment carries several important fields. The source and destination ports identify, respectively, the sending device's outbound channel and the receiving device's listening service. Sequence and acknowledgment numbers allow data to be reassembled in the correct order even if segments arrive out of sequence, with the acknowledgment number essentially confirming receipt and indicating readiness for the next segment. A checksum verifies data integrity, and flag fields indicate how a given segment should be handled by the receiving device.

TCP establishes a connection through a three-way handshake: the client sends a SYN segment proposing a starting sequence number, the server responds with a SYN/ACK segment acknowledging this and proposing its own starting sequence number, and the client confirms with a final ACK, after which data transfer begins. Each side tracks its own sequence numbers independently, incrementing from wherever it started, which is what allows the receiver to reconstruct the original order of transmission regardless of the order segments actually arrived in.

Closing a TCP connection follows a comparable multi-step exchange: one side signals it has finished sending data with a FIN segment, the other acknowledges and sends its own FIN once it too is finished, and a final acknowledgment closes the connection completely. An RST segment, by contrast, represents an abrupt termination — used when something has gone seriously wrong, such as an error condition or unavailable resource, rather than a graceful close.

## UDP — User Datagram Protocol

UDP represents the other major transport-layer protocol, distinguished by the fact that it establishes no connection before sending data — it simply transmits and moves on, with no built-in mechanism to confirm that anything arrived. This lack of overhead makes UDP substantially faster than TCP and better suited to situations where the application itself needs full control over the pace of transmission, without the constraints of a persistent connection.

The trade-off is a complete absence of delivery guarantees: UDP does not verify that data arrived, and an unstable connection can severely degrade the quality of whatever is being transmitted, since there's no retransmission mechanism to fall back on. This makes UDP the preferred choice for applications where speed and low latency matter more than perfect accuracy — occasional gaps or losses are far less disruptive than the added delay of guaranteed delivery would be.

A UDP datagram carries a comparable but reduced set of headers relative to TCP — source and destination IP addresses, source and destination ports, a time-to-live counter, and the payload itself — but without any of the sequencing, acknowledgment, or handshake mechanisms that define TCP. Because there's no handshake at all, data begins flowing immediately, with essentially zero connection-establishment overhead, which is exactly what makes UDP well suited to real-time applications.

## Network Ports

A port is a numerical value between 0 and 65535 that identifies a specific application or service on a device, allowing a single device to run many different network services simultaneously, each reachable through its own distinct port. Ports in the range 0 through 1024 are reserved as well-known ports, allocated to the most common and widely used protocols and services.

Services can technically be configured to run on non-standard ports rather than their default, but doing so means clients must explicitly specify that port when connecting, since automatic discovery assumes the standard port is in use. Services found running on unusual or non-standard ports are worth additional scrutiny, since this is sometimes used as a simple technique to evade automated scanning tools that only check well-known ports by default.

## Practical Example — Checking Open Ports and Active Connections

```bash
$ sudo nmap -sV 192.168.1.10
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.9p1
80/tcp   open  http    nginx 1.18.0
443/tcp  open  https   nginx 1.18.0
3389/tcp open  ms-wbt-server  ← unexpected on a Linux web server

$ netstat -antp | grep ESTABLISHED
tcp   0   0 192.168.1.10:443   203.0.113.44:51322   ESTABLISHED  1421/nginx
```

The `nmap` scan reveals which services are actually listening and their versions — outdated versions here are a starting point for checking against known CVEs. Port 3389 (RDP) appearing on what should be a Linux web server is exactly the kind of anomaly worth flagging immediately. The `netstat` output shows a currently active connection, useful for confirming who is actively talking to a server right now.
