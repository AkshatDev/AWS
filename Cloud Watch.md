---
tags:
  - basics
---
![[cloudwatch.png]]
## Basics

- Collects and manages operational data on your behalf.
- This is a product that allows collection, monitoring and actions based on metrics. eg CPU utilization of EC2 instances, disk space usage etc.
- It is a public service.
- Metrics
	- Some metrics are generated within the AWS and handled by the AWS , ex CPU utilization, to collect metrics outside the AWS, we need the **Cloud Watch agent**. This agent is also used for services running inside an AWS service  example CPU processes going on.
- Cloud Watch Logs
	- This allows collection, monitoring, actions based on monitoring **logging data**.
	- Could be Linux logs, Server Logs etc.
- Cloud Watch Events
	- It provides 2 very important features
	1. Generate events when something happens, for eg, if an EC2 instance is terminated then it can perform some events.
	2. It can perform events during specific times for eg day, month , day of week etc.

What are metrics?::Data related to AWS products, applications or on premises systems.
<!--SR:!2024-07-20,17,250-->


## Namespace for metrics 
All namespace styles are fair game for your own services, having said that there are AWS services that have reserved namespace styles and you cannot use them. For those services this is the format **AWS/service**. for eg AWS/EC2. 

## Alarms 
It has 2 states, 'ok' and 'alarm' state. Alarms can be set according to different metric thresholds and an Alarm can do different things depending on what the user wants, for example if the CPU usage of an EC2 instance goes more than 50% we can have an email sent to us.

# CloudWatch Logs

-  These are a public services and could be accessed via the **AWS public zone**.
- Store, Monitor and Access logging data.
- AWS Integrations - EC2, VPC Flow Logs, Lambda, CloudTrail, R53 and more.
- Capable of performing actions based on the logging data - metric filter.
- 