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
    + Click Admin group then choose user
    + Choose the Name created before
    + Add user

+ For IAM Users: When we refresh the browser we get new user that was made previously and Got Readonly Access    

#### IAM Password Policies
+ strong password= high security
+ can set up a password policy by setting length using num alphanumeric and uppercase and lowercase character.
+ Allow IAM user to change their own password
+ prevent password reuse

#### Multifactor Authentication
+ User can change, delete resource to protect root and IAM users
+ MFA= password we know + security devices like Google authenticator(For virtual) and Universal 2F authentication where physical device is used.

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

#### Lab
+ search aws organization which is global service and click create an organization
+ add a new account
+ we can create or invite existing account using email and sending invitation
+ we can view invitation
+ go to aws organization again and click invitation it shows 'accept' click there
+ after accepting invitation click on dashboard
+ back to aws organization and aws account there is root click there
+ click action 'create new'
+ organizational unit name ='Dev' create OU
+  action:create new 
+ organizational unit name 'test'
+ organizational unit name 'prod'
+ again inside prod click prod and -> action -> create new-> OU name:HR
+ again action-> finance
+ Aws accounts it shows all the OU
+ we can move management account of test to prod or any other by  check in that account-> action-.move->prod

##### To restrict service control policies
+ click on aws organization and click on policies
+ It shows 4 policies which are disable
+ click service control policies-> enable service control policies
+ click service control policies
+ create new policy
+ policy name: DenyAccessS3
+ In JSON command "Effect": "Deny"
+ In the right side of JSON code there are some statement and search for S3 and click "s3:*"  and resource=[*]
+ create policy
+ Now check policies by clicking the 'aws accounts'-> root-> policies (i shows policies attached directly)
+ Likewise in children OU -> policies( there is one extra that is inherited from root)

##### We can attached new policy
+ click on any child (finance) and policy
+ attach policy click on 'DenyAccessS3' or other we made it shows 'DenyAccessS3 has been inherited from finance
+ if we search S3 services and bucket there is no permission because we have denied permission

#### IAM Conditions
1. aws:SourceIp
  + used to restrict the client Ip from which the API calls are being made
  + It has deny * on everything if its not an IP address and then we have a list of two CIDRs of two Ip address ranges. So that means that unless the client makes an API call from within these IP addresses then the API call is being denied
+ this can be used to restrict usage on AWS only to, for example your company network and therefore guaranteeing that only your company can access your own AWS environment so that's one of these conditions 

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "*",
      "Resource": "*",
      "Condition":{
        "NotIpAddress":{
          "aws:SourceIp":[192.0.2.0/24,"23.0.113.0/24]
        }
      }
    }
  ]
}

2. aws:RequestedRegion
+ restrict the region the API calls are made to
+ it is something global because it started at the AWS and its restricting the region the API calls are made to. So in this one we deny anything on EC2. RDS, and DynanoDB
+ if we are in the region eu-central-1 or eu-west-1, so here we deny access to these services in this specific region on their organization SCP to deny or to allow only access to a specific region

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "["ec2:*,"rds:*","dynamodb:*"]",
      "Resource": "*",
      "Condition":{
        "StringEquals":{
          "aws:SourceIp":["eu-central-1","eu-west-1"]
        }
      }
    }
  ]
}

3. ec2:ResourceTag
+ there is prefix ec2 therefore this applies to the tags on your ec2 instance. And so here we allow to start and to stop instances, for any instance if the Resource Tag/Project is equals to DataAnalytics
+ That means that if the ec2 instance has the correct tags, being project and DataAnalytics, then we're good
+ but then as you can see there is the aws:PrincipleTag, and this applies to your user tag. So its not an ec2 instance tag, this is a user tag.
+ so your user must also be the part of department data to perform these actions

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "["ec2:startInstances","ec2:StopInstances"]
      "Resource": "arn:aws:ec2:us-east-1:1233456789012:instance/*",
      "Condition":{
        "StringEquals":{
          "ec2:ResourceTag/Project": "DataAnalytics",
          "aws:PrincipalTag/Department":["Data"]
        }
      }
    }
  ]
}




4. aws:MultiFactorAuthPresent
+ to for MFA
+ but the user can do anything on EC2, but they can only stop and terminate instances if they have MFA so this is deny on false


{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "ec2:*,
      "Resource": "*"
    
    },
    {
      "Effect": "Deny",
      "Action": "ec2:StopInstances","ec2:TerminateInstances"],
      "Resource": "*",
      "Condition":{
        "BoolIfExists":{
            "aws:MultiFactorAuthPresent":false
        }
      }
    }
  ]
}

#### IAM for S3
+ we have two bucket list
+ first one is list bucket and this applies to this arn right here, so s3:::test because its a bucket level permission and therefore we have to specify the bucket itself
+ This permission allows the user to see the list of objects within the bucket.

