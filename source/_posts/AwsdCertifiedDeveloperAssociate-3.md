---
title: AWS Fundamentals, RDS + Aurora + ElatiCache
date: 2021-03-27 18:44:20
tags:
- study
- aws_certified_developer_associate
---

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
  * Transparent Data Encryption (TDE, real time encryption/decryption on I/O) available for Oracle and SQL Server
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

### Overview

* Postgres and MySQL are both supported as Aurora DB (that means your drivers will work as if Aurora was a Postgres or MySQL database)

* Aurora is “AWS cloud optimized” and claims 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
* Aurora storage automatically grows in increments of 10GB, up to 64 TB.
* Aurora can have 15 replicas while MySQL has 5, and the replication process is faster (sub 10 ms replica lag)
*  Failover in Aurora is instantaneous. It’s HA (High Availability) native.
* Aurora costs more than RDS (20% more) – but is more efficient

### Aurora High Availability and Read Scaling

* 6 copies of your data across 3 AZ:
  * 4 copies out of 6 needed for writes
  *  3 copies out of 6 need for reads
  * Self healing with peer-to-peer replication
  *  Storage is striped across 100s of volumes

* One Aurora Instance takes writes (master)
* Automated failover for master in less than 30 seconds, One of the replicas will become the **Master** once the Master fails
* Master + up to 15 Aurora Read Replicas serve reads
* **Support for Cross Region Replication**

### Aurora DB Cluster

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202021-03-28%20at%203.03.05%20PM.png)

### Features of Aurora

* Automatic fail-over
* Backup and Recovery
* Isolation and security
* Industry compliance
* Push-button scaling
* Automated Patching with Zero Downtime
* Advanced Monitoring
* Routine Maintenance
* Backtrack: restore data at any point of time without using backups

### Aurora Security

* Similar to RDS because uses the same engines
* Encryption at rest using KMS
* Automated backups, snapshots and replicas are also encrypted
* Encryption in flight using SSL (same process as MySQL or Postgres)
* Possibility to authenticate using IAM token (same method as RDS)
* You are responsible for protecting the instance with security groups
* You can’t SSH

### Aurora Serverless

* Automated database instantiation and autoscaling based on actual usage

* Good for infrequent, intermittent or unpredictable workloads

* No capacity planning needed
* Pay per second, can be more cost-effective

### Global Aurora

* Aurora Cross Region Read Replicas:
  * Useful for disaster recovery
  * Simple to put in place
* Aurora Global Database (recommended):
  * 1 Primary Region (read / write)
  * Up to 5 secondary (read-only) regions, replication lag is less than 1 second
  * Up to 16 Read Replicas per secondary region
  * Helps for decreasing latency
  * Promoting another region (for disaster recovery) has an RTO(Recover time objective) of < 1 minute

## ElastiCache

### Overview

It's a RDS for Caches.

* The same way RDS is to get managed Relational Databases…
* ElastiCache is to get managed Redis or Memcached
* Caches are in-memory databases with really high performance, low latency
* Helps reduce load off of databases for read intensive workloads
* Helps make your application stateless
* AWS takes care of OS maintenance / patching, optimizations, setup, configuration, monitoring, failure recovery and backups

### Architecture

#### DB Cache

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202021-03-28%20at%2011.29.38%20PM.png)

* Applications queries ElastiCache, if not available, get from RDS and store in ElastiCache.
* Helps relieve load in RDS
* Cache must have an invalidation strategy to make sure only the most current data is used in there.

#### User Session Store

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202021-03-28%20at%2011.42.46%20PM.png)

* User logs into any of the application
* The application writes the session data into ElastiCache
* The user hits another instance of our application
* The instance retrieves the data and the user is already logged in

### ElastiCache - Redis vs Memcached

| REDIS                                                        | MEMCACHED                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| * Multi AZ with Auto-Failover<br />* Read Replicas to scale reads and have high availability<br />* Data Durability using AOF persistence<br />* Backup and restore features | * Multi-node for partitioning of data (sharding)<br />* No persistence<br />* No backup and restore<br />Multi-threaded architecture |

### Lazy Loading

* Pros:
  * Only requested data is cached (the cache isn’t filled up with unused data)
  * Node failures are not fatal (just increased latency to warm the cache)
* Cons:
  * Cache miss penalty that results in 3 round trips, noticeable delay for that request
  * Stale data: data can be updated in the database and outdated in the cache

* Python PseudoCode:

  ```python
  def get_user(user_id):
    # Check the cache
    record = cache.get(user_id)
    
    if record is None:
      # Run a DB query
      record = db.query("select * from users where id = ?", user_id)
      # Populate the cache
      cache.get(user_id, record)
      return record
    else:
      return record
    
  # App code
  user = get_user(17)
  ```

  ### Write through

  Add or Update the cache when databases is updated.

  ![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202021-03-29%20at%2012.12.25%20AM.png)

* Pros:
  * Data in cache is never stale, reads are quick
  * Write penalty vs Read penalty (each write requires 2 calls)
* Cons:
  * Missing Data until it is added / updated in the DB. Mitigation is to implement Lazy Loading strategy as well
  * Cache churn – a lot of the data will never be read

* PseudoCode:

  ```python
  def save_user(user_id, values):
    record = db.query("update users ... where id = ?", user_id, values)
    cache.set(user_id, record)
    return record
  
  # App code
  user = save_user(17, {"Name":"Fake"})
  ```

### Cache Eviction and TTL

* Cache eviction can occur in three ways:
  1. You delete the item explicitly in the cache
  2. Item is evicted because the memory is full and it’s not recently used (LRU)
  3. You set an item time-to-live (or TTL)
* TTL are helpful for any kind of data:
  * Leaderboards
  * Comments
  * Activity streams
* TTL can range from few seconds to hours or days
* If too many evictions happen due to memory, you should scale up or out

