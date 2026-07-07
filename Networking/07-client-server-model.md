# The Client-Server Model

The client-server model describes the fundamental relationship underlying most network communication: a client always initiates a request, and a server responds to it — the direction of initiation never reverses under normal circumstances.

Several elements work together within this model. A protocol is the shared set of communication rules that both the client and server agree to follow, defining what commands are understood, how a request must be structured, and what a valid response looks like. A port identifies the specific service being requested on the server, since a single server is often capable of running multiple distinct services simultaneously, each listening on its own port. DNS plays a supporting role by translating a human-readable domain name into the numerical IP address the client actually needs to establish a connection. The IP address itself functions as the server's unique network address, identifying exactly where a request should be sent.

Because a connection is always initiated by the client, this directionality carries diagnostic significance: a server that unexpectedly initiates an outbound connection on its own, rather than merely responding to inbound requests, deviates from the expected pattern and often warrants closer investigation.

## Practical Example — Spotting an Unexpected Outbound Connection

```bash
$ sudo netstat -antp | grep ESTABLISHED
tcp  0  0  10.0.0.5:443     51.15.22.9:80        ESTABLISHED  8823/nginx
tcp  0  0  10.0.0.5:47812   185.220.101.4:4444   ESTABLISHED  2291/(unknown)
```

The first line is normal — a client connected inbound to the web server on port 443. The second line is the anomaly: the server itself is the source of an outbound connection to an external IP on port 4444, a commonly abused port for reverse shells. Combined with the unidentified process name, this is exactly the kind of client-server role reversal worth escalating for investigation.
