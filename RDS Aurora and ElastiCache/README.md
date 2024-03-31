#### RDS, Aurora & ElastiCache

##### Amazon RDS Overview 
+  RDS stands for Relational Database Service
+  It’s a managed DB service for DB use SQL as a query language. 
+  It allows you to create databases in the cloud that are managed by AWS
    +  Postgres
    +  MySQL
    +  MariaDB
    +  Oracle
    +  Microsoft SQL Server
    +  IBM DB2
    +  Aurora (AWS Proprietary database)

##### Advantage over using RDS versus deploying DB on EC2
+  RDS is a managed service:
+  Automated provisioning, OS patching
+  Continuous backups and restore to specific timestamp (Point in Time Restore)!
+  Monitoring dashboards
+  Read replicas for improved read performance
+  Multi AZ setup for DR (Disaster Recovery)
+  Maintenance windows for upgrades
+  Scaling capability (vertical and horizontal)
+  Storage backed by EBS (gp2 or io1)
+  BUT you can’t SSH into your instances


##### RDS-Storage Auto Scaling
+ Dynamic Scaling: Storage Auto Scaling allows you to increase the storage capacity of your RDS DB instance dynamically, without manual intervention.

+ Automatic Scaling: When RDS detects that you are running out of free database storage, it automatically scales the storage capacity for you.

+ Avoid Manual Scaling: With Storage Auto Scaling, you can avoid the manual effort of monitoring storage usage and scaling your database storage.

+ Configuration: To use Storage Auto Scaling, you need to set a Maximum Storage Threshold, which defines the maximum limit for the DB storage.

+ Automatic Adjustment Conditions: Storage Auto Scaling will automatically modify storage if certain conditions are met, such as when free storage is less than 10% of allocated storage, low storage conditions persist for at least 5 minutes, or 6 hours have passed since the last modification.

+ Use Cases: This feature is particularly useful for applications with unpredictable workloads where storage requirements may fluctuate over time.

+ Compatibility: Storage Auto Scaling is supported across all RDS database engine types, including MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Amazon Aurora.

##### RDS Read Replicas for read scalability
+ RDS Read Replicas for read scalability: Read Replicas in Amazon RDS (Relational Database Service) are copies of your primary database instance that allow you to offload read queries from your primary database. By distributing read traffic across multiple replicas, you can improve the read scalability of your application.

+ RDS DB instance: This refers to your primary RDS database instance, which handles both read and write operations.

+ RDS DB instance read replica: These are additional instances created from your primary RDS instance specifically for handling read queries. They replicate data from the primary instance asynchronously.

+ Application writes reads reads reads: This indicates that while the application is performing write operations (such as INSERT, UPDATE, DELETE), it's also performing multiple read operations.

+ ASYNC replication: Replication between the primary RDS instance and its read replicas is asynchronous. This means that changes made on the primary instance are not immediately reflected on the replicas. There might be a slight delay, so the read replicas are eventually consistent with the primary instance.

+ Up to 15 Read Replicas: Amazon RDS allows you to create up to 15 read replicas for a given primary database instance.

+ Within AZ, Cross AZ, or Cross Region: Read replicas can be created within the same Availability Zone (AZ) as the primary instance, in a different AZ within the same region, or even in a different region altogether for disaster recovery or geographical distribution purposes.

+ Replicas can be promoted to their own DB: If needed, a read replica can be promoted to become its own standalone database instance. This can be useful for scenarios such as scaling out or performing maintenance on the primary instance.

+ Applications must update the connection string to leverage read replicas: In order to take advantage of read replicas, the application must be configured to distribute read queries across both the primary instance and its read replicas. This typically involves updating the connection string used by the application to include information about the read replicas.

Overall, utilizing read replicas in Amazon RDS can significantly improve the scalability, availability, and performance of your application's read operations, while also providing options for disaster recovery and maintenance.

<img src='images/read replicas.png' height='100%' width='100%' > 

##### RDS Read Replicas Use Cases:
+ Production database handling normal load: You have a primary database instance in production that is currently managing the regular workload of your application.

+ Running a reporting application for analytics: You have a reporting or analytics application that needs to run complex queries and analytics tasks on the data in your database. These queries might be resource-intensive and could potentially impact the performance of your production application if run directly on the primary database instance.

+ Creating a Read Replica for the new workload: To offload the analytics workload from the primary instance and ensure that it doesn't affect the performance of your production application, you create a Read Replica of the primary database instance.

+ Production application remains unaffected: By directing the analytics workload to the Read Replica, you ensure that your production application continues to operate smoothly without any degradation in performance. The Read Replica handles the analytics queries separately, without impacting the primary instance.

+ Read replicas used for SELECT (read-only) statements: Read replicas are ideal for scenarios where you primarily need to perform read operations (SELECT statements) rather than write operations (INSERT, UPDATE, DELETE). In this use case, the reporting or analytics application likely only needs to read data from the database to generate reports or perform analysis, so utilizing a Read Replica is a suitable choice.

<img src='images/replica usecase.png' height='100%' width='100%' > 

##### RDS Read Replicas – Network Cost 
+ Network Cost Between AZs: Amazon Web Services (AWS) charges for data transfer between Availability Zones (AZs) within the same region. Whenever data moves from one AZ to another within the same region, there may be associated network costs.

+ RDS Read Replicas Within the Same Region: When you set up Read Replicas for your RDS instance within the same region, you typically don't incur additional network costs. This is because data replication between the primary instance and its replicas occurs within the same region and often within the same AZ. Since there's no data transfer between different AZs or regions, there's no additional fee for network data transfer.