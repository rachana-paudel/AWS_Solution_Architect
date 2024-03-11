### Associate EC2

#### Amazon EC2 
+ It is most popular of AWS offering
+ It consist in the capability of
    + renting VM (EC2)
    + storing data on virtual drives (EBS)
    + distributing load across machines (ELB)
    + scaling the services using an auto-scaling, group (ASG)
+ knowing EC2 is fundamental to understand how cloud work.    
+ It provide virtual machine reffered to as EC2 instance in the cloud
+ Give you full control over the guest OS on each instace
+ We can launch instance of any size into an Aavailability Zone anywhere in the world
+ launch instance from AMI
+ we can control traffic to and from instance 
+ uses are application server, web server

#### EC2 User Data
+ It is possible to launch our commands when machine start using ec2 user data script
+ Ec2 user data is used to automate book tasks such as:
 + installine updates
 + installing software
 + downloading common files from the internal
+ EC2 user data script runs with root user 

#### Ec2 instance types
1. General purpose
+ All the types that start with family 't' like t2.micro, t3.micro etc
+ it make balance between compute, memory and networking

2. Compute optimized
+ All types starting with family 'c' like C5.large
+ it is great for computing intensive task that require high performance processors.

3. Memory optimized
+ Series of R like r5.large
+ fast performance for workload, high performance, perform real time processing og big unstructured data.

4. Storage optimized
+ family start with 'D' ,'H' and 'I' like i3.large
+ used for storing intensive task
+ high frequency OLTP system

#### Introduction to Security Group
+ security group is something that is embedded in any instance which act as firewall for that instance
+ all the inbound to the instance and outbound fro the instance are filtered in security group 
+ if the unauthorized port send some information the access is denied
+ authorized IP ranges IPV4 and IPV6
+ if your application is not accessible (time out)then its a issue of security group
+ if your application gives a "connection refused", error when its an applicaion error or its not launched.

#### Classic port to know
+ 22 = SSH(secure shell) to log into a linux instance
+ 21= FTP (file transfer protocol) upload files into a fule sahre
+ 22 = SFTP( secure ftp) upload file using ssh
+ 80 = HTTP- access unsecured websites
+ 443= HTTPS access secured websites
+ 3389 = RDP (Remote Desktop Protocol) log into a window instance

### SSH Summary Table
<!DOCTYPE html>
<html lang="en">

<body>

<table>
  <tr>
    <th></th>
    <th>SSH</th>
    <th>Putty</th>
    <th>EC2 instance connect</th>
  </tr>

  
  <tr>
    <th>Mac</th>
    <td>&#10004;</td>
    <td></td>
    <td>&#10004;</td>
    
  </tr>
  <tr>
    <th>Linux</th>
    <td>&#10004;</td>
    <td></td>
    <td>&#10004;</td>
  </tr>
  <tr>
    <th>Window<10</th>
    <td></td>
    <td>&#10004;</td>
    <td>&#10004;</td>
  </tr>
  <tr>
    <th>Window>=10</th>
    <td>&#10004;</td>
    <td>&#10004;</td>
    <td>&#10004;</td>
  </tr>
</table>

</body>
</html>

### EC2 instance Roles Demo
+ my first instance->connect
+ ec2 instance connect-> connect
+ linux terminal is opened in browser
+ write : aws --version
+ aws iam list-users
+ aws configure
 + It ask for AWS access key id, name, region and output format
 + But it is not good way becaus eit can leak detail if anyone connect to our EC2 instance

#### EC2 purchasing options
1. On demand instance
+ we have to pay for what we use
+ we can pay per second after first minute for windows or linux and hourly for other OS
+ recommended for short term and uninterrupted workload 

2. Reserved Instances
+ It provides upto 72% discount compared to on demand.
+ Reservation period is 1 to 3years
+ payment options- no upfront(+), partial (++), full upfront(+++)
+ convertible reserved instance can change instance type,family, os etc.

3. Ec2 saving plans
+ discount is similar of Reserved instance
+ commit to a certain type of usage( $10|hour for 1 or 3 years)
+ flexible across m5.xlarge, m5.2xlarge etc

