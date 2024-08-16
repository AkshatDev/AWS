---
tags:
  - basics
---


You cannot log into an IAM group as groups do not have credentials.

- IAM groups exist to make it easy to **organise large sets of users**.
- IAM Groups can have **inline and managed policies attached** to them.
- A single IAM group could **have any number of users** (max number of total users is a single AWS account is 5000).
- There is no **build-in all users group** that AWS provides you, you can make one and manage it yourself.
- **No nesting is allowed**.
- There is a limit of **300 IAM groups** but **this is a soft limit and** can be increased with an email.

There are policies that can be attached to resources, these policies can reference identities using ARNs, although groups do have ARNs they are not considered an AWS resource in the same way that users or roles are.

**Groups are not a true identity and hence cannot be referenced as a principal in a policy.**

Can IAM groups be referenced in resource policies using ARNs?::No, because they are not considered an AWS resource in the same way that users or roles are, although groups do have ARNs.
<!--SR:!2024-08-23,7,250-->