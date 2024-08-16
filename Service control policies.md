---
tags:
  - basics
---

These are just policies in JSON format. There are used to set permissions for AWS accounts, org units or root containers.

SCPs inherit down the org tree, ed, if they are attached to an OU they affect all the member accounts inside, similarly if they are attached to the root container, they affect all the org members.
 
 **SCPs do not affect the org management account**. There for security purposes, it makes sense to never use the management account for any resources in production.

- SCPs are account permission boundaries.
- They limit what the account (including account root user) can do. Although you cannot directly restrict the account root but using SCPs you can restrict the account itself thereby restricting the account root.
- They **do not grant any permissions**. SCPs only limit permissions but are not able to grant any.

## Allow list architecture  vs Deny List architecture

### Allow List Architecture

In an **Allow List architecture**, the default stance is that all actions are denied unless explicitly allowed. This approach is typically more secure because it ensures that permissions are granted intentionally and minimally. For SCPs, this means:

- **Specifically Allow**: You specify only the actions that accounts or users are allowed to perform.
- **Security Posture**: By default, no actions are permitted unless they are explicitly included in the SCP, reducing the risk of unintended privileges being granted.

### Deny List Architecture

Conversely, a **Deny List architecture** starts with everything allowed unless explicitly denied. This approach can be more flexible but might introduce more risk, as it depends on administrators explicitly blocking potentially harmful actions. For SCPs, this means:

- **Specifically Deny**: You list the actions that accounts or users are not permitted to perform.
- **Open by Default**: All actions are allowed, except those specifically denied. This can be useful when you trust the users or accounts but want to prevent specific actions that could pose risks.

What is the effect of attaching a Service Control Policy (SCP) to the root container in AWS Organizations?:: SCPs attached to the root container affect all organizational units and accounts within the organization, except the management account.
<!--SR:!2024-08-17,1,230-->

How do SCPs affect the management account in AWS Organizations?:: SCPs do not affect the management account, which retains full permissions to manage the organization and all its accounts.

What is the difference between an Allow List and a Deny List architecture in the context of SCPs?:: An Allow List architecture specifies only the actions that are explicitly allowed, defaulting to deny all others. A Deny List architecture allows all actions except those specifically denied.
<!--SR:!2024-08-17,1,230-->

Can SCPs grant permissions to AWS accounts or users?:: No, SCPs do not grant permissions; they only restrict permissions based on what is specified, serving as permission boundaries within AWS Organizations.


## Explicit Deny in SCPs

**If an SCP explicitly denies an action, any request to perform that action is denied, regardless of what the identity-based policies say**. This is straightforward and aligns with your understanding of explicit deny overriding any allow.

## Absence of Explicit Allow in SCPs

SCPs do not actually need to explicitly deny an action to restrict access. Because SCPs define the maximum permissions boundary for accounts within an AWS Organization, if an action is not explicitly allowed in an SCP, it's as good as being denied. This means that:

- **If an SCP does not mention (allow) a specific action, no entity within the affected accounts can perform that action, even if their attached identity-based policies allow it.**

This mechanism works because SCPs restrict the permissions space that identity-based policies can operate within. Therefore:

- **SCPs as Permission Boundaries**: They set the outer limits of what’s permissible. Anything outside this boundary is implicitly denied unless explicitly allowed by an SCP.
- **Identity Policies as Permission Granters**: Within the boundary set by SCPs, identity policies specify what the entities are allowed to do. They can't grant permissions outside the boundaries set by SCPs.

## Effective Permissions Calculation

![[scp_iam_policies.png]]

The effective permission for any action is determined by both the SCPs and the identity-based policies:

- If the SCP does not explicitly allow an action, the action cannot be performed, regardless of identity policies.
- If the SCP allows an action, the identity policies then determine whether the action is allowed for specific users or roles.

What happens if a principal is allowed all access to an s3 but there is not explicit allow in any SCPs for any actions on s3 for that principal
? 
The principal will not be able to perform any actions on S3. The SCP's absence of an explicit allow on S3 actions overrides and restricts the permissions that the identity policy can grant.