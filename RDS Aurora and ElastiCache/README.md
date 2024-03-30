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

+Compatibility: Storage Auto Scaling is supported across all RDS database engine types, including MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Amazon Aurora.