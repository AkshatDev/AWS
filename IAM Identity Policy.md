IAM Identity Policy is just a set of security statements to AWS. It grants or denies access to AWS programs/features to any identity that uses that identity.

![[iampolicydocument.png]]

A policy document is always in JSON format, it is a collection of different **statements**.

What makes up a statement?

STATEMENT iD "SID", this is the optional part of the statement, it tells you what the statement does. This is a way to **inform the reader** the intention of the statement.

"Resource" - The resource you are trying to interact with, eg s3, ec2. Resource could be a single individual action, a list of actions or wildcards.

'Action' - The action you are trying to perform on the resource, could be a single individual action, a list of actions or wildcards.

'Effect' -  Usually **'Allow' or 'Deny'**.

This could get very complicated very easily. An identity could have 'ALLOWED' access to some resource and be 'DENIED' access to it the same time.

For example, an identity is allowed full access to an s3 but could be denied access to some specific buckets at the same time or an identity is allowed full access to s3 but is a part of a group with denied access.

How do we know what will the final outcome be? 
Remember this order **Explicit Deny, Explicit Allow, Implicit DENY**, in terms of  priority, 'Deny' has the most priority. If an identity is denied access to a resource anywhere, it will take precedence over all ALLOWs, no matter how many policies ALLOW access for the resource to that identity.

Secondly priority is ALLOW, if an identity is allowed access, it will be granted access, unless there is explicit deny.

Third care if nothing is specified, an identity is always (implicit) denied access. **If they are not allowed access they do not have access**.

## Policy types

**Inline**, these policies are usually for individual users. If you want to grant access to a resource to an individual developer, you might use inline policy. These are not scalable because if you do this for 300 employees and want to change it, it is a extremely time consuming. It is not the best practice.

**Managed**, these policies are created as their own **objects**, you can then attach these policies to any identities you want. These are much more scalable and easy to maintain.

There are **2 types of managed policies**, number one **AWS managed**. These are hard to configure if you have different needs.
Second one is **user managed policies**, you can create and use these according to your business needs.

What is the order of priority of access rights in IAM policies?:: Explicit Deny, Explicit Allow, Implicit DENY

What are the most common types of IAM policy types?::Inline and Managed.

## Trust Policy
These policies control which identities can assume that role.

Trust policies can reference Identities in same AWS accounts or identities in other AWS accounts and hence these policies make it very easy to manage more users.

Trust policies can also allow anonymous usage of a role for other types of Identities like facebook, google or twitter.

## Permissions Policy

**Permissions Policy**: This policy specifies what actions and resources the entity assuming the role has access to.