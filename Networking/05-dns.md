# DNS

**Record types:** A (IPv4), AAAA (IPv6), CNAME (alias), MX (mail server), TXT (verification/anti-spam).

**Resolution flow:** local cache → ISP resolver → root DNS server → TLD server → authoritative server returns the real IP (cached per its TTL).

**Recursive vs authoritative:** a recursive resolver does the legwork on your behalf; the authoritative server holds the actual source-of-truth records.
