# The CIA Triad

- **Confidentiality** — data accessible only to authorized people. Violation = data breach. Defenses: encryption, MFA, access control.
- **Integrity** — data can't be modified without authorization. Violation = tampering. Defenses: hashing (SHA-256), digital signatures, audit logs.
- **Availability** — data/services accessible when needed. Violation = outage (DoS/DDoS/ransomware). Defenses: load balancers, backups, CDN, rate limiting.

**Every incident maps to one of these three questions:** Did data leak? Was data changed? Was a service unavailable?
