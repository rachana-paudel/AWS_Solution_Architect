## Associate Identity Acess Management(IAM)

### IAM is one of the global services of AWS Cloud.
Owner create a root and donot share it to others. User need permission to get access of services like EC2, VPC etc.

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

