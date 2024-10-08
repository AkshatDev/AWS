---
tags:
  - basics
---

## Virtual Private Cloud

A service used to create private services inside AWS that other private services will run from. This service is also used to connect AWS private networks to on-premises networks.
It also lets you connect to other cloud networks.

## VPC Basics

1. It is a Virtual Network inside AWS.
2. A default VPC is within 1 account & 1 region.
3. They oprate withing multiple AZ inside a region.
4. Private and Isolate by default, unless you decide otherwise. All VPCs are isolated from each other and the public AWS zone and public internet.
5. Two types - Default VPC and Custom VPCs.

### Default VPC
1. Can have **only one** of these within a region, this means in theory a region could have 0 default VPC, some services assume that there is a Default VPC present that is why it is recommended to keep default VPC in the region active.
2. Managed by AWS, all networking is handled on your behalf by AWS and hence are lot less flexible than custom VPCs
3. A region can have only 1 VPC but multiple custom VPCs.
4. Every VPC is allocated a range of IP addresses called VPC CIDR that determines the range of IP addresses a VPC can use.
5. The default VPC always gets only  1 CIDR range, 172.31.0.0/16.
6. Default VPC is sub-divided into subnets, each subnet in a VPC is located inside one AZ, it is the default during a creation and cannot be changed. A default VPC will always have one subnet in each AZ iniside that region.
7. Each subnet inside an AZ can use part of the VPC's CIDR, these cannot be the same as the other subnets in the VPC, they cannot overlap with any other subnets in the VPC.
8. The IP ranges given to each subnet in the VPC have a start, eg - 172.31.0.0, and an end , ed - 172.31.15.255. Any private services inside that subnet can use these.
9. Default VPCs can be removed & recreated from an AWS account.
10. Inside a Default VPC, a /20 subnet is created in each AZ in that region. Higher the /number, smaller the network. For eg, /17 os half the size of /16.
11. 16 /20 subents can fit into one /16 that the VPC uses.
12. By default you are provided with Internet Gateway (IGW), Security Group (SG) & NACL.
13. By default anything placed in the default VPC subnets is assigned a public ipv4 address.
What determines the IP range for the default VPC::VPC CIDR
<!--SR:!2024-10-14,59,250-->
The Default VPC subnets are assigned a public IPv4, True or False::True
<!--SR:!2024-09-29,44,250-->

### Custom VPC

1. Can have as many custom VPCs.
2. Have to configure everything by yourself end to end and are by default 100% private.
3. Can configure them to communicate with other VPCs and even other cloud platforms and on premises network.

