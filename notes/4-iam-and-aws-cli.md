# IAM & AWS CLI

Root Account
- only used to set up account

AIM 
- one user per person

- User can be grouped by groups
- Users don't need to belong to a group
- User can belong to multiple groups

Policy
- Policy describes services user is allowed to use
- JSON document
- Users can be assigned a policy

Least Privilege Principle
- Give only the least amount of privileges a user needs to complete their tasks

---

## IAM Policies

Policy
- Policy describes services user is allowed to use
- JSON document
- Users can be assigned a policy

Policy can be attached at group level or an individual user

Version # - 2012-10-17
id
One or more Statements
  sid - statement id
  Effect - Allow / Deny
  Principal - which accounts this policy will be applied to
  Action - list of actions policy allows or denies
  Resource - list of resources actions will be applied to
  Condition - (optional) - conditions for when policy is in effect

---

## MFA Devices

virtual MFA device
- Google Ahtenticator
- Authy

Universal 2nd Factor Security Key
- YubiKey - USB device used as a key

Hardware Key Bof MFA Device
- Gemalto

---

## Ways to Access your AWS Account

AWS Management Console
  - Protected by MFA, password

AWS CLI
  - Protected by access keys

AWS SDK
  - protected by access keys

User manages their own access keys. Not to be shared
Access Key ID ~= username
Secret Access Key ~= password

## AWS CLI

- Direct access to public APIs of AWS services
- You can develop scripts to manage your resources

CLI is open source
[https://github.com/aws/aws-cli](https://github.com/aws/aws-cli)

## SDK
- language specific APIs
- allows for managing AWS services programatically
- Embedded within app
- Js, PY, PHP, .NET, Ruby, Go, Node, C++, IoT device SDK
- The AWS CLI is built on the AWS SDK for python

--

## AWS Cloud Shell

https://docs.aws.amazon.com/cloudshell/latest/userguide/faq-list.html#regions-available

---

## IAM Roles

- Roles will allow AWS recourses we create to perform actions on our behalf
- Roles will have permissions attached to them to grant permissions to AWS resources

For example
- EC2 instance roles (virtual machine / virtual server)
- Lambda function roles
- CloudFormation roles

---

## IAM Security Tools

An IAM entity that defines a set of permissions for making requests to AWS services, and will be used by an AWS service.

IAM Credentials Report
- Created at the account level
- A report listing all your account's users and the status of their various credentials

IAM Access Advisor
- Created at the user level
- shows service permissions granted to a user
- When those services were last accessed

- Can use the access advisors tab in user pane to see when services were last used
- Can Consider removing services that are not being used

## IAM Best Practices

- Do not use root account except when setting up other accounts
- One AWS user should correspond to one physical user
- Can assign users to groups and assign permissions to groups
- Create strong password policy
- Use and enforce MFA (Multi-factor authentication)
- Create and use roles for giving permissions to AWS services
- Generate Access Keys when using CLI / SDK
- Audit permissions of your account with IAM credentials report
- Never share access keys or user credentials


