# Intrusion Detection Systems (IDS)

An intrusion detection system continuously monitors a network or an individual host for signs of unauthorized activity, comparing observed behavior against known patterns of malicious activity or unexpected deviations from a system's normal baseline. This typically includes detecting the presence of a device on the network that hasn't been authorized to connect, as well as identifying attempts by a user to access or modify a file they shouldn't have permission to touch.

An IDS is fundamentally a detection mechanism rather than a preventive one — it identifies and alerts on suspicious activity, but unlike a firewall, it doesn't inherently block that activity from occurring. This distinction is important during an investigation, since an IDS alert indicates that something was observed and flagged, not necessarily that it was stopped.

## Practical Example — Reading a Snort Alert

```
$ sudo snort -A console -q -c /etc/snort/snort.conf -i eth0

07/07-14:22:09.442  [**] [1:2001219:20] ET SCAN Nmap Scripting Engine User-Agent
Detected [**] [Classification: Detection of a Network Scan]
{TCP} 203.0.113.44:51122 -> 10.0.0.5:80

07/07-14:22:11.108  [**] [1:2003068:11] ET POLICY curl User-Agent Outbound
[**] [Classification: Attempted Information Leak]
{TCP} 10.0.0.5:47812 -> 185.220.101.4:443
```

The first alert flags a scanning tool's signature hitting a web server on port 80 — reconnaissance activity worth logging and watching. The second flags something more concerning: an *outbound* connection from the internal server itself, using a scripted client rather than a browser, toward an external IP — worth cross-referencing against the client-server model expectations discussed elsewhere in these notes.
