
# Mounting Aws EFS on Multiple EC2 Instances

Instructions to mount an Amazon Elastic File System (EFS) on multiple EC2 instances. This setup allows to share the same file system across different servers, ensuring consistency and easy access to shared data.



## Steps involved: 

1) Create three EC2 instances with different security groups and subnet zones. For example within the Mumbai region (ap-south-1), with each instance placed in a different availability zone, such as ap-south-1a, ap-south-1b, and ap-south-1c.

2) Create a new security group:
- Set the type to NFS
- Attach the security group id of all the 3 EC2 instances to inbound rules.
- save.








![App Screenshot](https://github.com/Glycine26/aws-efs-setup/blob/dc80441fef7d8d0db1be919ac1a7bbd29cd405b7/img/inbound_rules.PNG?raw=true)


3) Create a new Elastic File System (EFS) and attach the security group (created in previous step) to all the Availability zone.
![App Screenshot](https://github.com/Glycine26/aws-efs-setup/blob/main/img/mount%20target%20sg.PNG?raw=true)
3) Create a new Elastic File System (EFS) and attach the security group (created in previous step) to all the Availability zone.


4. Connect to Each EC2 Instance:

5. Switch to the root user.
```bash
  sudo su
```
6. Install the Amazon EFS utils package:

   Install the Amazon EFS Utils package, which includes the efs mount helper. This simplifies the process of mounting EFS.
```bash
  yum install -y amazon-efs-utils
```
7. Create a directory for the Mount Point:
```bash
  mkdir -p /mnt/efs/fs1
```
8. Mount the EFS file system:
```bash
  sudo mount -t efs File system ID:/ /mnt/efs/fs1
```
9. Verify the mount
To verify that the EFS is successfully mounted, use the df -h command:
```bash
  df -h
```
![App Screenshot](https://github.com/Glycine26/aws-efs-setup/blob/main/img/mount%20point.PNG?raw=true)

Now the files stored in the EFS become accessible from any of these 3 instances. This means we can read, write, and manage files from any EC2 instance that is connected to the EFS, making it a shared storage solution across multiple instances.