---
tags:
  - basics
---

![[AWS_network_architecture.png]]

## Public vs Private


**Public**
1. These services are accessed using public endpoints only, eg s3.
**Private** 
1. A private AWS services is something that works inside a [[VPC]], only things connected to that VPC can access those services.
2. You can attach a Gateway to a VPC for some service in the VPC to be able to access AWS public Zone.
3. **No AWS PRIVATE ZONE CAN ACCESS PUBLIC INTERNET ZONE DIRECTLY**, the communication happens through AWS PUBLIC ZONE.

Can AWS private zone services connect directly with the public internet.
?
No, all the services have to use AWS Public Zone Endpoints.
<!--SR:!2024-09-21,36,230-->

## AWS Global Infrastructure

### **AWS Region**

1. A region in context of AWS does not map onto a continent or a country. It is a creation of AWS, inside this region is full deployment of AWS infrastructure.
**PROS**
1. Geographical Separation - Isolated Fault Domain.
	1. If a fault occurs in one region, it will not affect other regions.
2.  Geopolitical Separation - Different governance. 
	1. Depending on the region, you will be affected by the laws and regulation of that country.
	2. If you store data in one region, then unless you configure it, it won't leave that region.
3. Location Control - You can pick a region as close to your customers to have maximum data transfer speed and availability.
We can refer to a region using REGION CODE or REGION NAME, typically CLIs and APIs use REGION CODE.
Console UI uses REGION NAME

### AZs

Lower lever Architecture Zones. Inside **regions** AWS provides multiple availability zones.
These zones are isolated inside zones.
If one availability zone inside a Region fails, all the other zones are not affected by it.

### **AWS Edge Locations**

1. AWS cannot create more AWS Regions faster because it takes a lot of resources and the county's political permissions, for this reason they have AWS Edge Locations.
2. AWS Edge Locations are smaller than AWS Regions and the provide content distribution services. 
3. These are important for companies like NETFLIX, they want to store their data as close as possible to their consumers for fast services. So, Netflix could use a Region in a country but use a different edge location closer to the consumers in different cities.
### **Global services**

Some services are not dependent on regions, eg IAM or Route53.
### Service Resilience
1. Global resilient services
	1.  A service that operates globally with a single database, it's one product and it's data is replicated inside multiple regions. This means that any region could fail but it wont affect a global service. It would take the world to fail for a globally resilient service to face outage, eg IAM
2. Region Resilient services
	1.  Services operating inside a single region with one set of data per region. They generally replicate data to different AZs in that region. So, if the whole region fails then the service will fail.
3. AZ resilient services
	1. These services are run for a single availability zone. Generally AZ resilient services are very prone to fail.