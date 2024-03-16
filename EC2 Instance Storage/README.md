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
+ Click on Instance-> storage tab on bottom-> you can see volume->click on volume(to see detail)
+ In left side click volumes->create volume(from right side)->volume type(General purpose ssd)->AZs:eu-west-1b because previous volume has also same->refresh->we can see detail nd see it is available->action:attach volume->instance: ......that we already have of same AZs-> click attach volume
+ storage->block devices(we have 2 block devices)
+ again create volume for different AZs let say eu-west-1a -> create volume-> action->attach volume: we cannot tach because  we don't have instance for new AZs we have created this time.
+ Accessing the Storage Tab:

    + Navigate to the "Instance" dashboard.
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