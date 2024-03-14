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

+ Snapshot Requirement for Migration: To move an EBS volume across availability zones, it needs to be first snapshot, as it's not directly copied. Then we area able to move a volume across from different AZ