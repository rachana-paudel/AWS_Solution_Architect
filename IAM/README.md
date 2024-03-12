## Associate Identity Access Management(IAM)

### IAM is one of the global services of AWS Cloud.
Owner create a root and do not share it to others. User need permission to get access of services like EC2, VPC etc.

#### IAM Permission
+ To allow the services
+ User or group can be assign JSON document called policies.
+ These policies define permission of the users.
+ In AWS you apply leave privilege principle don't give more permission than a user needs.

The format of JSON documents looks like the following:
IAM Policy
----------

Version: 2012-10-17

Statement 1:
  Effect: Allow or Deny
  Action: Action(s)
  Resource: Resource(s)

Statement 2:
  Effect: Allow or Deny
  Action: Action(s)
  Resource: Resource(s)

Additional statements can be added here

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:Get*",
      "Resource": "*"
    }
  ]
}

#### Steps for IAM Policies
+ For root user
    + Go to IAM and click 'Users'
    + Click 'Groups'
    + Click on Group name: admin
    + Remove that name
    + Click on IAM and users
    + Make new Users and add permission to that users
    + Click 'IAMReadonly' or something
    + Click User group and create a group
    + set name : developers
    + policy: choose any
    + Choose 'Create group'
    + Click Amin group then choose user
    + Choose the Name created before
    + Add user

+ For IAM Users: When we refresh the browser we get new user that was made previously and Got Readonly Access    

#### IAM Password Policies
+ strong password= high security
+ can set up a password policy by setting length using num alphanumeric and uppercase and lowercase character.
+ Allow IAM user to change their own password
+ prevent password reuse

#### Multifactor Authentication
+ User can change,delete resource to protect root and IAM users
+ MFA= password we know + security devices like Google authenticator(For virtaul) and Universal 2F authentication where physical device is used.

#### How can user access AWS?
1.  Management Console
    + Access keys are generated through AWS Console
    + User manage their own access keys
    + Access keys are secret just like a password so don't share them
    + Access key IS ~=username and secret key ID ~=password

2.  AWS Command Line Interface (CLI)
    + It is tool that enables you to interact AWS services using commands in your command Line Shell
    + Direct access to the public APIs of AWS services
    + You can develop scropts to manage your resources
    + Alternative to AWS Management Console.

3.  AWS Software Development kit (SDK)
    + language specific API
    + enables to access and manage AWS service programming
    + embedded within your application
    + supports
      + mobile SDKs(android, ios)
      + IOT device (embedded C, Arduino)
      + SDKs(JS, python, PHP)

#### CLI setup on Windows
+ click on username of the account on right side
+ Click security credential
+ Create access key
+ tick CLI and check mark the terms and click next
+ Finally click the 'Create Access key"
  + What happened if permission is removed
  => The answer is no respond is shown because permission is denied


#### AWS Cloudshell
  It allows to run CLI cmd directly from the browser without needing to install and configure any software on your local machine.

#### IAM roles for services
+  some AWS service will need to pergform action on your behalf
+  to do so, we will assign permission to AWS service with IAM roles
+  common roles: EC2 instance role
               : Lambda function roles
               : Role for cloud formation  


+ Steps for IAM roles
  + Click 'User' and then choose the user let say 'Rachana'
  + Click Roles then create roles
  + Choose AWS service               
  + Use case: EC2
  + Click 'next'
  + Set Role name: 'DemoEC2
  + Create role
  

#### IAM Security tools
+ IAM credentials report ( account level)
  + A report that list all your account users and the status of their various credentials

+ IAM Access Advisor (user level)
  + It shows the service permissions granted to user and when those service were last accessed
  + You can use this information to revise your policies.    

#### IAM best practices
+  don't use root user except for AWS account setup.
+  1 physical user=1 aws user.
+  assign user to group and assign permission to group.
+ create strong password policy.
+ use and enforce MFA.
+ create roles for giving permissions to AWS service.
+ use access key for programmatic access.
+ audit permission of your account using IAM credentials report and IAM access advisor
+ never share IAM users and access key.

#### AWS Organization
+ It is a global service allows to manage multiple AWS accounts
+ The main account is the management account and other accounts are member accounts
+ member account can only be the part of 1 organization
+ It allows consolidated billing across all accounts so we can perform single payment for different facilities.
+ There is benefit from aggregated usage like ec2,s3 because there is more discount in this process.
+ If reserved instance is unused of one account is not using any services then it means that services can be used by another account within an organization
+ API is used to to automate AWS account creation

<img src="images/aws organization.png" height='100%' width='100%'>

#### Organizational Units (OU)
1.  Business Unit
  + Management account
    + Sales OU
      + Sales account1
      + Sales account2
    + Retail OU
      + Retail account1
      + Retail account2
    + Finance OU
      + Finance account1
      + Finance account2

2. Environmental Lifecycle
  + Production OU
  + Dev OU
  + Test OU

3. Project Based
  + Project1 OU
  + Project2 OU
  + Project3 OU 

#### Security: Service Control Policies(SCP)
+ IAM policies applied to OU or accounts to restrict users and roles
+ They do not apply to the management account
+ must have an explicit allow

<img src='images/scp heirarchy.png' height='100%' width='100%' >

1. Management account can do anything
2. Account A can do anything except Redshift
3. Account B can do anything except access redshift, except lambda
4. Account C can do anything except access redshift

#### SCP Examples
Blocklist and Allowlist strategies
<img src='images/allow and block list.png' height='100%' width='100%' >

### End of IAM 