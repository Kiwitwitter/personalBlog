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

* Feature
  * Fully-Managed serverless compute
  * Event-driven execution
  * Sub-second meeting
  * Multiple languages supported

* AWS Lambda is compute service that lets users run code with provisioning or managing services. AWS Lambda executes code only when needed and scales automatically to thousands of requests per second. 

* AWS Lambda runs code on a highly available compute infrastructure, which provides all administration, including server and operating system maintenance, capacity provisioning, and auto-scaling, code monitoring and logging.

* AWS Lambda supports a variety of programming languages, including Node.js, Java, C# and Python.

* AWS Lambda is a event-based computing, user can run code in response to events, including changes to Amazon S3 buckets or an Amazon DynamoDB table.

* Lambda can respond to HTTP requests using Amazon API Gateway, and caan also invoke code using API calls made using AWS SDKs. 

* AWS Lambda is intended to support serverless and micro-service applications. User can build serverless applications that are triggered by AWS Lambda functions, and can automatically deploy them using AWS CodePipeline, AWS CodeDeploy

### Use Cases

It's very simple to use AWS Lambda, user just configure the environment, upload code and watch it run.

AWS use cases includes:

* Automated backups
* Event-driven log analysis
* Event-driven transformations
* Internet of Things
* operating serverless websites

Also can use Amazon Lambda and Amazon Kinesis to process real-time streaming data for 

* application activity tracking
* transaction order processing
* clickstream analysis
* data cleamsing metrics
* generation log filtering
* Indexing social media analysis
* device telemetry and monitoring



## AWS Elastic Beanstalk

### Introduction

What is Elastic Beanstalk?

* Platform as a Service, means that you have the whole infrastructure created for you

* Allows quick deployment of your applications

* Reduces management complexity

* Keep control in your hands:

  * Choose your instance
  * Choose your database
  * Set and adjust Auto Scaling
  * Update your application
  * Access server log files
  * Enable HTTPS on Load Balancer

* Supports a large range of platforms

  * Packer Builder
  * Single Container, Multicontainer, or Preconfigured Docker
  * Go
  * Java SE
  * Java with Tomcat
  * .NET on Windows Server with IIS
  * Node.js
  * PHP
  * Python
  * Ruby

* Easy Delpoyment and update

  ![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-19%20at%204.40.27%20PM.jpg)

### Components

* Elastic Beanstalk provides:

  ![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-19%20at%204.37.49%20PM.jpg)





## Amazon Simple Notification Service

### Instroduction

Amazon Simple Notification Service:

* Flexible, fully managed pub/sub messaging and mobile communications service

* SNS also coodinates the delivery of messages to subscribing endpoints and clients

* Easy to setup, operate and send reliable communications

Amazon SNS pub/sub Messaging and Mobile Notifications:

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-19%20at%205.08.28%20PM.jpg)

## Amazon CloudWatch

### Service Introduction

Amazon CloudWatch monitors your Amazon Web Services (AWS) resources and the applications you run on AWS in real time, including:

* Collect and track metrics
* Collect and monitor log files
* Set alarms
* Automatically react to changes

### Overview

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-19%20at%206.03.26%20PM.jpg)

### Use Cases

* Respond to state changes in your AWS resources
* Automatically invoke an AWS Lambda function to update DNS entries when a event notifies that Amazon EC2 instance enters the running state
* Direct specific API records from CloudTrail to a Kinesis stream for detailed analysis of potential security or availability risks
* Take a snapshot of an Amazon EBS volume on a schedule
* Log S3 Object Level Operation using CloudWatch Events

### CloudWatch Components

#### Metrics

* Data about the performance of the systems

* Represents a time-ordered set of data points that are published to CloudWatch

* By default, sevral services provide free metrics for resources

  Such as Amazon EC2 insatcne, Amazon EBS volumes, Amazon RDS DB instances

* Publish your own application metrics

* Load all the metrics in your account for search, graphing, and alarms

#### Alarms

* Watch a single metric

* Performs one or more actions

  Based on the value of the metric relative to a threshold over a number of time periods

* The action can be:

  * An Amazon EC2 action
  * The Auto Scaling action
  * A notification sent to an Amazon SNS topic

* Invokes actions for sustained state changes only

#### Events

* New real-time stream of system events that describe changes in AWS resources
* Use simple rules to match events and route them to one or more target functions or streams
* Aware of operational changes as they occur
* Responds to these operational changes amd takes corrective action as necessary
* Schedule automated actions that self-trigger at certain times using Cron or rate expressions

