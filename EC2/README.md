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


