---
title: AWS Cloud Practitioner, AWS Integrated Services
date: 2020-01-12 23:53:51
tags:
- study
- aws_cloud_practitioner
---

## Application Load Balancer

### Service Introduction

* Application Load Balancer is the second type of balancer introduced as part of Elastic Load Balancing Service.
* Some of the additional features for the Application Load Balancer are the ability to enable additional routing mechanisms for your request using path- or host-based routing, native IPv6 support in a VPC, AWS web application firewall integration, and more.

### Overview

* Key terms

  | Concept      | Description                                                  |
  | ------------ | :----------------------------------------------------------- |
  | Listeners    | A Listener is a process that checks for connection requests, using the protocol and port that you configure. The rules that you define for a listener determine how the load balancer routes requests to the target in one or more target groups |
  | Target       | A target is a destination for traffic based on the established listener rules. |
  | Target Group | Each target group routes requests to one or more registered targets using the protocol and port number specified. A target can be registered with multiple target groups. Health checks can be configured on a per target group basis. |

* Added features

  * Path and host-based routing

    * Path-based provides rules that forward requests to different target groups

    * Host-based provides rules that forward requests to different target groups based on host name

  * Deletion Protection & Request tracing

    Request tracing can be used to track HTTP requests from clients to target

  * Dynamic Ports

    Amazon ECS integrates with Application Load Balancer to expose Dynamic Ports utilized by scheduled containers

  * AWS WAF (AWS Web Application Firewall)

  * Native IPv6 Support

### Use Case

* Sample use case:

  ![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-13%20at%2010.34.40%20PM.jpg)



## Auto Scaling

### Service Introduction

Auto Scaling helps you ensure that you have the correct number of Amazon EC2 instances available to handle the load for your application. 

We need to monitor the workload using Amazon CloudWatch, though CloudWatch will not add or remove EC2 instances.

We need to keep Scalibity as well as Automation.

### Overview

* Scaling out and Scaling in

  * Auto Scaling can automatically adjust the number of EC2 instances running based in the condition that user defines, or as scheduled.
  * If Auto Scaling adds more instances, this is termed **scaling out**.
  * When Auto Scaling terminates instances, this is termed **scaling in**.

* Auto Scaling Components

  * Launch Configuration
    * AMI
    * Instance type
    * Security Groups
    * Roles
  * Auto Scaling Group
    * VPC and Subnet(s)
    * Load Balancer
    * Minimum instances
    * Maximum instances
    * Desired capacity
  * Auto Scaling Policy
    * Scheduled
    * On-demand
    * Scale-out policy
    * Scale-in policy

* Dynamic Auto Scaling

  ![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-13%20at%2011.51.03%20PM.jpg)

  

  ## Amazon Route 53

  ### Introduction

  Amazon Route 53 is a Domain Name System, or DNS, web service designed to provide businesses and developers with a reliable and highly scalable way to route end-user t internet applications.

  ### How does it work?

  ![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-14%20at%2012.11.15%20AM.jpg)

  The user asks to translate a name into an IP address \<A> and Route 53 does the translation.



## Amazon Relational Database Services (RDS)

### Challenges of Relational Database

* Server Mantenance and energy footprint
* Software install and patches
* database backups and high availability
* Limits on scalability
* Data security
* OS install and patches

### Service Introduction

Amazon RDS is a managed service that sets up and operates a relational database in the cloud, Amazon RDS provides a cost-efficient and resizable capacity while automating time-consuming administrative tasks. 

Amazon RDS gives the performance, high availability, security, and compatibility to users.

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-18%20at%201.00.17%20AM.jpg)

Amazon RDS manages:

* OS Installation and patches
* Database software install and patches
* Database backups
* High Availability
* Scaling
* Power and rack & stack
* Server maintenance

### Overview and Use Cases

The basic building block if Amazon RFS is the database instance. A database instance is an isolated environment that can contain multiple user-created databases and can be accessed by using the same tools and applications that you use with a standalone database instance.

The resources found in a database instance are determined by its database instance class, the type of storage, is dictated by the type of disks.

DB Instance class includes:

* CPU
* Memory
* Network performance

DB Instance Storage Includes:

* Magnetic
* General purpose (SSD)
* Provisioned IOPS

Amazon RDS currently supports 6 databases:

* MySQL
* Amazon Aurora
* Microsoft Sequel Server
* PostgreSQL
* MariaDB
* Oracle

You can run an instance using Amazon VPC and have control of the virtual networking environment.

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-18%20at%201.51.13%20AM.jpg)

User can select own IP address range, create subnets, and configure routing and access control lists.  

The basic functionality of Amazon RDS is the same whether or not it is in the VPC. But usually the database insatcne is isolated in an VPC and is only made directly accessible to indicated application instances.

One of the most powerful features of Amazon RDS is the ability to configure the database instance for high availability with a multi-agency deployment. Once configured, RDS automatically generates a standby copy of the database instance in another Availability Zone within the same VPC. After seeding the database copy, transactions are synchronously replicated to the standby copy. 

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-18%20at%202.00.45%20AM.jpg)

Having multi-AZ RDS database can provide high availability as well as protection against database instance failure. If one master instance failed, the RDS can bring the replication online as the new master instance. And there should be no data loss due to the synchronous replication. Because applications reference the database by name using RDS DNS endpoint, user don't need to change anything in the application code to use the standby copy.

RDS also supports the creation of read replicas for MySQL, MariaDB, PostgreSQL and Amazon Aurora. Updates made to the source database instances are asynchronously copied to the read replica instance. User can reduce the read load on source by routing read queries to read replicas, and can also scale out beyond the capacity constraints of a single database instance for read-heavy database workloads. Read replica can also be promoted to become the master database instance, but due to asynchronous replication, this requires manual action.



Read replicas can be created in a different region than the master database, which help satisfy disaster recovery requirements or cutting down latency by redirecting read queries to to a read replica. 

Use cases:

* RDS is ideal for Web and mobile applications that need a database with high throughput, massive storage scalability and high availability. 

* RDS doesn't have any licensing constraints, it perfectly fits the variable usage pattern of these applications. RDS also provides a flexible, secured, and low-cost database solution for online sales and retailing. 
* RDS manages the database infrastructure, so mobile and online game developers don't have to worry about provisioning, scaling, or monitoring database servers. 

### Benefits

* Highly scalable
* HIgh Performance
* Easy to administer
* Available and durable
* Secure and compliant

## AWS Lambda

### Overview

* Fully-Managed serverless compute
* Event-driven execution
* Sub-second meeting
* Multiple languages supported

AWS Lambda is compute service that lets users run code with provisioning or managing services. AWS Lambda executes code only when needed and scales automatically to thousands of requests per second. 

### Use Cases



## AWS Elastic Beanstalk



## Amazon Simple Notification Service



## Amazon CloudWatch



## Amazon CloudFront



## AWS CloudFormation

