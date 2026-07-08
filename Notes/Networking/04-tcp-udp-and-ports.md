# TCP, UDP, and Network Ports

## TCP

Connection-oriented — negotiates a connection before sending data, which is what lets it guarantee reliable, in-order, uncorrupted delivery. Trade-off: lost segments get retransmitted, and the overhead makes it slower than UDP.

Segment fields: source/destination port, sequence + acknowledgment numbers (reassembly in order), checksum (integrity), flags (how to handle the segment).

**Three-way handshake (opening):** SYN (client) → SYN/ACK (server) → ACK (client) → data transfer begins.

**Closing:** FIN → ACK + FIN (other side) → final ACK. An RST is an abrupt termination (error/unavailable resource), not a graceful close.

## UDP

Connectionless — sends and moves on, no confirmation of arrival. Faster than TCP, no delivery guarantees. Preferred where speed/low latency matters more than perfect accuracy (streaming, real-time).

Header: source/destination IP + port, TTL, payload — no sequencing/ACK/handshake.

## Ports

Number 0–65535 identifying a specific app/service on a device. 0–1024 = well-known ports (reserved for common services).

Services *can* run on non-standard ports — but then clients must specify the port explicitly. Unusual ports are worth extra scrutiny; can be used to dodge scanners that only check well-known ports.
