# AWS EBS Volume Management

## Project Overview
This lab demonstrates how to manage Amazon Elastic Block Store (EBS) volumes with Amazon EC2.

The objective is to create an EBS volume, attach it to an EC2 instance, configure a Linux file system, create a snapshot backup, and restore deleted data from that snapshot.

## AWS Services Used
- Amazon EC2
- Amazon EBS
- EBS Snapshots
- AWS Systems Manager Session Manager

## Tasks Performed

### 1. Create EBS Volume
- Created a new 1 GiB EBS volume.
- Selected General Purpose SSD (gp2).
- Used the same Availability Zone as the EC2 instance.
- Named the volume `My Volume`.

### 2. Attach EBS Volume
- Attached the volume to the EC2 instance named `Lab`.
- Selected `/dev/sdb` as the requested device name.

### 3. Configure File System
- Connected to EC2 using Session Manager.
- Created an ext3 file system.
- Created `/mnt/data-store`.
- Mounted the EBS volume.
- Added a mount entry to `/etc/fstab`.

### 4. Create and Verify a File
- Created `file.txt` on the mounted volume.
- Verified its content using Linux commands.

### 5. Create EBS Snapshot
- Created a snapshot named `My Snapshot`.
- Waited for the snapshot status to become `Completed`.
- Deleted the original file to test data recovery.

### 6. Restore Snapshot
- Created a new EBS volume from the snapshot.
- Named it `Restored Volume`.
- Attached it to the EC2 instance.
- Mounted it at `/mnt/data-store2`.
- Verified that `file.txt` was recovered.

## Linux Commands Used

```bash
df -h
sudo mkfs -t ext3 /dev/sdb
sudo mkdir /mnt/data-store
sudo mount /dev/sdb /mnt/data-store
cat /etc/fstab
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
cat /mnt/data-store/file.txt
sudo rm /mnt/data-store/file.txt
ls /mnt/data-store/
sudo mkdir /mnt/data-store2
sudo mount /dev/sdc /mnt/data-store2
ls /mnt/data-store2/
cat /mnt/data-store2/file.txt
```

> Note: Linux device names can differ from the requested EC2 device names. Use `lsblk` to identify the actual device before formatting or mounting it. Never format the root disk.

## Screenshots
Add your lab screenshots to the `screenshots/` folder. Suggested evidence:
1. EC2 instance details and Availability Zone
2. `My Volume` (1 GiB)
3. Attached volume (`In-use`)
4. File system and mount verification (`df -h`)
5. Original `file.txt` content
6. `My Snapshot` (`Completed`)
7. Original file deleted
8. `Restored Volume` (`In-use`)
9. Restored `file.txt` content
10. Lab grades / submission report

## Key Learning Outcomes
- Understanding EBS persistent block storage.
- Creating and attaching EBS volumes to EC2 instances.
- Formatting and mounting Linux file systems.
- Configuring mounts with `/etc/fstab`.
- Creating EBS snapshots for backup.
- Restoring data from snapshots.

## Conclusion
Completed a hands-on AWS EBS lab covering volume creation, attachment, Linux file system configuration, snapshot backup, and data restoration.
