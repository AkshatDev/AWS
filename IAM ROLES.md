A role is suited when you have multiple principals.
There could be multiple users inside AWS account or multiple users outside AWS that can use these roles.

If you cannot identify number of principals which use an Identity then an IAM role is best suited.
If you have more than 5000 principals, then because of limit for IAM users, roles are better suited.

Roles are also used for temporary basis. Roles are assumed my some principals for temp basis and are then cleared.
A roles is not something that represents you, it is something that represents level of access in AWS.

Roles can have policies attached to them, either inline policies or managed policies.

**IAM roles have 2 types of policies that can be attached, [[IAM Identity Policy#Trust Policy| Trust Policy]] or [[IAM Identity Policy#Permissions Policy|Permissions Policy]].**

If a role gets assumed by something that is allowed to assume that role then AWS generates temp credentials using [[Secure Token Service]] (STS) for that identity assuming that role.

These temp credentials will be able to access what ever resources are specified in permissions policy.

Roles are real identities and just like IAM users, roles can be referenced withing resource policies.


## When to use IAM Roles

The most common use of IAM Roles is AWS services inside the same AWS account, for example AWS lambda.

## Service Linked Roles

SLR is simply an IAM role linked to a specific AWS service.

They provide a set of permissions that are pre defined by a service.

They provide permissions that a service needs to interact with other AWS services on your behalf.

The difference bw a role and a SLR is that you cannot delete a SLR until it is no longer required.

### Example

Let's say you use AWS RDS (Relational Database Service). AWS RDS can automatically back up your database to S3. To perform this action, RDS needs access to S3. Instead of requiring you to manually create a role and attach policies that allow RDS to write to S3, AWS provides a Service-Linked Role with the necessary permissions predefined. When you set up backups, RDS assumes this role, ensuring it has the permissions needed to write backups to S3 without any additional configuration on your part.
## PassRole 
This is a permission that allows an AWS service or user to pass a role to another AWS service. For example, allowing EC2 instances to pass an IAM role to an AWS Lambda function that might be triggered to process data on the instance. It's crucial for scenarios where one service creates or manages resources that then require a role to operate.