#### Logs

* Monitor and troubleshoot systems and applications using existing log files
  * Monitor logs for specific phrases, values, or patterns
* Retrieve the associated log data from CloudWatch Logs
* Includes an installable agent for Ubuntu, Amazon Linux, and WIndows at no additional charge
* Monitor Logs from Amazon EC2 Instances in Real-time
* Monitor AWS ClouTrail Logged Events
* Archive Log Data, your metrics can be stored durably in CloudWatch as CloudWatch log:
  * Admins and other parties can review CloudWatch Logs directly in the AWS Management Console
  * Logs can be stored in Amazon S3, to be accessed by other services or another user.
  * Logs can be streamed in real time to data-processing solutions like Amazon Kinesis Streams or AWS Lambda.

#### Dashboards

* Customizable home pages in the CLoudWatch console to monitor your resources in a single view
  * Even those resources that are spread acress different regions
* Create customized views of the metrics and alarms for your AWS resources.
  * Each dashboard can display multiple metrics, and can be accessorized with text and images
* Create dashvoards by using the console, the AWS CLI, or by using the **PutDashboard** API



## Amazon CloudFront

### AWS Global Infrastructure

AWS CLoudFront uses a global network of more than 80 locations and more than 10 regional edge caches for content delivery. The edge locations are located globally around the world, and frequently increases. 

### CloudFront overview

* Global, Growing Network
* Secure Content at the Edge
* Deep Integration with Key AWS Services
* High Performance
* Cost Effective
* Easy to Use

### Creating and configuring a CDN

When creating a CDN, you need to choose what type you want to create. RTMP is used for video content streaming, and Web is designed to use it by usual content delivery that is not a video stream. 

Then, you must specify at least one origin and one behavior. 

* Basically, the origin can be your S3 bucket or any application that you run even outside AWS. You can put the IP address of your web server, the load balancer endpoints taht can be reachable over the Internet.
* The behavior basically matches: "What is the URL pattern that you want to associate woth that origin?"
* User can always add more origins in the future, but must specify one during creation.
* User can even use other AWS services or AWS command line interface to automate the creation of new distributions for new environment. 

### Use cases

* static asset caching
* live and on-demand video streaming
* security and DDoS protection
* API acceleration
* Software Distribution



## AWS CloudFormation

### Service Introduction

* AWS CloudFormation **simplifies** the task of **repeatedly** and **predictably** creating groups of related resources that power your applications. CloudFormation is all about resource provisioning.

* There are three method to call the APIs: the AWS management console, the AWS CLI, the AWS SDK/API. Using one of the three methods, we can construct virtual environment for our workploads. 
* We use API calls such as CreateVPC to construct a VPC, LaunchInstances to create a new EC2 instance.
* CloudFormation is a:
  * Fully-managed service
  * Create, update and delete resources in stacks

### Overview

* The big picture of this process is:

  * Confirmation reads template files (the instructions on what resources to actually go ahead and provisions)
  * CloudFormation constructs the resources listed in the template file and the output of this process is your environment, which is known as a stack.

  ![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-20%20at%2012.07.41%20AM.jpg)

* You can interact with the service through the management console or build scripts to automate CloudFormation actions.

#### Stacks:

* Resources generated
* Unit of deployment
* Create Stack, Update Stack by rerunning a modified template, Delete Stack
* Most organizations modularize stacks by creating separate templates for networking, security and applications.

#### Templates:

* describe the resources to provision

* These are text files written in JSON or YAML format

* As an added benefit, if you provisioned your environment using templates, then your template become a form of documentation for your environment.

* Template includes:

  * The same information you would specify if you built the environment mannually through the console
  * Template does use specific formatting constructs, but the resource and property information is the same
  * You don't have to list your resources in the exact order of the creation, we can simply use **DependsOn** attribute to control the order CloudFormation will create the resources, so that we can build a sequence of events, like Database server needs to be created before a web server.

* Parameters in the template can be used to control the stacks generated. E.g. Parameter one creates the development stack, Parameter two will generate the product stack.

* **Infrastructure as Code**:

  Means you can simply control your infrastructure through software code like a template, which is flexible. 

  You can change it and also keep different versions of the same template,.

  Organizations that reply on CloudFormation build out template libraries much as they do code repositories for applications.

#### Two critical requirements for CloudFormation:

* Templates have to be correct, otherwise CloudFormation stops
* The user who run the CloudFormation msut have the permission to all services referenced in the template. 