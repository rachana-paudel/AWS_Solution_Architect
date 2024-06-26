#### EBS( Elastic Block Storage) Volume

+ Network Drive Attachment: EBS volumes can be attached to running EC2 instances as network drives.

+ Single Instance Attachment: Each EBS volume can only be attached to a single EC2 instance at a time, but multiple EBS volumes can be attached to a single instance.

+ Data Persistence(store): EBS allows data to persist even after the termination of the associated EC2 instance.

+ Mounting: EBS volumes can only be mounted(making a file system available for access in a particular location within a directory tree) to one ec2 instance at a time ( at the CCP level)

+ Availability Zone Binding: EBS volumes are bound to specific availability zones within a region.

+ Analogous to Network USB Stick: It is like a network USB stick where we can take from one computer and attach to another computer but it is not a physical usb it is network usb

+ Free Tier Offering: The AWS Free Tier provides 30 GB of free EBS storage of General Purpose SSD or Magnetic types per month.

+ Latency vs. Speed: While there might be some latency in communication between computers, detaching and attaching EBS volumes to different EC2 instances is generally fast.

+ Inability to Attach Across AZs: EBS volumes cannot be attached across different availability zones within a region. for eg: EBS volume in us-east-1a cannot be attached to us-east-1b

+ Snapshot Requirement for Migration: To move an EBS volume across availability zones, it needs to be first snapshot, as it's not directly copied. Then we are able to move a volume across from different AZ

+ You have to provision capacity in advance so you need to say how many GBs you want in advance and the IOPS, which is I/O operation per seconds, and you are basically defining how you want your ebs volume to perform. You get billed for all the provisioned capacity

#### EBS - Delete on termination attribute
+ by default the root EBS volume is deleted(attribute enable)
+ by default any other attached EBS volume is not deleted (attribute is disabled)

<img src='images/termination protection.png' height='100%' width='100%' >  

#### Lab
+ Accessing the Storage Tab:
    + Navigate(move through or interact) to the "Instance" dashboard.
    + Click on the "Storage" tab at the bottom.

+ Viewing Volume Details:
    + Locate the volume you want to view details for and click on it.

+ Creating a Volume:
    + Click on "Volumes" on the left side.
    + Select "Create Volume" from the right side.
    + Specify the volume type, such as "General Purpose SSD."
    + Choose the Availability Zone (AZ), such as "eu-west-1b" to match the previous volume.
    + Click "Refresh" to ensure the volume is available.

+ Attaching the Volume:
    + Under "Actions," select "Attach Volume."
    + Choose the instance to attach the volume to. Ensure it's in the same AZ as the volume.
    + Click "Attach Volume."

+ Viewing Block Devices:
    + Navigate back to the "Storage" tab.
    + Look under "Block Devices" to see the attached volumes.

+ Creating Another Volume for a Different AZ:
    + Repeat the volume creation process, but this time choose a different AZ, like "eu-west-1a."

+  Attempting to Attach the Volume to an Instance:
    + When attempting to attach the newly created volume, you'll find that there are no instances available in the new AZ ("eu-west-1a") because you only have instances in the previous AZ ("eu-west-1b").

+  Availability Check:
    + After attempting to attach the volume to an instance in a different Availability Zone (AZ) and finding it's not available, you decide to delete the volume.

+ Deleting the Volume:
    + Navigate to the volume in question.
    + Choose "Actions."
    + Select "Delete Volume."
    + Confirm the deletion.

+ Updating Block Device Settings:
    + Go to the "Storage" tab.
    + Navigate to "Block Devices."
    + Verify that the first volume has "Delete on Termination" set to "Yes."

+ Changing "Delete on Termination" Setting:
    + To change the "Delete on Termination" setting, go to the "Launch Instance" section.
    + Find the option to configure storage settings.
    + Adjust the setting for the volume to "Delete on Termination: No."

#### EBS Snapshots
+ EBS snapshot is used to make a backup of your EBS volume at a point of time.    
+ snapshot captures the data and configuration of instances
+ It is not necessary to detach a volume to do snapshot but it is recommended.
+ Availability Zones (AZs) are distinct locations within a region, each comprising one or more data centers with independent power, cooling, and networking infrastructure.
+ AWS allows users to copy snapshots of EBS volumes across different AZs within the same region or even across regions.
+ Example: you can use ebs volume to 1 instance and take a snapshot and restore it to another instance of another AZs

