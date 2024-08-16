---
tags:
  - basics
---

![[iam_user_authentication.png]]

IAM Users are an identity used for anything  requiring long-term AWS access, e.g. Humans, Application or service accounts.

If you can identify **one thing, individually** that needs access to some AWS services, most of the times, IAM user is required.

**Authentication**
When an IAM user has to access any AWS rervice or resource it has to prove it's identity to IAM using username/password or access keys, this process is called authentication.

 **Authorization**
 Once IAM has authenticated a user, and the user wants to use a service or a resource, AWS then checks all if that identity is authorized to do that using all the policy statements for that identity.

How many IAM Users are allowed per account::5000 IAM Users
<!--SR:!2024-08-17,1,190-->
How many groups can an IAM user be a memmber of?::10 Groups
<!--SR:!2024-08-18,2,210-->