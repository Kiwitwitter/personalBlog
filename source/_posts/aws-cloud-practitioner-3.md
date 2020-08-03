---
title: AWS Cloud Practitioner Essentials, Architecture
date: 2020-01-20 15:10:34
tags:
- study
- aws_cloud_practitioner
---

## The AWS Well-Architectured Framework

### Introduction

* Access and improve architectures
* Understand how design decisions impact business
* Learn the five pillars and design principles

### 5 Pillars

#### In general:

* Security
* Reliability
* Performance efficiency
* Cost optimization
* Operational excellence

#### Security Pillar:

* Identify and access management (IAM)

  Critical to ensure that only authorized and authenticated users are able to access your resources, and only in the manner you intend.

* Detective controls

  Can be used to identify a potential security incident by considering approaches such as capturing or analyzing logs and integration auditing controls.

* Infrastructure protection

  Ensures that systems and services within your architecture are protected against unintended and unauthorized access.

* Data protection

  There are numerous approaches and methods to consider. Some of them include dara classification, encryption, protecting data at rest and in transit, data backup, and finally replication and recovery when needed.

* Indicent response

  Will ensure that your architecture is updated to accommodate a timely investigation in recovery.

* **Design Principles**:

  * Implement security at all layers
  * Enable traceability
  * Apply principle of least provilege
  * Focus on securing your system
  * Automate

#### Reliability Pillar:

* Recover from issues/failures

* Apply best practices in:

  * Foundations

    In order to achiveve reliability, your architecture and system must have a well-planned foundation in place that can handle changes in demand or with requirement, and also detect failure and automatically heal itself. 

    Before architecting any system, foundational requirements that influence reliability should be in place.

  * Change management

    It's important to fully understand and be aware of how change can affect your system.

    If you planned proactively and monitor your system, you can accommodate and adjust to change quickly and reliably. To ensure the system is reliable, it's a key to anticipate, become aware and respond and prevent failures form happening. 

  * Failure management

    In a cloud environment, you can take advantage of automation with monitoring, replace systems in your environment, and later troubleshoot failed systems, all at low cost, and all while it's still being reliable

* Anticipate, respond, and prevent failures

* **Design principles**:

  * Test recovery procedures

  * Automatically recover

  * Scale horizontally

    When you have a large service, it's beneficial to replace it with multiple small resources to reduce the impact of a single resources to reduce the impact of a single point of failure on the overall system.

  * Stop guessing capacity

    In cloud environment, you have the ability to monitor demand and system utilization and automate the addition or removal of resources

  * Manage change in automation

#### Performance Efficiency Pillar:

* Select customizable solutions

  Solutions vary based on the kind of workload you have. With AWS, resources are virtualized and allow you to customize your solutions in many different types and configurations

* Review to continually innovate

  With review, you can continually innovate your solutions and take advantage of newer technologies that become available. 

* Monitor AWS services

  You need to monitor the performance to ensure that you can remediate any issues before customers are affected and become aware of them.

* Consider the trade-offs

* **Design Principles**:

  * Democratize advanced technologies

    Consume new knowledge and technologies as a service rather than having IT team figure out how to do it.

  * Go global in minutes

    Do global depploy with AWS for lower latency and better experience for customers, at a minial cost

  * Use a serverless architectures

    This remove the need to run and  maintain traditional servers for compute actibities, and also remove burden and can lower transactional costs

  * Experiment more often

    Carry out quick testing to enhance efficiency

  * Have mechanical sympathy

    Use technology approach that best aligns to what you're trying to do.

#### Cost Optimization Pillar:

* Use cost-effective resources

  Make sure the system is using the right services, resources and configurations is one of the key parts to cost savings

* Matching supply with demand

* Increase expenditure awareness

  Being fully cognizant of what spending and cost drivers are happening with your business is critical. So having the ability to see, understand, and break down the current costs, predict future costs, and plan accordingly only enhances the cost optimization of your architecture in the cloud.

* Optimize over time

* **Design Principles**:

  * Adopt consumption omdel

  * Measure overall efficiency

    Measure the business output of the systems, and the costs associated woth delivery it, then take this measurement to uderstand how gains are made from increasing output and reducing cost.

  * **Reduce** spending on data center operations

  * Analyze and attribute expenditure

    Accurately identidy the usage and cost of systems. Customers can measure their return on investment, which provides them the opportunities to optimize services and reduce costs.

  * Use managed service

    Use managed service to remove operational burden.

#### Operational Excellence Pillar:

* Manage and automate changes
* Respond to events
* Define the standards

## Fault Tolerance and High Availability

Fault Tolerance refers to:

* Ability of a system to remain operational
* Built-in redundancy of a application's component

High Availability refers to:

* Systems are generally functioning and accessible
* Downtime is minimized
* Minimal human intervention is required
* Minimal up-front financial investment

On premises vs AWS:

| Traditional (On premises)                         | AWS                                                          |
| ------------------------------------------------- | ------------------------------------------------------------ |
| Expensive<br />Only mission-critical applications | Multiple servers<br />Availability Zones<br />Regions<br />Fault Tolerant services |

### High Availability Service Tools

* Elastic Load Balancers

  ELB is a service that distributes incoming traffic or load amongst your instances. ELB can also send metrics to Amazon CloudWatch, which is a managed monitoring service.

  ELB can be a trigger and notify you of high latency or if servers are becoming over-utilized.

* Elastic IP Addresses

  Elastic IP Addresses are useful in providing greater fault-tolerance for applications.

  Elastic IPs are static IP addresses designed for dynamic cloud computing. 

  This tool allows you to mask a failure of an instance or software by allowing your user to use the same IP address with replacement resources.

* Amazon Route 53

  This is used to translate domain names into IP addresses. 

  It was developed to support simple routing, latency-based routing, health checks and DNS failover, and geolocation routing.

* Auto Scaling

  Designed to assist user in building a flexible system that can adjust and be modified depending on changes in customer demand. 

  With Auto Scaling, you can avoid limitations of manually creating new resources. Instead, you can create new resources on demand or have scheduled provisioning. This ensures that your applications and systems are always available no matter what the load is. 

* Amazon CloudWatch

  It collects and tracks your metrics of your applications. Another feature is that you have the ability to create and use your own custom metrics. If there is high latency or metrics that have passsed the set threshold, CloudWatch can adjust automatically to ensure high availability of your architecture.

### Fault Tolerant Tools

* Amazon Simple Queue Service

  Can be used as the backbone of the fault-tolerant application. It is highly reliable distributed messaging system. SQS can help you ensure that your queue is always available.

* Amazon Simple Storage Service

  Provides high durable and fault-tolerant data storage. S3 stores all of the data redundantly on multiple different devices across multiple facilities in a region.

* Amazon Relational Database Service

  Provides high availability and fault tolerance by offering several features tp enhance the reliability of your critical databases.

  

