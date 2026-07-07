# The Client-Server Model

Client always initiates a request, server responds. Direction never reverses under normal circumstances.

| Element | Role |
|---------|------|
| Protocol | Shared rules both sides follow |
| Port | Identifies which service on the server |
| DNS | Translates domain name → IP |
| IP address | Server's actual network address |

Since a connection is always client-initiated, a server that unexpectedly initiates an outbound connection on its own is a deviation from the expected pattern and worth investigating.
