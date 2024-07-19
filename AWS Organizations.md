---
tags:
  - basics
---

![[AWS_ORGANIZATIONS.png]]

AWS orgs in a cost-effective way that helps large businesses to manage multiple AWS accounts.

This is how (ideal situation) AWS organizations is structured.

- A standard AWS account (**this is not within any organization**) is created.
- Using this account, an AWS org is created , this AWS account becomes the AWS management account or **master account**.
- Using the master account, you can invite other standard AWS accounts into the organization.
- If the accounts invited are already existing accounts then they need to accept the invite.
- When stasndard AWS accounts join the AWS organization then they become the members of the AWS account (member accounts).
- Orgs have one and **only one management account** and 0 or more member accounts.
- Structure withing AWS accounts is **hierarchical**, like a tree.
- Inside an AWS organization there is a **Organization Root Container**, this is different than AWS root user.
- This container can contain member or management accounts as well, this container can also contain other **containers** called as **organizational units**, these units can also have AWS member accounts and their own complex  nested structures.
- You can also create new AWS accounts within an AWS organization , since these accounts are created withing the organization then there is no invites to be accepted.
- When using AWS organizations, the best practices of using AWS change. Using IAM roles instead of IAM users if preferred.
- Large organizations can have their own identity system and based on that they can have an identity account, this Identity account can use **identity federation** and handle logins to this Identity account. Then using **roll switch** instead of logging in to separate AWS member accounts it becomes easy to access member accounts.

## Features

**Consolidated billing** - 
Billing methods of AWS members accounts (if existing) are removed and instead passed to the management/master account (sometimes also referred to as payer account). This removes the overhead of managing multiple billing methods for a large company and could be the most important reason alone to use AWS organizations.

Since all the usage of services used my member accounts is consolidated together, this allows organizations to avail offers and discounts on services that AWS offers.

Usually payer account is the master account but sometimes to keep the master account clean, some companies might create a member account and use that as the payer account.

**[[Service control policies]]**-
AWS organizations also contain SCP feature, this lets you restrict what AWS accounts in an AWS organization can do.

---
What is the role of the management account in AWS Organizations?:: The management account is responsible for managing the entire AWS Organization, including creating new accounts, inviting existing AWS accounts to join the organization, and applying service control policies across all accounts.

Can organizational units (OUs) in AWS Organizations contain the management account?:: No, organizational units cannot contain the management account. The management account exists outside of any OU to maintain centralized control over the organization.

What is the purpose of service control policies (SCPs) in AWS Organizations?:: SCPs are used to centrally manage permissions in AWS Organizations, allowing administrators to define and enforce permission guardrails that all accounts within the organization must adhere to.

How does consolidated billing work in AWS Organizations?:: Consolidated billing in AWS Organizations aggregates the usage from all member accounts into a single bill managed by the management account. This approach simplifies billing management and may allow organizations to receive volume discounts on AWS services.

Is it possible to designate a different account for billing purposes in AWS Organizations, apart from the management account?:: Yes, although the management account typically handles billing, AWS Organizations allows the designation of a different account as the billing account if needed, helping keep billing separate from management activities.

What is the Organizational Root Container in AWS Organizations?:: The Organizational Root Container is the top-level container in an AWS Organization's hierarchy. It organizes all accounts under it, including the management account and any organizational units (OUs), but does

What is the purpose of Organizational Units (OUs) in AWS Organizations?:: Organizational Units (OUs) in AWS Organizations help manage groups of AWS accounts by allowing administrators to apply policies and service control policies at a more granular level than the organizational root, facilitating better control and management of subsets of accounts.
