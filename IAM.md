---
tags:
  - basics
---
Every AWS account comes with IAM, it also has its own database, it is secure across all AWS regions.

## 3 Types of identity objects

1. [[IAM Users|Users]] - 
	Identities that represent humans or applications that need access to your account.
2. [[IAM Groups|Group]] -
	Collection of related users e.g. development team, finance or HR.
3. Role - (Hard to understand)
	Can be used by AWS Services, or for granting external access to your account.

**How many and what identity objects are there in IAM**::3 types, User, Group, Role
<!--SR:!2024-08-30,14,190-->

Users VS Role

USERS ARE USED WHEN WE CAN IDENTIFY THE INDIVIDUAL THING THAT WILL LOG INTO THAT USER.number of things are uncertain, for ex, you want to allow 'x' number of EC2 instances access to certain services in your account.
## [[IAM Identity Policy]]
 IAM let's users to create policies which are objects or documents that can deny or allow access to AWS services **ONLY WHEN** they are attached to users, groups or roles.

## IAM JOBS

![[iam_jobs.png]]
1. Manage Identities.
2. Authenticate.
3. Authorize.

## More IAM properties.

1. No Cost.
2. Global Service.
3. Controls only it's own identities through IAM Policies.
4. **No direct control on external accounts or users.**
5. user MFA and Identity Federation.

## IAM Access Keys
To access AWS with cmd is done using IAM access keys. They are long term credentials in AWS.
Rotating Access keys - Means creating new access keys.
IAM users are the only identities that use access keys, IAM roles do not use any access keys.

Out of all IAM identity objects (users, groups and role), which one uses access keys to have a connection with::users.
<!--SR:!2024-08-22,6,226-->

Can you attach identity policies to identities outside your AWS account?::No, identity policies can only be attached to identities in your account.
<!--SR:!2024-08-18,2,241-->