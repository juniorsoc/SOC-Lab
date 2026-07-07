# Client-Server Model

The **client** initiates a request; the **server** responds — never the reverse. A **protocol** (HTTP, FTP, SSH) is the shared communication ruleset; a **port** is the door to a specific service (HTTP=80, HTTPS=443, SSH=22); **DNS** translates domain names to IP addresses.

**SOC relevance:** if a server suddenly initiates an outbound connection on its own, that's a strong signal of a reverse shell or C2 beaconing.