4. EC2 spot instances
+ can get discount upto 90% compared to on demand
+ Instances that you can lose at any point of time if your max price is less than the current spot price

5. Ec2 Dedicated Host
+ instance run on hardware that's dedicated to us
+ may share hardware with other instances in the same account
+ no control over instance placement

6. EC2 capacity reservation
+ it is reserved on demand instances capacity in a specific AZ for any duration
+ we always have access to ec2 capacity when you need it
+ charge at on demand rate whether we run instance or not

#### EC2 spot instances requests
The process of requesting and using EC2 Spot Instances in AWS involves several steps:

1. Creating a Spot Instance Request:
   To request Spot Instances, you use the AWS Management Console, AWS CLI, or an SDK to create a Spot Instance request. In this request, you specify parameters such as instance type, maximum price (bid price), availability zone, and the number of instances you need.

2. Spot Instance Pricing:
    AWS calculates Spot prices based on supply and demand for EC2 capacity. Your bid price should be equal to or greater than the current Spot price to ensure your Spot Instances are fulfilled. If the Spot price exceeds your bid price, your instances may be terminated with a two-minute notification.

3. Fulfillment: 
   When your bid price exceeds the current Spot price, AWS fulfills your Spot Instance request by launching the requested instances. The instances run until the Spot price exceeds your bid price or capacity becomes unavailable, at which point they may be terminated with a two-minute notification.

4. Handling Interruptions:
   Since Spot Instances can be interrupted with short notice, it's essential to design your applications to handle interruptions gracefully. You can use strategies like checkpointing, auto-scaling groups, and maintaining state externally to handle interruptions and ensure application availability.

5. Termination Notifications:
   AWS provides a two-minute notification before terminating Spot Instances due to changes in Spot prices or capacity availability. This notification allows your applications to gracefully handle the instance termination by saving state, completing tasks, or transferring workloads to other instances.

6. Monitoring and Managing Spot Instances: 
   You can monitor and manage your Spot Instances using AWS services like Amazon CloudWatch, AWS Trusted Advisor, and AWS Cost Explorer. These services provide insights into instance performance, cost optimization, and recommendations for improving efficiency.

7. Spot Fleet: 
   Alternatively, you can use Spot Fleet to manage a combination of Spot Instances, On-Demand Instances, and Reserved Instances to meet your workload requirements efficiently. Spot Fleet automatically fulfills your capacity requirements while optimizing costs based on your preferences and constraints.

By following these steps and best practices, you can effectively request, manage, and utilize EC2 Spot Instances in AWS to reduce costs and scale your applications dynamically.

#### How to terminate spot instances
There are two types of request
1. One-Time Request: 
   This type of request is for a single, short-term allocation of Spot Instances. With a one-time request, you specify the instance type, the maximum price (bid price) you're willing to pay per hour, the number of instances you need, and other parameters such as the availability zone. AWS attempts to fulfill this request by launching the requested number of Spot Instances that match your specifications. These instances run until they are interrupted due to either the Spot price exceeding your bid price or capacity constraints in the AWS cloud. Once the instances are terminated, the one-time request is considered fulfilled, and you may need to create a new request if you require additional instances.

2. Persistent Request (Spot Fleet): 
   This type of request involves using Spot Fleet, which allows you to maintain a specified number of Spot Instances continuously over time. With a persistent request, you configure Spot Fleet with parameters such as the instance types, the maximum price, the target capacity, and optional parameters like diversification across multiple Spot pools and instance weighting. Spot Fleet continually monitors and maintains the target capacity you specify, replenishing any terminated instances automatically to meet your capacity requirements. This type of request is suitable for long-running or continuous workloads where you need to maintain a certain capacity of instances over time.

#### Strategies to allocate spot instances   
+ lowest price : from the pool with lowest price
+ diversified: distributed across all pools
+ capacity optimized: pool with the optimal capacity for the number of instance
+ price capacity optimized: pods with highest capacity available then select the pod with lowest price
+ spot fleets allows us to automatically request spot instances with lowest price