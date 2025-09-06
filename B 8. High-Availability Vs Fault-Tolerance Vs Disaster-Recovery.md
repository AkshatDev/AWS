---
tags:
  - basics
---

### High Availability

High Availability (HA) refers to a system's ability to **remain operational and accessible without significant downtime**. It's about reducing downtime and ensuring that the system can continue to operate, typically by switching to a redundant system or component in case of failure. The focus is on **minimizing interruptions and ensuring continuous operation**, which may involve automatic failover mechanisms. It should not be solely about how fast services can be resumed but also about the system's ability to operate continuously without significant **downtime**.

### Fault Tolerance

Fault Tolerance (FT) describes a system's ability to **continue functioning correctly even when part of it fails**. This usually involves redundancy in system components, such as having multiple servers running simultaneously so that if one fails, others can instantly take over without any service interruption. Fault-tolerant systems are designed to handle failures transparently to the end-users. They are **typically more expensive than high availability solutions** because they require additional hardware and more complex software architectures.

### Disaster Recovery

Disaster Recovery (DR) involves the plans and processes that are followed to recover from a catastrophic failure of a system, such as a natural disaster, significant hardware failure, or a cyber-attack. This encompasses the strategies and measures that enable the restoration of critical data and systems after a disaster. DR is broader and includes not just the technology to restore operations but also the policies and procedures that organizations follow to resume normal operations.

What is the difference between High Availability and Fault Tolerance?
?
A high availability system has to remain operational and accessible without significant downtime (minimizing interruptions and ensuring continuous operation ).
While a more fault tolerant system has to continue functioning correctly even when part of it fails.
<!--SR:!2024-09-27,42,250-->