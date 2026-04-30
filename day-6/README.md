# Amazon Route 53 — DNS Overview

## What is Route 53?

**Amazon Route 53** is a highly available, scalable, and fully managed **Domain Name System (DNS)** web service provided by AWS. The name "Route 53" refers to **TCP/UDP port 53**, the standard port used by DNS.

---

## Core DNS Functions

### 1. Domain Registration
Route 53 allows you to register domain names (e.g., `example.com`) directly through AWS, acting as a **domain registrar**.

### 2. DNS Resolution
It translates human-readable domain names into machine-readable **IP addresses** (e.g., `example.com` → `192.0.2.1`), enabling browsers and clients to locate servers on the internet.

### 3. Health Checking
Route 53 continuously monitors the health of your endpoints and can **automatically reroute traffic** away from unhealthy resources.

---

## Key DNS Record Types Supported

| Record Type | Purpose |
|-------------|---------|
| `A`         | Maps domain to an IPv4 address |
| `AAAA`      | Maps domain to an IPv6 address |
| `CNAME`     | Alias one domain to another |
| `MX`        | Mail exchange records |
| `TXT`       | Text records (SPF, domain verification) |
| `NS`        | Name server records |
| `SOA`       | Start of Authority record |
| `Alias`     | AWS-specific; maps to AWS resources like ELB, CloudFront, S3 |

> **Note:** The `Alias` record is unique to Route 53 and allows mapping to AWS resources without incurring extra DNS charges.

---

## Routing Policies

Route 53 supports multiple routing policies to control how DNS queries are answered:

- **Simple Routing** — Single resource, no health checks.
- **Weighted Routing** — Distribute traffic across multiple resources by percentage (useful for A/B testing).
- **Latency-Based Routing** — Routes users to the AWS region with the lowest latency.
- **Failover Routing** — Active-passive failover using health checks.
- **Geolocation Routing** — Routes based on the geographic location of the user.
- **Geoproximity Routing** — Routes based on resource location with optional bias.
- **Multivalue Answer Routing** — Returns multiple healthy IP addresses (basic load balancing).

---

## How DNS Resolution Works with Route 53

```
User Browser
     │
     ▼
Recursive Resolver (ISP)
     │
     ▼
Route 53 Name Servers  ←── Authoritative DNS for your domain
     │
     ▼
Returns IP Address
     │
     ▼
User connects to the Server
```

---

## Key Features

- **100% SLA availability** — Route 53 is designed for high availability with a financially backed SLA.
- **Global Anycast Network** — DNS queries are answered from the nearest edge location across 100+ Points of Presence (PoPs).
- **Private DNS** — Resolve domain names within an Amazon VPC without exposing records publicly.
- **DNSSEC** — Supports DNS Security Extensions for protection against spoofing and cache poisoning.
- **Traffic Flow** — Visual editor to build complex routing configurations.

---

## Common Use Cases

1. **Hosting a public website** — Register a domain and point it to an EC2 instance, S3 static site, or CloudFront distribution.
2. **Blue/Green deployments** — Use weighted routing to gradually shift traffic.
3. **Disaster recovery** — Failover routing to a standby environment.
4. **Internal service discovery** — Private hosted zones within a VPC.
5. **Multi-region architectures** — Latency-based routing to serve users from the nearest region.

---

## Pricing Highlights

- Charged per **hosted zone** per month.
- Charged per **million DNS queries** answered.
- Health checks are billed separately.
- No charge for queries to **Alias records** pointing to AWS resources.

---

## Summary

> Amazon Route 53 is more than just a DNS service — it's a **traffic management platform** that combines domain registration, DNS resolution, health monitoring, and intelligent routing policies to build resilient, globally distributed applications on AWS.
