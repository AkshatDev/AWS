
ACT can be thought of AWS organizations but with more features (**new AWS Orgs with more features**). 
- Quick and easy setup for multi-account environment.
- Orchestrates other AWS services to provide this functionality.
- Uses organizations, IAM Identity Center, CloudFormation,  Config and more ...

- Landing zone - multi account env (this is where most of the interaction with ACT happens)
- Provides Guard Rails, which allows to detect/Mandate rules/standards across all accounts.
- Account Factory - Automate and Standardises new account creation.
- Dashboard - single page oversight of the entire environment .
- Uses AWS config and [[Service control policies]] to maintain guardrails, these detect drifts away from governance standards.

Just like AWS orgs, ACT is created within an AWS account, this account then becomes the **management account** of the landing zone.

When ACT is first setup it first creates **2 organizational units** 
- **Foundational Organisational Unit**, by default called security.
		Inside Foundational US, there are 2 accounts by default -
		**Audit Account**.
		Users that need access to the audit info made available by the ACT.
		This account could also be used as location for any 3rd party tools to perform auditing of your env.
		Example - CloudWatch for monitoring landing zone wide metrics.
		**Log Archive Account**.
		 For users that need all login info for all the accounts in the landing zone.
		 Example AWS Config and CloudTrail logs, they are stored here.

- **Custom foundational unit**, by default called sand box.

## Account Factory

ACT provides **Account Factory**, this is like a team of robots that can create,modify, delete AWS accounts as you need them. 

Can be interacted with ACT or service catalogue.
**Account Factory creates AWS accounts inside the Custom Foundational OU, in a fully automated way.**
The config of these accounts is handled by Account Factory.
CloudFormation is used under the hood for most of this automation.

## Guard Rails

Rules for multi-account governance.
They come in 3 types, Mandatory, Strongly Recommended or Elective.
They function in 2 ways, **preventive and detective.**

Preventive guard rails are enforced or not enabled, example allow or deny regions or disallow bucket policy changes

Detective - These are like compliance checks.
These are either clear, in violation or not enabled. example detect CloudTrial enabled or EC2 instances have public IPv4.


The difference is preventive guard rails stop something and detective guard rails will only detect something.