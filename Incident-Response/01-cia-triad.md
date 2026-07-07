# The CIA Triad — What We Protect in Cybersecurity

Foundational framework for cybersecurity: confidentiality, integrity, availability. Almost every incident is a violation of one or more of these — reviewing an incident against this triad is usually the first analytical step.

| Property | Ensures | Violation = | Defenses | Investigation question |
|----------|---------|-------------|----------|--------------------------|
| Confidentiality | Only authorized people access data/systems | Data breach | Encryption (in transit + at rest), MFA, access controls | Was data accessed/exposed without authorization? |
| Integrity | Data can't be modified without authorization | Tampering | Hashing, digital signatures, audit logging | Was data modified by someone without authorization? |
| Availability | Data/services accessible when needed | Outage (DoS, ransomware) | Load balancing, backups, CDNs, rate limiting | Was uptime affected, and why? |

These three questions — was data exposed, was data changed, was a service unavailable — are the mental checklist for reasoning about any incident.