+ but if we have a look at second(object level permission) GetObject, PutObject, and delete object this applies to objects within a bucket and therefore your arn is going to be different and you are going to have /* to represent all the objects within your buckets
+ this is why we have different arn because this is object level permission.


{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "["s3:ListBucket"]
      "Resource": "arn:aws:s3:::test"
    },
    {
      "Effect": "Allow",
      "Action": "[
        "s3:PutObject,
        "s3:GetObject",
        "s3:DeleteObject"
        ],
      "Resource": "arn:aws:s3:::test"
    }
  ]
}

<img src='images/resource policies.png' height='100%' width='100%' >
      

#### IAM Roles vs Resource Based Policies
Cross account are those account which allow a principal in one account to access resources in a second account. It can be done in 2 ways

1. IAM roles:
+ Certainly! Imagine you have two accounts: Account A and Account B. Account A wants to access Amazon S3 (a storage service), but it doesn't have permission. So, what you do is you assign a special role (think of it like a set of permissions) to Account B that allows it to use Amazon S3.

+ Now, when someone from Account A wants to use Amazon S3, they don't directly use their own permissions. Instead, they "put on" the permissions of Account B by assuming the role assigned to it. In simple terms, assuming a role means you're temporarily swapping your own permissions for the ones assigned to that role. It's like borrowing someone else's keys to open a door because yours won't work. Once you're done using the borrowed permissions, you go back to using your own.


2. Resource based policies
+ When a user in Account A applies an S3 bucket policy to access Amazon S3, they're setting rules directly on the bucket itself. Unlike assuming a role, where one gives up their own permissions to adopt another's, with a resource-based policy, the user doesn't have to surrender their permissions. Instead, they're simply setting rules for who can access the bucket and how. It's like installing a lock on a door; the person with the key (the user) doesn't lose their ability to open the door, they're just controlling who else can enter.

###### Difference
+ Resource-based policy: With a resource-based policy, you're directly attaching policies to specific AWS resources like Lambda functions, SNS topics, SQS queues, CloudWatch Logs, or API Gateway endpoints. For example, you can create a resource-based policy to allow Amazon EventBridge to send events to a particular SNS topic. This means the resource itself (e.g., the SNS topic) dictates who can access it, rather than the user or role.

+ IAM role: Conversely, when using IAM roles, you're granting permissions to entities assuming those roles. For instance, you might have an IAM role that allows a Kinesis stream, Systems Manager Run Command, or ECS task to access resources like S3 buckets or DynamoDB tables. These permissions are associated with the role itself, and entities assume the role to temporarily gain those permissions.

### IAM Permission Boundaries
+ It is supported for users and roles(not group)
+ advanced feature to use a managed policy to set the maximum permission an IAM entity can get
+ Go to IAM -> User-> User name:john->next permission->next tags->review->create user
+ Click john->add permissions->attach existing policies(any we want)->review->add permission
+ click job->set boundary->select any we want->set boundary
+ It can be used as a combinations of AWS Organizations SCP
The intersection of organization scp, permission boundary, identity based policy is called 'effective permissions'
+ Use cases:
  + Delegate responsibilities to non administrators within their permission boundaries for example create newIAM users
  + allow developers to self-assign policies and a
  manage their own permissions while making sure they cant escalate their privileges
  + useful to restrict one specific user

 for IAM permission boundary
 <br>
 {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "iam:*",
      "Resource": "*"
    }
  ]
}
<br>

for IAM permission for IAM policy<br>
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example-bucket/*"
    }
  ]
}
<br>
if we use both then we get permission denied because iam is denied but can use ec2 becuase that is not denied.


<img src='images/iam policy evaluation logic.png' height='100%' width='100%' >


#### IAM Identity Center( successor to aws single sign-on)
+ One login for all your:
  + AWS accounts in AWS Organizations: AWS Organizations enables you to centrally manage and govern multiple AWS accounts. With a single login, typically through AWS Single Sign-On (SSO), users can access all AWS accounts within the organization without needing separate credentials for each account.

  + Business cloud applications (e.g., Salesforce, Box, Microsoft 365, etc.): Similarly, through a single sign-on solution like AWS SSO or a third-party identity provider (IdP) such as Active Directory (AD) or OneLogin, users can access various business cloud applications without the need for multiple sets of credentials.

  + EC2 Windows instances: For accessing EC2 Windows instances, you can leverage AWS Systems Manager's Session Manager feature, which allows secure remote shell access to EC2 instances without requiring SSH keys or opening inbound ports. Users can authenticate using AWS SSO or IAM credentials.

+ Identity Providers:

  + Built-in identity store in IAM Identity Center: AWS IAM (Identity and Access Management) provides a built-in identity store where you can manage users and their permissions within AWS. This allows you to create and manage IAM users directly within AWS.

  + Third-party Identity Providers (e.g., Active Directory, OneLogin, etc.): These are external services that manage user identities and authentication outside of AWS. For example, Active Directory is commonly used in on-premises environments and can be integrated with AWS using AWS Directory Service. Similarly, OneLogin is a cloud-based identity and access management solution that can be integrated with AWS for centralized user authentication and access control.


<img src='images/iam identity center.png' height='100%' width='100%' >

#### AWS IAM Identity Center Fine-grained permissions and assignments
1. Multi- account permission
+ manage access across aws accounts in your aws organization
+ permission sets- a collection of one or more IAM policies assigned to users and groups to define aws access

2. application assignments
+ provide required url , certificate and metadata
+ SSO access to many SAML 2. business applications (Salesforce Box, Microsoft 365,..)

3. Attribute based access control (ABAC)
+ fine grained permissions based on users attributes stored in IAM Identity Center Identity Store
+ Example cost centre, title, locale, ..
+ USe case: define permission once then modify aws access by changing the attributes

#### Microsoft Active Directory (AD)
+ It is software found in any windows server with AD Domain services
+ Database of Objects: AD serves as a database storing various objects such as users, accounts, computers, printers, file shares, and security groups.

+ Centralized Security Management: It provides centralized security management, allowing administrators to create user accounts and assign permissions across the network.

+ Organizational Structure: Objects in AD are organized hierarchically in a tree-like structure, with each tree containing domains. Domains are logical groupings of objects within a network.

+ Forest in Active Directory:

  + A group of trees in Active Directory is referred to as a forest.
  + A forest is a collection of one or more domain trees that share a common schema, configuration, and global catalog.
  + Each tree in the forest maintains a separate namespace but shares a common schema and trust relationship.
  + Forests enable organizations to establish separate domains with their own administrative boundaries while allowing for communication and resource sharing between them.

+ Example:
  + we have a domain controller and create an account with username john and password= password
  + the idea that all the other windows machines we have within our network are going to be connected to domain controller, so that if we are using the john password on the first machine is going to look it up in the controller and say yes we have that login and then allow you to login in that machine
  + so all these machines are going to be connected to your domain controller and that allows you to have the users accessible on any single machine

#### AD services
1. AWS Managed Microsoft AD
+  to create your own AD in aws, manage users locally, supports MFA
+  you can also create trust connections with your on-premise AD
+  user shares trust between on-premises and aws managed AD
+  on-premise trust aws and aws trust on-premises
+  if on-premise directory user goes an authentic to your on-premise AD using AWS accounts, and vice versa, it can be trusted to go and look it up

2. AD Connector
+ directory gateway(proxy) to redirect to on-premise AD, supports MFA and it support MFA if you need MFA
+ users are solely managed into the on-premise AD
+ AD connector act as proxy,perform query for on-premise AD

3. Simple AD
+ cannot be joined with on-premise AD
+ AD compatible managed directory on AWS

Using AD you can create ec2 instances that are going to be run in windows and these windows instances can join the domain controllers for your network and shares all the logins, credential and so on.

#### Connection of IAM Identity Center with AD Setup
+ if you connect to AD that is managed on your aws using the directory service then the integration is out of the box. You just tell IAM identity center to integrate and connect to your aws managed microsoft AD
+ if we have self managed directory for example on-premises, in that case, you have 2 ways of connecting to your self managed directory
  + the first one is to create 2 way trust relationship using aws managed microsoft AD and the you setup 2 way trust relationship between you AD then you use out of the box integration coming from IAM identity center for single sign-up
  + the other option would be to use an AD Connector. so an AD connector would have the role to integrate with IAM identity center. And then you would connect to it and then it would automatically proxy any kind of request on to your self managed directory.

<img src='images/selfmanage directory.png' height='100%' width='100%' >

#### Lab
+ search service called 'directory service'
+ setup directory -> directory types: aws managed microsoft AD (or any we want)-> next
+ Edition: Enterprise edition-> next
+ Likewise we can choose any directory types  we want

#### AWS Control Tower
+ easy way to set up and govern a secure and compliant multi-account aws environment based on best practices
+ aws control tower uses aws organizations to create accounts
+ automate the setup of your environment in a few clicks
+ automate ongoing policy management using guardrails
+ detect policy violations remediate them
+ monitor compliance through an interactive dashboard

#### AWS Control Tower - Guardrails
+ provides ongoing governance for your control tower environment
+ There are 2 kinds of guardrails:

  a.  Preventive Guardrails:
    Preventive guardrails aim to prevent accounts from performing certain actions that could lead to security risks or non-compliance.
    These guardrails typically use Service Control Policies (SCPs), which are applied at the AWS Organizations level to enforce restrictions across all accounts within your AWS environment.
    For example, you can use SCPs to restrict certain AWS regions, limit access to specific services, or enforce encryption requirements.

  b. Detective Guardrails:
    Detective guardrails focus on detecting non-compliance or potential security issues within your AWS environment.
    These guardrails leverage services like AWS Config to monitor resource configurations and changes.
    For instance, you can set up detective guardrails to detect untagged resources, unauthorized IAM permissions, or non-compliant configurations.

Both preventive and detective guardrails work together to provide ongoing governance and compliance for your AWS Control Tower environment. Preventive guardrails help enforce policies proactively, while detective guardrails help identify and address compliance issues after the fact.

<img src='images/control tower.png' height='100%' width='100%' >  







### End of IAM 