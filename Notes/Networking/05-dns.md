# DNS — Domain Name System

## Record types

| Record | Maps to |
|--------|---------|
| A | Domain → IPv4 |
| AAAA | Domain → IPv6 |
| CNAME | Domain → another domain (alias) |
| MX | Mail server responsible for the domain |
| TXT | Verification / anti-spam (SPF, DKIM) |

## Resolution flow

1. Check local cache — if cached, done.
2. Ask ISP resolver — if cached there, done.
3. Ask a root DNS server — points to the right TLD server.
4. TLD server points to the authoritative server for that domain.
5. Authoritative server returns the real record — cached by resolvers along the way per the record's TTL.

**Recursive resolver** = does the lookup work on your behalf. **Authoritative server** = actual source of truth for the domain's records.
