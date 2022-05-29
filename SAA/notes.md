# AWS Accounts

- Having multiple accounts (one for dev, one for test another one for prod) can limit the damage if some information is leaked, since they are containers and only the resources of that account can be deleted.


## Setting up basic AWS Account config
- In real world usage, under account settings, fill the alternate contacts list to keep the owners of the accourn on the loop.

- Activate the IAM access to billing information under settings  as well. This way you don't need to be signed in with your root user to see the information.



## MFA (Multi Factor Authentication)

A factor is a piece of evidence that provides an identity

The 4 most common factors are:
1. Knowledge -> Username and passwords
2. Possession -> Bank Card, MFA device (token generator, could be Gmail)
3. Inherent -> Fingerprint, voice, etc.
4. Location -> A network or WIFI


### How to secure an AWS account with MFA?
1. Go to the right top menu and select "security credentials"
2. Go to MFA and select an option (the easiest one is Virtual MFA)
3. Use any third party application to set up the MFA on your mobile phone or PC (google authenticator is the easiest one)


**You should set a different MFA for each user in the account**


## Budgets
### Setting up budget alerts
1. Go to the right top menu and select "billing dashboard"
2. Go to Billing Preferences and check "Receive invoce by email", "Receive Free tier alert" and "receive billing alerts"

### Creating budget
1. In the billing dashboard go to "Budgets" and "Create a new Budget"
    - Enable the cost explorer
2. Create a Cost Budget
    - Monthly, Recurrent, Fixed & the amount you want
3. Create a budget alert between 50%-80%


# IAM (Identity and Access Management)
**It is globally recilient (stored in all the world)**

There are two different types of users in AWS. You are either the account owner (root user) or you are an AWS  IAM user. The only restrictions from IAM compared to the root user is on some billing features and account closure.

### IAM lets you create 3 different types of identity objects:
1. Users -> Humans or applications that need access to your account
2. Groups -> Collection of related users (development team, finance, HR)
3. Roles -> Can be used by AWS Services or to grant external access to your account

The difference between users and roles is that a user is attached to a specific application or human and the role is like a blueprint you can use for any number of services (like a bunch of EC2 instances or an external application trying to use an S3 bucket)


Policies -> Allow or Deny access to AWS Services ONLY WHEN THEY ARE ATTACHED TO ANY OF THE 3 OBJECTS ABOVE


### In general IAM does:

1. Manages Identities - AN ID Provider (IDP)
2. Authenticate
3. Authorize


**You can create an account alias for a friendlier interface**
go to IAM -> left menu you should see a create alias button


### Creating an admin user
go to IAM -> User -> Create new user -> Attach existing policy for AdministratorAccess.


### Access Keys

An IAM user can have 2 access keys at most.

They can be created and deleted or made active or inactive

Access keys are formed by 2 parts:

1. Access Key (similart to a username)
2. Secret Access Key (similar to a password)

You only get the Secret Access Key ID one time, its your responsibility to store it somewhere.


Rotating access keys just means to create a new pair and remove the old one (that's why you can have 2 of them at the same time). update your applications to use that one instead.


### AWS CLI

use

```
aws configure --profile name_of_profile
```
to confgure multiple AWS accounts credentials in your machine.


# Cloud Computing Fundamentals

Characteristics for a system to be considered cloud

1. On-Demand Self-Service
2. Broad Netweork Access
3. Resource Pooling
4. Rapid Elasticity
5. Measured Service


### On-Demand Self-Service
can provision capabilities as needed without requiring human interaction, on demand.


### Broad Network Access
Capabilites are available over the netowork and access through standard mechanisms

### Resource Pooling
No control or knowledge over the EXACT location of the resources.

Resources are pooled to server multiple consumers using a multi-tenant model.

### Rapid Elasticity
Capabilities can be elastically provisioned and released to scale rapidly outward and inward with deman.

To the consumer, the capabilities available for provisioning often appear to be unlimited.

### Measured Service

Resources usage can be monitored, controlled, reported AND billed.