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

3.  AWS Softwate Development kit (SDK)
    + language specific API
    + enables to access and manage AWS service programming
    + embedded within your application
    + supports
      + mobile SDKs(android, ios)
      + IOT device (embedded C, Arduino)
      + SDKs(JS, python, PHP)
