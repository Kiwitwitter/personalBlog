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
    * Maximum insatnces
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

(To be continued...)