#### EBS Snapshots Features
+ EBS Snapshot Archive:
    This feature allows you to store snapshots of your EBS volumes in a long-term, cost-effective manner.

+ Move a Snapshot to an "Archive Tier":
    You can transfer snapshots to a lower-cost storage tier, typically around 75% cheaper than regular storage. This is useful for data that doesn't need to be accessed frequently.

+ Restoration Time:
 Snapshots stored in the archive tier can take between 24 to 72 hours to restore, so it's best suited for data that isn't needed immediately.

+ Recycle Bin for EBS Snapshots:
    You can set up a recycle bin for EBS snapshots, ensuring that deleted snapshots are retained for a specified period before permanent deletion.

+ Retain Deleted Snapshots:
    You can define rules to retain deleted snapshots for a specified duration, ranging from 1 day to 1 year, allowing you to recover them if needed.

+ Fast Snapshot Restore (FSR):
    This feature accelerates the restoration of snapshots by pre-warming the underlying EBS volumes, reducing latency upon first use.

+ Force Full Initialization:
    This ensures that when a snapshot is used for the first time, there's no latency as all necessary data is immediately available but little costly

#### Lab
+ Create Snapshot:
    + Click on "Volume" in the AWS Management Console.
    + Select the desired volume.
    + Choose "Actions" and then "Create Snapshot."
    + Provide a description, such as "demosnapshot," and confirm to + create the snapshot.

+ Copy Snapshot to Another Region:
   +  Navigate to "Snapshots" from the left-side menu.
   +  Right-click on the snapshot you want to copy.
    + Select "Copy Snapshot" and specify the destination region.

+ Create Volume from Snapshot:
    + Navigate to "Snapshots" from the left-side menu.
    + Select the desired snapshot.
    + Choose "Actions" and then "Create Volume from Snapshot."

+ Set Up Retention for Deleted Snapshots:
    + Navigate to "Snapshots" from the left-side menu.
    + Click on "Recycle Bin."
    + Create a retention rule by clicking "Create Retention Rule."
    + Provide a name like "demoretention," select "EBS snapshots" as the resource type, and check "Apply to all resources." Then, + create the retention rule.

+ Manage Snapshots in the Recycle Bin:
    + Navigate to "Snapshots" from the left-side menu.
    + Click on "Recycle Bin" to view deleted snapshots.
    + From here, you can select the deleted snapshot you want to recover and choose "Recover" to restore it.

+ Archive or Delete Snapshots:
    + Navigate to "Snapshots" from the left-side menu.
    + Select the snapshot you want to archive or delete.
    + Choose "Actions" and then either "Archive Snapshot" or "Delete Snapshot" as per your requirement.

+ Access the Recycle Bin:
    + Navigate to "Snapshots" from the left-side menu in the AWS Management Console.
    + Click on "Recycle Bin" to access the list of deleted snapshots.

+ Recover a Deleted Snapshot:
    + In the recycle bin, locate the snapshot you want to recover.
    + Select the deleted snapshot you wish to restore.
    + Choose the "Recover" option. This action will initiate the recovery process for the selected snapshot.

#### AMI(Amazon Machine Image) 
+ Customization: AMIs allow users to customize EC2 instances with their own software, configuration, operating system, and monitoring tools. This customization facilitates the creation of environments tailored to specific requirements.

+ Boot and Configuration Time: AMIs speedup boot and configuration processes because all necessary software is pre-packaged within the image. This streamlines the setup of new instances and reduces deployment time.

+ Region Specificity: AMIs are built for a specific AWS region. However, they can be copied across regions, enabling deployment in multiple geographic locations to meet global needs.

+ Launch Options: Users can launch EC2 instances from various types of AMIs:

    + Public AMIs: Provided by AWS, these offer a range of pre-configured environments and operating systems.
    + Custom AMIs: Users create and maintain these images themselves, tailoring them to their specific applications and requirements.
    + AWS Marketplace AMIs: Offered by third-party vendors, these AMIs provide pre-configured solutions for various purposes, potentially including paid offerings.

