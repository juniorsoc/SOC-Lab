# The CIA Triad — What We Protect in Cybersecurity

The CIA Triad provides the foundational framework underlying nearly all of cybersecurity practice, describing the three properties that security controls exist to protect: confidentiality, integrity, and availability. Nearly every security incident can be understood, at its core, as a violation of one or more of these three properties, which is why reviewing an incident against this framework is often the first analytical step a SOC analyst takes.

Confidentiality ensures that data and systems remain accessible only to those explicitly authorized to access them. A violation of confidentiality is what's commonly referred to as a data breach — information reaching parties who were never meant to see it. Defenses against confidentiality violations center on controlling and verifying access, including encryption of data both in transit and at rest, multi-factor authentication, and carefully scoped access controls. When investigating a potential confidentiality violation, the relevant question is whether data was accessed or exposed to someone without proper authorization, and logs are reviewed with that specific question in mind.

Integrity ensures that data cannot be modified without proper authorization, and without this guarantee, data essentially cannot be trusted at all, since there would be no way to know whether it reflects reality or has been tampered with. A violation of integrity constitutes tampering — an unauthorized change to data that should have remained untouched. Defenses here center on detecting and preventing unauthorized modification, including cryptographic hashing to verify that data hasn't changed, digital signatures to confirm authenticity, and audit logging to record every legitimate change for later review. Investigating a potential integrity violation centers on identifying whether data was modified by someone or something without proper authorization to do so.

Availability ensures that data and services remain accessible to authorized users precisely when they need them, and even brief periods of unavailability can carry serious financial and operational consequences depending on what's affected. A violation of availability manifests as an outage, whether caused deliberately through a denial-of-service attack or as a side effect of something like ransomware rendering systems unusable. Defenses against availability violations include load balancing to distribute demand, regular backups to allow recovery, content delivery networks to absorb traffic surges, and rate limiting to prevent any single source from overwhelming a system. Investigating a potential availability violation centers on monitoring uptime and identifying the cause of any disruption to normal service.

Taken together, these three questions — was data exposed, was data changed, was a service unavailable — form the mental checklist a SOC analyst applies to essentially every incident under review, providing a consistent structure for reasoning about what actually happened and how serious it is.

## Practical Example — Classifying an Incident Against the Triad

```bash
$ grep "203.0.113.44" access.log | grep "/export/customer_data" | wc -l
1

$ grep "203.0.113.44" access.log | tail -1
203.0.113.44 - - [07/Jul/2026:02:14:33] "GET /export/customer_data.csv HTTP/1.1" 200 8482291
```

A single successful (`200`) request pulling an 8MB customer data export, from an IP not associated with any known internal system, is a clear **confidentiality violation** — unauthorized data exfiltration — rather than an integrity or availability issue. Framing the finding this way in an incident report (*"This is a confidentiality breach, not a system outage"*) is exactly the kind of classification a triage write-up is expected to make explicit.
