---
title: AWS Cloud Practitioner, Core Serviceds
date: 2020-01-02 22:45:06
tags:
- study
- aws_cloud_practitioner
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

* Regions are geographical zones that holds more than 2 availability zones, and are the organizing level for AWS services
* You need to pick the region where those resources are located for lower latency and minimizing costs and adhering regulatory requirements
* Services can be deployed in multi-regions that best suit the business's needs
* Regions are completely separate entities from one another, resources in one region are not automatically replicated to another region, though some of the most common services are available in all regions

### Availability Zones

* Availabilty Zones are a collection of data centers within a specific region.
* Each availability zone is physically isolated from the others, but connected together by a fast, low latency network
* Each availability zone is a physically distinct, independent infrastructure, physically and logically independent
* They also have their own discrete, uninterruptable power supply; onsite backup generators, cooling equipments and network connectivity
* Isolating the availability zone means they are protected from failures in other zones, which ensures high availability 
* Data redundancy within a region means that if one zone goes down, the other zones can handle requests, that's why AWS recommends provisioning your data across multiple Availability Zones as a best practice

### Edge Locations

* Edge locations host a content delivery network, in short CDN, in Amazon CloudFront. CDN is used to deliver content to your customers , requests for content will be automatically routed to the nearest edge location so that the content is delivered faster to the end uses
* Edge Locations are typically located in highly poplated areas

## Amazon Virtual Private Cloud (VPC)

### Introduction

The resources and services must be accessible via normal IP protocols implemented with familiar network structures. Customers need to adhere to networking best practices as well as meet regularity and organizational requirement. Amazon Virtual Private Cloud, aka VPC meets all the network requirements.

* A private, virtual network in the AWS Cloud
  * Uses same concepts as on premise networking, like IP address spaces, subnets, and routing tables
* Allows complete control of network configuration
  * Ability to isolate and expose resources inside VPC
* Offeres several layers of security controls
  * Ability to allow and deny specific internet and internal traffic
* Other AWS services deploy into VPC
  * Services inherent security built into network, integrated with numerous AWS services

### Features

* Builds upon high availability of AWS Regions and Availability zones

  * VPC lives within a Region
  * Multiple VPCs per accuount

* Subnets

  * Used to divide Amazon VPC
  * Allows VPC to span multiple AZs
  * You can create unlimited subnets, but the fewer is recommended to reduce the complexity

* Route tables

  * Control traffic going out of the subnets

* Internet Gateway (IGW)

  * Subnets can be public or priavte, public goes to internet, private doesn't go to internet

  * Allows access to the Internet from VPC

* NAT Gateway

  * Allows private subnet resources to access Internet

* Network Access Control Lists (NACL)

  * Control access to subnets, stateless

### Example

1. Select Region
2. Create the VPC, define IP Address space for the VPC
3. Create subnets, specify the AZ of the subnet
4. Add Internet Gateway
5. Configure the acesss

## AWS Security Groups

At AWS, security groups will act like a built-in firewall for virtual servers. With these security groups, you have full control on how accessible your instances are. In another word, it is just another method to filter traffic to your instances, provides you control on what traffic to allow or deny. To do this, you need to configure a security group rule , that can vary from keeping instance completely private, totally public, or somewhere between.

