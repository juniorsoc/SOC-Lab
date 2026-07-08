# Cloud Computing — What a SOC Analyst Needs to Know

## Service models

| Model | What the provider gives you | What you manage |
|-------|------------------------------|------------------|
| IaaS | Raw compute, storage, networking | Everything on top (OS, apps, config) |
| PaaS | Ready-to-use environment | Just your application |
| SaaS | Fully built application (browser access) | Nothing — provider handles it all |

## Why it matters for a SOC

Cloud environments have their own logging ecosystem, different from on-prem. Each provider (AWS, Azure, GCP) has its own native logging service, its own log format, and covers different events than an on-prem system would.

As orgs mix on-prem + cloud, knowing that these logs exist, roughly what they capture, and that they need separate analysis is a core SOC skill — even before learning any one provider's tooling in depth.
