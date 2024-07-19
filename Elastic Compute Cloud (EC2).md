---
tags:
  - basics
cssclasses:
  - bold-blue
---

## Key Facts & Features
1. Infrastructure as a service (IAAS) - Provides Virtual Machines, also known as **instances**. Instance is just an OS configured with a certain set of resources.
2. EC2 is a **private AWS service**. It uses VPC networking, by detault EC2 runs in the private AWS zone.
3. It is configured to launch in a single VPC subnet. If you want any public access you have to configure it and the VPC it is running inside should support public access.
4. While EC2 instances themselves are not inherently resilient across Availability Zones (AZs), you can architect applications to be resilient by distributing instances across multiple AZs. If an AZ fails, only the instances within that AZ are impacted.
5. Before launching , you can choose various sizes and capabilities for that instance.
6. **On-Demand billing. Per Second**. You pay for the resource you use.
7. Two popular types of storage - Local on-host storage or Elastic Block Store (EBS).

EC3 is an ==Infrastructure as a service (IAAS)==.
<!--SR:!2024-07-10,7,210-->

What is an instance in context of EC2::An OS with resources configured.
<!--SR:!2024-07-13,10,230-->
## Instance Lifecycle

Every EC2 instance has a state attribute. It provides indication of its condition.
Most **common states are Running, Stopped, Terminated**, there are more types but these are the most common.

You can change the state of an instance from running to stopped or vice vera, these actions are reversible.
Terminated on the other hand is irreversible. The instance will be fully deleted.

1. When an instance is running you are charged for CPU, memory, storage and networking.
2. When an instance is stopped you will not be charged for CPU, memory or networking but you will be charged for storage that is allocated to you.
3. Only when an instance is terminated, you will not be charged for these resources.

When you have an active instance running, what are you usually charged for?::CPU, Memory, Networking, Storage.
<!--SR:!2024-07-14,11,226-->

When an instance is stopped, what are you charged for?::Storage.
<!--SR:!2024-07-15,12,246-->
## Amazon machine image (AMI)

An AMI can be created from an EC2 instance or an EC2 instance could be created from an AMI.

### Permissions
An AMI contains attached permissions, these permissions control who can and cannot use the AMI. 
An AMI could be public, this is what AWS provides.
An AMI could have Implicit access permissions provisioned by the owner.
An AMI could also have explicit permissions, where specific AWS accounts are allowed access.

### Root Volume
It is like the root volume in Linux, it is the drive that boots the OS, it could also have other volumes but it always has a root volumn.

It is mandatory to provied a ==root volumne== to an Amazon Machine Image (AMI).
<!--SR:!2024-07-13,10,244-->

### Block Device Mapping
It links all the volumes that an AMI has and how they are presented to the OS.

What is block device mapping::The links to all the volumes an AMI has and how they are presented to the OS.
<!--SR:!2024-07-05,2,184-->