#### Scalability & High Availability
+ Scalability means that an application / system can handle greater loads 
by adapting. 
+ There are two kinds of scalability:
+ Vertical Scalability
+ Horizontal Scalability (= elasticity)
+ Scalability is linked but different to High Availability
+ Scalability refers to a system's ability to handle increasing loads by adding resources or scaling out horizontally across multiple nodes.

+ High availability, on the other hand, is concerned with ensuring that a system remains operational and accessible for a high percentage of time, typically measured as uptime.

1. Vertical Scalability:

+ Involves increasing the size or capacity of a single instance or server.
+ Commonly used for non-distributed systems such as databases.
+ Example: Upgrading from a small instance like t2.micro to a larger instance like t2.large.
+ Services like RDS (Relational Database Service) and ElastiCache support vertical scalability.
+ There is typically a limit to how much you can vertically scale due to hardware constraints.

2. Horizontal Scalability:

+ Involves increasing the number of instances or systems for an application.
+ Commonly used for distributed systems, such as web applications.
+ Easily achieved with cloud offerings like Amazon EC2, where you can spin up multiple instances as needed.
+ Horizontal scalability allows the workload to be distributed across multiple machines, increasing overall capacity and redundancy.

#### High Availability (HA) and Horizontal Scaling:

+ High Availability (HA):

    + Often coupled with horizontal scaling.
    + Involves running the system in at least 2 data centers (Availability Zones).
    + Goal: Survive a data center loss to maintain operational continuity.

+ Passive HA:
    + Example: RDS Multi-AZ.
    + Standby resources are activated during failures.

+ Active HA with Horizontal Scaling:
    + Distributes workload across multiple active instances.
    + Load balancers manage traffic distribution for scalability and redundancy.

#### Types of Scaling
+ Vertical Scaling:
    + Increasing the size of a single EC2 instance by upgrading its specifications.
    + Example: Upgrading from a small instance like t2.nano to a large one like u-12tb1.metal, which offers significantly more resources.

+ Horizontal Scaling:
    + Increasing the number of EC2 instances to handle increased load or traffic.
    + Achieved using Auto Scaling Groups, which automatically adjust the number of instances based on predefined conditions.

+ Load Balancer:
    + Distributes incoming traffic across multiple EC2 instances to ensure optimal resource utilization and availability.
    + Helps in horizontal scaling by evenly distributing workload among instances.

+ High Availability:
    + Ensures continuous operation and minimizes downtime by deploying EC2 instances across multiple Availability Zones (AZs).
    + Auto Scaling Groups can be configured to launch instances in multiple AZs for redundancy and fault tolerance.
    + Load Balancers can also be set up to route traffic to instances in different AZs for improved availability and reliability.


#### Load Balancing
+ Load Balances are servers that forward traffic to multiple 
servers (e.g., EC2 instances) downstream
<img src='images/elb.png' height='100%' width='100%' >



#### Why use a load balancer?

+ Spread load across multiple downstream instances: Balances incoming traffic across multiple servers, preventing any single server from being overwhelmed.

+ Expose a single point of access (DNS) to your application: Simplifies access for users by providing a single entry point to the application.

+ Seamlessly handle failures of downstream instances: Detects and redirects traffic away from failed or unhealthy servers, ensuring continuous service availability.

+ Do regular health checks to your instances: Monitors the health of downstream servers and removes unhealthy instances from the pool of available servers.

+ Provide SSL termination (HTTPS) for your websites: Terminates SSL connections at the load balancer, reducing the processing load on backend servers and simplifying SSL certificate management.

+ Enforce stickiness with cookies: Maintains session persistence by directing subsequent requests from a client to the same backend server, which can be useful for stateful applications.

+ High availability across zones: Distributes traffic across multiple data centers or availability zones to improve reliability and fault tolerance.

+ Separate public traffic from private traffic: Acts as a gateway, separating incoming public traffic from internal/private traffic, enhancing security and network segmentation.

#### Why use Elastic Load Balancing?
+ Managed Load Balancer: ELB is a managed service provided by AWS, meaning AWS handles the setup, maintenance, and upgrades of the load balancer infrastructure.

+ Guaranteed Working: AWS guarantees the reliability and availability of ELB, ensuring that it remains operational and performs as expected.

+ Maintenance and High Availability: AWS manages the high availability of ELB, ensuring that it is fault-tolerant and available even during upgrades or maintenance activities.

+ Limited Configuration Knobs: ELB abstracts away much of the complexity of load balancer configuration, offering a simplified interface with only a few configuration options, making it easier to use.

+ Cost-Efficient: While setting up your own load balancer might cost less initially, using ELB saves significant effort as AWS handles the operational overhead, resulting in potential long-term cost savings.

+ Integration with AWS Services: ELB seamlessly integrates with various AWS offerings and services such as EC2, EC2 Auto Scaling Groups, Amazon ECS, AWS Certificate Manager (ACM), CloudWatch, Route 53, AWS WAF (Web Application Firewall), and AWS Global Accelerator, simplifying the setup and management of complex architectures.


