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
+ we can move management account of test to prod or any other by  check in taht account-> action-.move->prod

##### To restrict service control policies
+ click on aws organization and click on policies
+ I shows 4 policies which are disable
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
    ]
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

      
        
      


### End of IAM 