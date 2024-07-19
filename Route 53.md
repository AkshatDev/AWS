---
tags:
  - basics
---

## Basics of AWS Route 53

1. **Register Domains**: Route 53 allows you to register domain names directly through AWS. This integrates with AWS’s ecosystem, simplifying management and configuration.
    
2. **Host Zone Files on Managed Nameservice**: Route 53 manages DNS records and zone files for the domains. It acts as a highly available and scalable DNS service.
    
3. **Global Service**: Route 53 is a global service. Unlike many AWS services that require you to select a region, Route 53 does not have this requirement because it operates at the Internet domain name system level.
    
4. **Globally Resilient**: The service is designed for high availability and fault tolerance. It replicates DNS data across multiple geographically dispersed servers to ensure resilience and reduce the risk of downtime.
    
5. **Scalability and Resilience**: Route 53 is built to handle large volumes of DNS queries without degradation in performance, ensuring that it continues operating smoothly even during failures or high traffic periods.

What is the main use of Route53?::Hosting Domains
<!--SR:!2024-07-28,25,250-->

## Manage Domains

![[route53_registerzones.png]]

- **Relationship with Domain Registries**: AWS maintains relationships with various domain registrars and registries (like Public Interest Registry for `.org` domains) to manage the registration and availability checks for domain names.
    
- **Zone Files and Name Servers**: When you register a domain with Route 53, it automatically creates a DNS zone file for that domain. AWS also assigns a set of name servers (typically four) to this zone file. These servers are distributed globally to ensure DNS queries are answered quickly and reliably, regardless of where they originate.

- Route 53 checks with PIR if that domain is available.
- Then route53 creates a zone file for the domain being registered. A domain file is just a database that contains all the DNS information for a particular domain.
- Rout53 also allocates nameservice for this zone, these are the services route53 creates and manages that are distributed globally, there are generally 4 of these services for an individual zone.
- Then the zone file created by AWS gets put in these 4 managed nameservices.

## Zones inside route53
**Hosted Zones**: In Route 53, a hosted zone acts as a container for DNS settings and records for a domain. You can create and manage DNS records within these hosted zones. AWS differentiates between two types of hosted zones:

- **Public Hosted Zones**: These are accessible over the internet. They allow you to manage the DNS records for a domain that is accessible from anywhere on the internet.
- **Private Hosted Zones**: These are used within Amazon VPCs and are accessible only within the VPCs they are associated with. This allows for internal domain name resolution, which is not accessible from the public internet.