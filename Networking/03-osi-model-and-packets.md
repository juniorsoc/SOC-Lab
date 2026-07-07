# The OSI Model, Packets, and Frames

## The OSI Model

The OSI (Open Systems Interconnection) model is the reference framework describing how network devices send, receive, and interpret data, allowing equipment from different manufacturers to interoperate through a shared, layered structure.

When data is transmitted, it moves downward through the layers, from Layer 7 to Layer 1, with each layer adding its own header — a process called encapsulation. When data is received, this process runs in reverse, with each layer stripping away its corresponding header as the data moves back up through the stack, known as decapsulation.

The seven layers, from top to bottom, are: Application, Presentation, Session, Transport, Network, Data Link, and Physical.

The **Application layer** provides the interface through which everyday programs — browsers, email clients — interact with network data, using protocols such as HTTP, HTTPS, DNS, and FTP. Attacks at this layer tend to target the application logic itself, including cross-site scripting and SQL injection.

The **Presentation layer** handles translation between data formats and manages encryption and compression, using protocols like TLS/SSL. Relevant security concerns here include certificate validity and downgrade attacks against encryption.

The **Session layer** creates, maintains, and terminates communication sessions between two systems, relying on protocols such as NetBIOS, RPC, and SMB sessions. Session hijacking is the primary threat associated with this layer.

The **Transport layer** determines how data moves between devices and with what reliability guarantee, primarily through TCP or UDP. This layer is a common target for port scanning and denial-of-service activity.

The **Network layer** is responsible for routing packets between networks using IP addressing, choosing the most efficient available path with the help of routing protocols such as OSPF and RIP. Threats at this layer include IP spoofing and manipulation of packet TTL values.

The **Data Link layer** handles physical addressing, attaching MAC addresses to outgoing data. Every network interface card has a MAC address burned in by its manufacturer, though this value can be spoofed. This layer is associated with ARP spoofing, MAC flooding, and Man-in-the-Middle attacks.

The **Physical layer** covers the actual transmission of raw bits across a physical medium — cabling, wireless signals, and the hardware that carries them. Threats here are generally physical in nature, such as unauthorized physical access or cable tapping.

A useful generalization: attacks against the lower layers (1 through 4) tend to be network-level in nature, while attacks against the upper layers (5 through 7) tend to be application-level.

### Layer 4: TCP and UDP

TCP guarantees delivery, checks for transmission errors, and preserves the correct ordering of data, at the cost of additional overhead and reduced speed. UDP offers no such guarantees — data may simply fail to arrive — but is considerably faster, since it carries none of TCP's connection-management overhead. TCP is generally used where reliability matters, such as web browsing, email, and file transfer, while UDP is favored where speed is prioritized over perfect accuracy, such as streaming and real-time communication.

### Layer 3: How Routing Works

Data is broken into packets, each tagged with the destination's IP address. A router examines that address and selects the appropriate path forward, taking into account the number of intermediate hops, the reliability of each candidate path, and the relative speed of the transmission medium involved. This path-selection logic is governed by routing protocols rather than being decided arbitrarily by the router itself.

## Packets and Frames

Packets and frames are the discrete units into which larger messages are broken down for transmission across a network, later reassembled at their destination.

A packet operates at Layer 3 and contains the sender's and receiver's IP addresses along with the actual data payload being transmitted. A frame operates at Layer 2 and wraps around a packet, adding the MAC addresses needed to move that packet across the local network segment. As a general rule, discussions involving IP addresses concern packets, while discussions involving MAC addresses concern frames.

Data is deliberately split into smaller units rather than transmitted as a single whole, primarily to reduce the risk of any single large transfer overwhelming network capacity, and to allow data to be rerouted or retransmitted in smaller, more manageable pieces if something goes wrong along the way.

Several header fields within an IP packet carry particular significance. The Time to Live field acts as an expiration counter, ensuring that a packet which fails to reach its destination within a reasonable number of hops is discarded rather than circulating indefinitely. The checksum field allows the receiving system to verify that the data wasn't corrupted in transit. The source and destination address fields identify, respectively, where the packet originated and where it is headed, which is what allows a response to be routed back correctly.
