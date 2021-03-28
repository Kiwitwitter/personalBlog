title: AWS Fundamentals, RDS + Aurora + ElatiCache
date: 2021-03-27 18:44:20
tags:
- study
- aws_certified_developer_associate

## Amazon RDS

### Overview

* RDS stands for Relational Database Service

* It’s a managed DB service for DB use SQL as a query language.

* It allows you to create databases in the cloud that are managed by AWS

  • Postgres

  • MySQL

  • MariaDB

  • Oracle

  • Microsoft SQL Server

  • Aurora (AWS Proprietary database)

### Advantage over using RDS vs Deploying DB on EC2

* RDS is **Managed** service, which means you cannot SSH into your instances

  • Automated provisioning, OS patching

  • Continuous backups and restore to specific timestamp (Point in Time Restore)!

  • Monitoring dashboards

  • Read replicas for improved read performance

  • Multi AZ setup for DR (Disaster Recovery)

  • Maintenance windows for upgrades

  • Scaling capability (vertical and horizontal)

  • Storage backed by EBS (gp2 or io1)

### RDS backups

* Automated backups:
  * Daily full backup of the database (during the maintenance window)
  * Transaction logs are backed-up by RDS every 5 minutes
  * => ability to restore to any point in time (from oldest backup to 5 minutes ago)
  * 7 days retention (can be increased to 35 days)

* DB Snapshot:
  * Manually triggered by the user
  * Retention of backup for as long as you want

### RDS Read replicas for read scalability

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202021-03-27%20at%207.04.28%20PM.png)

* Up to 5 replicas
* Within AZ, Cross AZ ot Cross Region
* Replication is **ASYNC**, so reads are eventually consistent
* Replicas can be promoted to their own DB
* Applications must update the connection string to leverage read replicas

#### Use Cases:

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202021-03-28%20at%2012.45.16%20PM.png)

* You have a production database that is taking on normal load
* You want to run a reporting application to run some analytics
* You create a Read Replica to run the new workload there
* The production application is unaffected
* Read replicas are used for SELECT (=read) only kind of statements (not INSERT, UPDATE, DELETE)

#### Network Cost

* In AWS there’s a network cost when data goes from one AZ to another
* To reduce the cost, you can have your Read Replicas in the same AZ

#### Multi-AZ(Disaster Recovery)

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202021-03-28%20at%2012.54.19%20PM.png)

* **SYNC** Replicas
* One DNS Name - automatic app failover to standby
* Increase availability
* Failoiver in case of loss of AZ, loss of network, instance or storage failure
* No manual intervention in apps
* Not used for scaling

### RDS Encryption and Security

* At Rest encryption:
  * Possibility to encrypt the master & read replicas with AWS KMS - AES-256 encryption
  * Encryption has to be defined at launch time
  * If the master is not encrypted, the read replicas cannot be encrypted
  * Transparent Data Encryption (TDE) available for Oracle and SQL Server
* In-flight encryption:
  * SSL certificates to encrypt data to RDS in flight
  * Provide SSL options with trust certificate when connecting to database
  * To enforce SSL:
    * PostgreSQL: `rds.force_ssl=1` in the AWS RDS Console (Parameter Groups)
    * MySQL: Within the DB: `GRANT USAGE ON *.* TO 'mysqluser'@'%' REQUIRE SSL;`

### RDS Encryption Operations

* Encrypting RDS backups

  * Snapshots of un-encrypted RDS databases are un-encrypted

  * Snapshots of encrypted RDS databases are encrypted

  * Can copy a snapshot into an encrypted one

* To encrypt an un-encrypted RDS database:

  * Create a snapshot of the un-encrypted database

  * Copy the snapshot and enable encryption for the snapshot

  * Restore the database from the encrypted snapshot

  * Migrate applications to the new database, and delete the old database

### RDS Security - Network & IAM

* Network Security
  * RDS databases are usually deployed within a private subnet, not in a public one
  * RDS security works by leveraging security groups (the same concept as for EC2 instances) – it controls which IP / security group can communicate with RDS

* Access Management
  * IAM Policiies help control who can manage AWS RSS, through RDS API
  * Traditional username and password can be used to log into the database
  * IAM-based authentication can be used to login into RDS MySQL & PostgreSQL

### RDS - IAM Authentication

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202021-03-28%20at%202.50.17%20PM.png)

* IAM database authentication works with MySQL and PostgreSQL
* You don’t need a password, just an authentication token obtained through IAM & RDS API calls
* Auth token has a lifetime of 15 minutes
* Benefits:
  1. Network in/out must be encrypted using SSL
  2. IAM to centrally manage users instead of DB
  3. Can leverage IAM Roles and EC2 Instance profiles for easy integration

### RDS Security - Summary

* Your responsibility:

  1. Check the ports / IP / security group inbound rules in DB’s SG
  2. In-database user creation and permissions or manage through IAM
  3. Creating a database with or without public access
  4. Ensure parameter groups or DB is configured to only allow SSL connections

* AWS responsibility:

  1. No SSH access

  2. No manual DB patching

  3. No manual OS patching

  4. No way to audit the underlying instance

## Amazon Aurora (from AWS, not open sourced)

