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