<img src='images/load balancer security group.png' height='100%' width='100%' >

#### Health Checks
+  Health Checks are crucial for Load Balancers
+ They enable the load balancer to know if instances it forwards traffic to 
are available to reply to requests
+ The health check is done on a port and a route (/health is common)
+ If the response is not 200 (OK), then the instance is unhealthy

#### Types of Load Balancer
1. Classic Load Balancer (CLB) (vI-old generation)-2009:
+ External (Public) CLB: Routes incoming traffic from the internet to the instances in your VPC. It has a public DNS name and public IP addresses.

+ Internal (Private) CLB: Routes traffic between the instances within the same VPC. It does not have a public DNS name or public IP addresses and is accessible only within the VPC.

2. Application Load Balancer (ALB)  (v2 - new generation) – 2016:
+ External (Public) ALB: Distributes incoming web traffic across multiple targets in multiple availability zones. It has a public DNS name and public IP addresses.

+ Internal (Private) ALB: Distributes traffic to targets within the same VPC, making it ideal for internal services. It does not have a public DNS name or public IP addresses.

+ Layer 7 (HTTP) Load Balancing: ALBs operate at the application layer (Layer 7) of the OSI model, enabling them to intelligently distribute incoming HTTP and HTTPS traffic to backend targets.

+ Load Balancing to Multiple HTTP Applications Across Machines (Target Groups): ALBs support routing traffic to multiple target groups, allowing you to direct requests to different sets of instances based on defined criteria, such as path patterns or hostnames.

+ Load Balancing to Multiple Applications on the Same Machine (e.g., Containers): ALBs can efficiently balance traffic to multiple applications running on the same instance, making them suitable for containerized environments where multiple services may coexist on a single host.

+ Support for HTTP/2 and WebSocket: ALBs offer native support for HTTP/2, enabling faster and more efficient communication between clients and servers. Additionally, they can handle WebSocket traffic, which is crucial for real-time communication applications like chat applications or online gaming.

+ Support for Redirects: ALBs can be configured to perform redirects, allowing you to seamlessly redirect HTTP requests to HTTPS for improved security or to different URLs as needed. This feature is particularly useful for enforcing HTTPS for secure communication between clients and servers.

Certainly! Application Load Balancers (ALBs) offer advanced routing capabilities that make them an ideal choice for modern microservices and container-based applications. Here's a detailed explanation:
1. Routing Tables to Different Target Groups:
    + ALBs support routing traffic to different target groups based on various criteria, including URL path, hostname, query strings, and headers. This allows for fine-grained control over how incoming requests are distributed to backend services.

2. Routing Based on Path in URL:
    + ALBs can route requests based on the path specified in the URL. For example, requests to "example.com/users" can be directed to one target group handling user-related services, while requests to "example.com/posts" can be routed to another target group handling post-related services.

3. Routing Based on Hostname in URL:
    + ALBs can also route requests based on the hostname specified in the URL. For instance, requests to "one.example.com" can be sent to one target group, while requests to "other.example.com" can be directed to a different target group, allowing for segregation of services based on subdomains.

4. Routing Based on Query String, Headers:
    ALBs support routing based on query string parameters and headers in the HTTP request. This enables dynamic routing decisions based on specific parameters or headers, such as user IDs, authentication tokens, or content types.

5. Suitability for Microservices & Container-Based Applications:    
    + ALBs are well-suited for microservices and container-based architectures due to their flexible routing capabilities and seamless integration with container orchestration platforms like Docker and Amazon ECS. They can efficiently distribute traffic across multiple containers or microservices running on different instances or tasks.

6. Port Mapping Feature for ECS:

    + ALBs offer a port mapping feature specifically designed for Amazon ECS, allowing containers within ECS tasks to dynamically bind to different ports. This eliminates the need to manage port conflicts manually and simplifies the deployment of containerized applications.

7. Comparison with Classic Load Balancers (CLBs):
    + In contrast to ALBs, which support multiple routing criteria and flexible target group configurations, CLBs are limited in their routing capabilities. To achieve similar functionality as ALBs, multiple CLBs would be required per application, leading to increased complexity and management overhead.

    <img src='images/ALB.png' height='100%' width='100%' >

3. Network Load Balancer (NLB) (v2 - new generation) – 2017:
+ External (Public) NLB: Routes TCP, TLS, and UDP traffic from clients over the internet to a target, typically an instance in a VPC. It has a public IP address.

+ Internal (Private) NLB: Routes traffic to targets within the same VPC, often used for internal-facing services. It does not have a public IP address.

4. Gateway Load Balancer (GWLB)-2020:
+ External (Public) GWLB: Routes traffic at the network layer (Layer 3) and operates with public IP addresses to direct traffic from clients over the internet to targets within a VPC.

+ Internal (Private) GWLB: Operates within the VPC and directs traffic internally, usually between services or instances within the same VPC. It does not have public IP addresses.

#### Application Load Balancer (v2)