#### AMI Process
+ Start an EC2 instance and customize it
+ Stop the instance (for data integrity)
+ Build an AMI – this will also create EBS snapshots
+ Launch instances from other AMIs
+ We can create AMI customize it and launch to another AZ from AMI 

#### Lab
+ After creating an instance -> right click on instance-> create image-> image name :Demoimage->create image
+ click on AMi from left side, Demoimage is registered
+ We can now launch instances from the AMI or direct from instance
+ launch instance -> instance name :from AMI -> Application and OS image(AMI): My AMIs: owned by me-> AMI :Demoimage-> perform other operation like selection or edit of network, user data etc. -> launch instance

#### EC2 Instance Store
+ EBS volumes offer good but "limited" performance as network drives.
+ For high-performance hardware disk needs, EC2 Instance Store is recommended due to better I/O performance.
+ EC2 Instance Store disks are ephemeral, meaning they lose their data if the instance is stopped or terminated.
+ They are suitable for buffer, cache, scratch data, or temporary storage purposes.
+ Ideal for scenarios where data persistence isn't critical and fast I/O capabilities are required for efficient handling of temporary workloads or large data volumes within a single session.

#### EBS Volume types
1. General Purpose SSD (gp2/gp3):
Use Cases:
+ Cost-effective storage with low-latency requirements.
+ Suitable for system boot volumes, virtual desktops, development, and test environments.
+ Volume Range: 1 GiB - 16 TiB.
+ gp3 Characteristics:
    + Baseline of 3,000 IOPS and throughput of 125 MiB/s.
    + Can independently increase IOPS up to 16,000 and throughput up to 1000 MiB/s.
+ gp2 Characteristics:
    + Small gp2 volumes can burst IOPS to 3,000.
    + IOPS are linked to the size of the volume, with a maximum of 16,000 IOPS.
    + Follows the 3 IOPS per GB rule, reaching max IOPS at 5,334 GB.

2. Provisioned IOPS (PIOPS) SSD (io1/io2):
Use Cases:
+ Critical business applications requiring sustained IOPS performance or needing more than 16,000 IOPS.
+ Ideal for database workloads sensitive to storage performance and consistency.
+ Volume Range: 4 GiB - 16 TiB for io1, 4 GiB - 64 TiB for io2 Block Express.
+ io1 Characteristics:
    + Max PIOPS of 64,000 for Nitro EC2 instances & 32,000 for others.
    + PIOPS can be increased independently from storage size.
+ io2 Block Express Characteristics:
    + uSb-millisecond latency.
    + Max PIOPS of 256,000 with an IOPS:GiB ratio of 1,000:1.
    + Supports EBS Multi-attach.

3. Hard Disk Drives (HDD) (st1/sc1):
Use Cases:
+ Throughput Optimized HDD (st1): Suitable for big data, data warehouses, log processing where high throughput is crucial.
+ Cold HDD (sc1): For infrequently accessed data or scenarios prioritizing cost-effectiveness.
+ Volume Range: 125 GiB to 16 TiB for both st1 and sc1.
+ Throughput Optimized HDD (st1) Characteristics:
    + Max throughput of 500 MiB/s and max IOPS of 500.
+ Cold HDD (sc1) Characteristics:
    + Max throughput of 250 MiB/s and max IOPS of 250.    

#### EBS Multi-Attach – io1/io2 family
+ Attach the same EBS volume to multiple EC2 
instances in the same AZ
+ Each instance has full read & write permissions 
to the high-performance volume
+ Use case:
+ Achieve higher application availability in clustered 
Linux applications (ex: Teradata)
+ Applications must manage concurrent write 
operations
+ Up to 16 EC2 Instances at a time
+ Must use a file system that’s cluster-aware (not 
XFS, EXT4, etc…)    

#### EBS Encryption
+  When you create an encrypted EBS volume, you get the following:
+  Data at rest is encrypted inside the volume
+  All the data in flight moving between the instance and the volume is encrypted
+  All snapshots are encrypted
+  All volumes created from the snapshot
+  Encryption and decryption are handled transparently (you have nothing to 
do)
+  Encryption has a minimal impact on latency
+  EBS Encryption leverages keys from KMS (AES-256)
+  Copying an unencrypted snapshot allows encryption
+  Snapshots of encrypted volumes are encrypted

