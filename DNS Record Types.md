---
tags:
  - basics
---
## Nameserver Records

- These are the record types that allow delegation to occur in DNS.
- For example for ',com, these nameservers point to servers managed by amazon.com, these are handled by amazon.

## A/AAAA Records

- These type of records map hostnames to IP addresses.
- A record type maps host to ipv4
- AAAA type record maps host to ipv6
-  As a solutions architect, you will generally create records with the same name.
## CNAME Records

- Canonical name record type lets you create DNS SHORTCUTS, HOST TO HOST RECORDS.
- Eg, we have 'A' record that maps to an IPv4, let's say that this server does ftp, mail and www. Cname here reduces ADMIN overhead by doing this automatically 

- CNAMES cannot point directly at IP addresses, only at names.
Can CNAMES point to an IPv4 address::False, they can only point to a nameserver.
<!--SR:!2024-07-05,2,190-->

## MX Records

- Mainly used for email.
- MX Records have 2 main parts, **priority** and **value**.
- The value could just be a host (assumed to be a part of the same zone it is in).
- If there is a dot on the right, it means it is a fully qualified domain name.
- It does an MX query using DNS on the domain and retrieves records.
- These record values have priority values and the smaller number means higher priority.
## TXT Records

These record types allow you to add arbitrary text to domain to prove ownership.
One common usage, let's say you want to add your domain to google to host your email, google might ask you to add some data to the email. Once your administrator does it, google would then query that text data and if it matches, it proves the ownership.

## TTL (Time To Live)
It is a numberic value (in seconds) that can be sent on DNS records.
