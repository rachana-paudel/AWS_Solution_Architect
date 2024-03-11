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