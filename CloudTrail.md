---
tags:
  - basics
---

![[cloudtrail.png]]

- This AWS service logs API actions that affect AWS accounts.
- By default stores last 90 days in Event History. This is enabled by default and no cost for 90 day history.
-  To customise the service, one or more trails must be created.
- There are 3 types of events, **management**, **data**, **insight** events.
- CloudTrail is not real time and hence cannot be used to real time logging.

## Management Events
They are also known as control plane operations like creating EC2, creating a VPC

## Data Events
Operations performed on or in a resource, for example adding objects to an EC2.
By **default CloudTrail does not log Data Events** because they are extremely high in volume.



A **CloudTrail trail** is a unit of configuration in AWS. It is a way you provide configuration to CloudTrail on how to operate.

A **trail logs events for the AWS region that it's created in** because CloudTrail is a regional service.

## One Region Trail
These trails can only log events that happen in the region the trails are.

## All region Trail

These trails can log global events as well for example IAM, CloudFront etc. The global events are called global service events and a trail needs to have this enable to be able to log these. By default it is always enabled.  

## Organisational Trails

If you create a trail from the management account for an org, it can store all the info for all the accounts inside that org. It gives a single endpoint API and is very powerful in managing big orgs.

### Additional Points

- **Event History**: By default, CloudTrail logs the last 90 days of management events in the Event History, which you can view from the CloudTrail console. This service is provided without additional cost.
    
- **Custom Trails**: To retain activity logs beyond 90 days or to log data events, you need to create a custom trail and specify an S3 bucket for storage. Custom trails can also integrate with CloudWatch Logs and S3 lifecycle policies for extended retention and management.
    
- **Real-Time Capabilities**: While CloudTrail is near real-time, it is not suited for real-time monitoring. There can be a slight delay between when an event occurs and when it appears in the log.


What are the default and cost-free logging capabilities of AWS CloudTrail?:: CloudTrail logs the last 90 days of management events in the Event History by default, at no additional cost.

What are management events in AWS CloudTrail?:: Management events in CloudTrail are operations performed on AWS resources, such as creating, deleting, and modifying EC2 instances or other AWS services.
<!--SR:!2024-08-17,1,230-->

Why are data events not logged by default in AWS CloudTrail?:: Data events are not logged by default due to their high volume and potential cost implications.

What is the purpose of an all-region trail in AWS CloudTrail?:: An all-region trail logs events from all regions in the AWS account, including global service events, providing comprehensive monitoring across an entire AWS environment.
<!--SR:!2024-08-17,1,230-->

What are the benefits of creating an organizational trail in AWS CloudTrail?:: Organizational trails, when created in a management account, can log events for all accounts in an AWS Organization, offering a centralized view and simplified management of logs across multiple accounts.

How does AWS CloudTrail handle real-time monitoring?:: While CloudTrail provides near real-time logging, it is not suited for real-time monitoring due to slight delays between when an event occurs and when it appears in the log.
<!--SR:!2024-08-17,1,230-->
