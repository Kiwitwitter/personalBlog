---
title: AWS Cloud Practitioner, Core Serviceds
date: 2020-01-02 22:45:06
tags:
- study
- aws
---

## Amazon Elastic Cloud Compute (EC2)

### Overview

* EC2 = Elastic Compute Cloud
* Can be used to do many things, including but not limited to Application Server, Web Server, Database Server, Game Server, Mail Server, etc.
* Elastic refers to the fact that if properly configured, you can increase and decrease the amount of servers required by application automatically according to the current demands on that application
* We call them instances instead of servers
* Characters:
  * Pay as you go
  * Broad selection of Hardware and Software
  * Global hosting
  * more on [aws.amazon.com/ec2](aws.amazon.com/ec2)

### Build And Configure EC2 Instance

1. Login to AWS Console
2. Choose a region
3. Launch EC2 Wizard
4. Select Amazon Machine Inage (AMI, Software)
5. Select Instance Type (Hardware)
6. Configure network
7. Configure storage
8. Configure key pairs (in order to ssh into this host)
9. Launch and Connect



## Amazon Elastic Block Store (EBS)

### Overview

* EBS Volumes are used for storage
* Can choose between HDD and SSD types
* Persistent and customizable black storage for EC2 instances
* Designed for being durable and available, which means that the data in a volume is automatically replicated across multiple servers
* Backup using Snapshots, also can recover using Snapshots, share Snapshots across Availability Zones
* Easy and transparent Encryption on EC2 side
* Elastic Volumes, can increase volume or even change type of storage

### Create and Attach EBS to EC2 Instance

1. Login to AWS Console
2. Go to "EC2" Console
3. Go to "Elastic Block Store" sidebar, and select "Volumes"
4. EBS must be created in the same Availability Zone with EC2 Instance to be attched to
5. "Create Volume" and select "Volume Type", specify "Size"
6. Select correct "Availibity Zone" and Create the Volume
7. Select the newly created Volume in the Volume console, Select "Attach Volume" in the "Actions" list
8. Enter the Instance and Device and Attach it
9. ssh into the EC2 Instance, and use ```$ lsblk``` to check the attached volume
10. Create file system using ```$ mke2fs file_system_folder```
11. Mount file system using ```$mount file_system_folder mount_folder``

## Amazon Simple Storage Service (S3)

### Overview

* Fully managed cloud storage service
* Store virtually unlimited number of objects
* Acces anytime, from anywhere
* Rich security controls

### Knowledge

* When user put a object into the S3 bucket, it's associated with a particular AWS region
* Whenever an object is stored in a bucket, it redundantly store across multiple AWS facilities within the selected region
* S3 will also scale to handle high volume of request, and user only be billed for what the user used
* Objects can be accessed from **AWS Management Console**, **AWS CLI**, **AWS SDK**, additionally can be accessed from any RESTful Endpoint what support HTTP and HTTPS
* URL Access: ```https://awsexamplebucket/s3-us-west-2.amazonaws.com/docs/hello.txt```, to support URL access, S3 bucket names must be globally unique and DNS compliant, and object-keys should be characters that are safe for URLs

### Common Use Cases

1. Storing Application Assets
2. Static Web Hosting
3. Backup & Disaster recover
4. Staging area for Big Data
5. etc.



## AWS Global Infrastructure

### Overview

* Regions
* Availability Zones
* Edge Locations

### Regions

(To be continued...)