#### Lab
+ create volume -> fill other detail like Gb of storage and AZ -> Encryption: Check on encrypt this volume -> create volume ( encryption is not shown in detail)
+ action-> create snapshot -> again the no encryption so -> action: copy snapshot -> write description, region and check on encrypt this snapshot-> click on copy snapshots 
+ from this snapshot we can create volume -> action : create volume from snapshot -> create volume
+ delete volume and snapshot 

#### Managed NFS: 
+ Managed NFS (network file system) that can be mounted on many EC2
+ EFS works with EC2 instances in multi-AZ
+ Highly available, scalable, expensive (3x gp2), pay per us

<img src='images/efs file system.png' height='100%' width='100%' >  

#### Use cases: 
+ content management, web serving, data sharing, Wordpress
+ Uses NFSv4.1 protocol
+ Uses security group to control access to EFS
+ Compatible with Linux based AMI (not Windows)
+ Encryption at rest using KMS
+ POSIX file system (~Linux) that has a standard file API
+ File system scales automatically, pay-per-use, no capacity planning

#### EFS -Performance and Storage Classes
+ EFS Scale:
    + Amazon EFS is designed to scale seamlessly to accommodate thousands of concurrent NFS clients and support throughput of over 10 GB/s. It can grow to petabyte-scale network file systems automatically, providing high scalability and performance for large-scale workloads.

+ Performance Mode:
    Performance mode is set at the time of EFS creation and determines how the file system prioritizes latency and throughput.

+ General Purpose (Default): 
    + Suitable for latency-sensitive use cases such as web servers and content management systems (CMS). It provides balanced performance for a wide range of workloads.

+ Max I/O: 
    Optimized for high throughput and parallel access, making it suitable for big data processing and media processing workloads. This mode may have higher latency compared to the General Purpose mode.

+ Throughput Mode:
    Throughput mode defines how the file system's throughput scales based on the amount of data stored and accessed.

+ Bursting: 
    Provides a baseline throughput of 50 MiB/s per TB of storage, with the ability to burst up to 100 MiB/s. Bursting mode is suitable for workloads with sporadic or variable access patterns.

+ Provisioned: 
    Allows you to set a specific throughput regardless of the storage size. For example, you can provision 1 GiB/s throughput for 1 TB of storage. This mode is beneficial for workloads that require consistent throughput.

+ Elastic: 
    Automatically scales throughput up or down based on workload demands. It can provide up to 3 GiB/s for reads and 1 GiB/s for writes, making it suitable for unpredictable workloads with fluctuating performance requirements.

#### Standard Tier:

+ Suitable for frequently accessed files.
    + Offers high availability and durability across multiple 
    + Availability Zones.
+ Infrequent Access (EFS-IA) Tier:
    + Designed for less frequently accessed files.
    + Lower storage costs but incurs retrieval costs.
    + Enabled via a Lifecycle Policy to automatically move files after a set period of inactivity.
+ Availability and Durability:
    + Standard Tier: Multi-AZ redundancy for production workloads.
    + One Zone: Single AZ storage suitable for development, with backup enabled by default.
+ Cost Savings:
    + Over 90% savings possible by utilizing storage tiers and appropriate availability options.
    + EFS-IA and One Zone options help optimize costs while maintaining data availability and durability.

#### Lab
+ firstly create a ec2 and security group inside it named : sg-ef-demo-> description : EFS Demo SG ->create security group-> security group name : efs-demo ->create security group
+ create EFS -> click on customize -> AZ: regional ->  enable automatic backups -> throughput mode : enhanced -> elastic is recommended -> next -> network : VPC -> mount target : efs-demo -> next -> File system policy : it is optional -> next -> create-> click on EFS we created 
+ launch instance -> name Instance A-> configure storage : o x file system : edit -> it ask to create subnet so create it from above ->launch instance -> launch another instance : Instance B 
+ search instance state :running -> go to security group in left -> inbound rule : security group is attached
+ click on 1 instance : connect -> ec2 instance connect







    