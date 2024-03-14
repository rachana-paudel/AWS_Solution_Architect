#### EBS( Elastic Block Storage) Volume
+ It is an network drive that we can attach to our instance while they run
+ we cannot attach 1 EBS to 2 or more EC2 instance but we can attach 2 or more EBS to a single instance
+ EBS allows us to store(persist) data even after the termination of ec2 instance
+ They can only be mounted(making a file system available for access in a particular location within a directory tree) to one ec2 instance at a time ( at the CCP level)
+ They are bound to specific availability zone
+ It is like a network USB stick where we can take from one computer and attach to another computer but it is not a physical usb it is network usb
+ Free tier provide 30 GB of free EBS storage of type General purpose SSD or magnetic per month
+ I might be a bit of latency to communicate between two computer but the speed is high to detach from an ec2 instance and attached to another one