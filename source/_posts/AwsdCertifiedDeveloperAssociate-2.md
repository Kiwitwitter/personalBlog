---
title: Aws Certified Developer Associate, EC2 Storages
date: 2020-08-23 20:30:56
tags:
- study
- aws_certified_developer_associate
---

## Elastic Block Store

A EC2 machine loses its root volume (main drive) when it is mannually terminated, and unexpected terminations might happen from time to time. So sometimes, you need a way to store your instance data somewhere. 

An EBS (Elastic Block Store) Volume is a network drive that you can attach to your instances while they run, and it allows your instances to persist data.

### EBS Volume

* It's a network drive (not a physical drive)
  * It uses the network to communicate the instance, which means there might be a bit of latency
  * It can be detached from an EC2 insatnce and attached to another one quickly in the same AZ
* It's locked to an Availability Zone (AZ)
  * To move a volumne across, you need to snapshot it
* Have a provisioned capacity (size in GBs and IOPS)
  * You get billed for all the provisioned capacity
  * You can increase the capacity of the drive over time

### EBS Volume Types

* EBS volumes come in 4 types:
  1. GP2 (SSD): general SSD balances price and performance for a variety of workloads
  2. IO1 (SSD): Highest-performance SSD volume for mission-critical  low latency or high-throughput workloads
  3. ST1 (HDD): Low cost HDD volume designed for frequently accessed, throughput-intensive workloads
  4. SC1 (HDD): Lowest cost HDD volume designed for less frequently accessed workloads
* EBS Volumes are characterized in Size| Throughput| IOPS (I/O Per Sec)
* When in doubt, always consult the AWS documentation.
* Only GP2 and IO1 can be used as boot volumes

### EBS Volume Types Use cases

1. GP2

   * Recommended for most workloads
   * System boot volumes
   * Virtual desktops
   * Low-latency interactive apps
   * Developemtn and test environments
   * Volume ranges from 1 GiB to 16 TiB, Max IOPS is 16,000.
   * Small GP2 volumes can burst IOPS to 3000, 3 IOPS/GiB, means that at 5,334GB, we are at the max IOPS

2. IO1

   * Critical business applications that require sustained IOPS performance, or more than 16,000 IOPS per volume (gp2 limit)

   * Large database workloads, such as:

     Mongoldb, cassandra, Microsoft SQL Server, MySQL, PostgreSQL, Oracle

   * Volume ranges from 4 GiB to 16 TiB

   * IOPS is provisioned, MIN 100 - MAX 64,000 (Nitro instance), else MAX 32,000 (other instance)

   * The maximum ratio of provisioned IOPS to requested volume size (in GiB) is 50:1

3. ST1

   * Streaming workloads requiring consistent, fast throughput at a low price
   * Big data, Data warehouses, Log processing
   * Apache Kafka
   * Cannot be a boot volume
   * Volume ranges from 500 GiB - 16TiB
   * Max IOPS is 500
   * Max throughput of 500 MiB/s - can burst

4. SC1

   * Throughput-oriented storage for large volumes of data that is infrequently accessed
   * Scenarios where the lowest storage cost is important
   * Cannot be a boot volume
   * Volume ranges from 500 GiB to 16 TiB
   * Max IOPS is 250
   * Max throughput of 250 MiB/s - can burst

### EBS vs Instance Store

* Instance Store Pros:
  * Better I/O performance
  * Good for buffer / cache/ scratch data/ temporary content
  * Data survives reboots
* Instance Store Cons:
  * On stop or termination, the instance store is lost
  * You can't resize the instance store
  * Backups must be operated by the user

## Elastic File System

* Managed NFS (Network File System) that can be mounted on many EC2s, which means all EC2 attached to it have access to it
* EFS works with EC2 instances in multi-AZs
* High available, scalable, expensive (3 * gp2), pay per use
* Use cases: content management, web serving, data sharing, Wordpress
* Use NFSv4.I protocol
* Use security groupn to control access to EFS
* **Compatible with Linux based AMI only**
* Encryption at rest using KMS
* POSIX file system (~Linux) that has a standard file API
* File system scales automatically, pay per use, no capacity planning

## EFS - Performance and Storage Classes

* EFS Scale:
  * 1000s of concurrent NFS clients, 10 GB+/s throughtput
  * Grow to Petabyte-scale NFS, automatically
* Performance Mode (Set at EFS creation time):
  * General purpose(default): latency-sensitive use cases(web server, CMS, etc..)
  * Max I/O - higher latency, throughtput, highly parallel
* Stoage Tiers (lifecycle management feature – move file after N days):
  * Standard: for frequently accessed files
  * Infrequent access (EFS-IA): cost to retrieve files, lower price to store

## EBS vs EFS

| EBS                                                          | EFS                                                   |
| ------------------------------------------------------------ | ----------------------------------------------------- |
| can be attached to only one instance at a time<br />are locked at the Availability Zone (AZ) level | Mounting 100s of instances across AZ                  |
| gp2: IO increases if the disk size increases<br />io1: can increase IO independently | 1000s of concurrent NFS clients, 10 GB+/s throughtput |

### EBS:

* To migrate an EBS volume across AZ
  1. Take a snapshot
  2. Restore the snapshot to another AZ
  3. EBS backups use IO and you shouldn’t run them while your application is handling a lot of traffic
* Root EBS Volumes of instances get terminated by default if the EC2 instance gets terminated. (you can disable that)

### EFS:

* Only for Linux Instances (POSIX)
* EFS has a higher price point than EBS
* Can leverage EFS-IA for cost savings