---
title: AWS Cloud Practitioner, AWS Security
date: 2020-01-21 23:32:50
tags:
- study
- aws_cloud_practitioner
---

## The Shared Responsibility Model

Both the user and AWS should be responsible for the security of the service running in AWS. 

We divide the security into 7 levels, and create a shared security model. Some levels are user fully responsible for, some levels are AWS fully responsible for. 

Model stack:

| User Data       |
| --------------- |
| **Application** |
| **Guest OS**    |
| **Hyperviser**  |
| **Network**     |
| **Physical**    |

* Physical

  This is iron and concrete, a barbed-wire fence. AWS don't give access to any third party to the service or data centers.

* Network

  AWS fully responsible for this, AWS run the network, proprietary networking protocols designed to allow security of our systems, so elements like VPC can work at scale, velocity, and designed to protect traffic.

* Hypervisor

  AWS hypervisor uses a Xen-based hypervisor, and AWS made a lot of specific changes to the hypervisor that make it secure and scalable.

* Guest OS, Application, User data

  When user choose the operating system, user can choose whatever operating systems they use and whatever applications that they are using inside the operating system. AWS has no visibility to that, and the data are totally protected by user's access key secret and how they encrypt it. 



## Identity and Access Management

### User

In the case of AWS, user is a permanent named operator. Could be human, or a machine. The Idea is that my credentials are permanent, and they stay with that named user util there is a forced rotation , whether is'a name and password, access key, secret key combination.

### Group

A collection of users. Group can have many users, users can belong to many groups.

### Role

In AWS, a role is not a permission, but an authentication method. A role is an operator, could be human, or a machine. The key part is the credentials with a role are temporary. 

### Policy Docs

Permissions, in every cases, happens in a seperate object known as the policy document. The policy document is a JSON document. It attaches either directly to a permanent named user or a group of users, or it can be attached directly to a role. The policy document lists the specific API or wildcard group of APIs that I am white-listing, or allowing, against which resources.

**Authentication and Authorization**: Authentication is verify who you are, authorization is to verify if you have the permission to do certain activities.



## Amazon Inspector

### IT Security Challenges

IT scurity matters, and securing IT infrastructure is:

* Complex
* Expensive
* Time consuming - build/configure.maintain
* Difficult to track all the changes in IT environment
* Hard to do effectively

### Introducing Amazon Inspector

* Assesses applications for:
  * Vulnerabilities
  * Deviations from best practices
* Produces a detailed report with:
  * Security findings
  * Prioritzed steps for remediation

### Amazon Inspector Benefits:

* Helps identify security vulnerabilities as well as deviations from security best practices in applications, both before they are deployed and while they are running in a production environment.
* Amazon Inspector is agent-based, API-driven, and delivered as a service. This makes it easy for you to build right into your existing DevOps process, decentralizing and automating vulnerability assessment an integral part of the deployment process
* The service helps reduce the risk of introducing security issues during development and deployment by automating the security vulnerabilities. 
* AWS continuously assesses the AWS environment and updates a knowledge base of security best practices and rules. 
* Amazon Inspector gives security teams and auditors visibility into security testing during application development.
* Amazon Inspector allows you to define standards and best practices for your applications and validate adherence to these standards.

### Amazin Inspector Accessing:

* Amazon Inspector Console
* AWS software development kits(SDKs)
* Amazon Inspector HTTPS API
* AWS command line tools

### Built-in rules

* Includes a knowledge base with hundreds of rules that mapped to:
  * Common Security compliance standards
  * Vulnerability definations
* Regularity updated by AWS security researchers



## AWS Shield

AWS shield is a **Managed Distributed Denial of Service** protection service that safeguards applications running on AWS. The service provides always-on detection and automatic inline mitigations that minimize application downtime and latency, so there is no need to engage AWS Support for DDOS protection.

### Differences between DDoS and DoS

#### DoS

DoS attack is a deliberate attemot to make your website or application unavailable to user-like flooding it with network traffic. Attackers use a variety of techniques that consume large amounts of network bandwidth or tie up other sysetm resources, disrupting access for legitimate users.

In short, a line attacker uses a single source to execute a DoS attck against a target.

#### DDoS

Attacker uses multiple sources to orchestrate an attack against a target. Sources may include distributed groups of malware infected computers, routers, IoT devices, and other endpoints.

DDoS are typically launched form a botnet of compromised computers or Internet devices. The objective to knock the targeted website or application offline for a period of time, disrupting availability for legitimate uses.

#### Difficulties of mitigating DDoS attack:

* Protection is complex to set up, and very often, it involves re-architecting your application
* Bandwidth issue may happen due to scalability issues if you opt to tackle mitigation from an on-oremises data center
* May need manual intervention to initiate mitigation
* In turn, this deplays resolution and increases network latency
* Due to the size, duration, and complex nature of mitigation systems, it can become cost-prohibitive

### AWS Shield tiers

#### AWS Shield standard

* Automatically protection
  * Any AWS resource
  * Any AWS region
* Quick Detection - Always on
* Inline attack mitigation
  * Built-in automated mitigation techniques
  * Avoids latency impact
* Self Service
  * No need to engage AWS Support

#### AWS Shield Advance

* Specialized support
* Advanced attack mitigation
* Visibility and attack notification
* Always-on monitoring
  * Amazon Route 53, Amazon CloudFront, Elastic Load Balancer, Elastic IP
* Enhance detection
* DDoS cost protection

### AWS Shield benefits

1. Seamless integration and deployment
2. Cost Efficient
3. Customizable protection

### AWS Shield Protections

1. Protecing DNS
   * Using Route 53
     * AWS Shield Standard - Hosted zones
     * AWS Shield Advanced - Attack visibility, DRT support
2. Protection web applications and APIs
   * Using Amazon CloudFront or Application Load Balancer
     * AWS Shield Standard - Always-on, scrubs bad traffic
     * AWS Shield Advanced - DRT support, traffic engineering, application layer protection
3. Protectin other applications
   * Using Elastic IP Address
     * AWS Shield Standard - Built-in techniques
     * AWS Shield Advanced - Custom mitigation profiles, additional bandwidth

## AWS Compliance

### AWS security information

AWS shares security information by:

* Obtaining industry certifications
* Publishing security and control practices
* Compliance reports

### Assurance programs

AWS provides compliance information and resources:

* Certification/attestations
* Legal/regulatory support
* Alignments/frameworks

![](https://raw.githubusercontent.com/Kiwitwitter/hexo-storage/master/img/Screen%20Shot%202020-01-23%20at%201.01.34%20AM.jpg)

### AWS risk and compliance programs

* Includes:
  * Criminal Justince Information Service (CJIS)
  * Cloud Security Alliance (CSA)
  * Family Educational Rights and Privacy Act (FERPA)
  * Health Insurance Portability and Accountability Act (HIPAA)
  * Motion Picture Association of America (MPAA)
* Help customers:
  * Document a complete control and governance framework
  * Deploy solutions that meet several industry-specific standards

### Components of AWS compliance

* Risk management
* Control environment
* Information security

#### Risk management foundation

AWS management established:

* Business plan:
  * Include risk management
  * Re-evaluated at list biannually
* Process:
  * Identify risks
  * Implement appropiate measures
  * Assess various internal/external risks

#### Risk management Framework

AWS compliance and security teams:

* Established framework and policies
* Maintain security policy
* Provide security training
* Perform application security reviews
  * Confidentially, integrity, and availability of data
  * Conformance to IS Policy

#### Risk management at work

* AWS security scans for vulnerabilities and notifies appropiate parties to remediate identified vulnerabilities 
* Customers request permission to conduct scans of their cloud infrastrcuture
* Independent security firms regularly perform vulnerability threat assessments
* Findings/recommendations categorized and delivered to AWS leadership

### Control environment

* Includes policies, processes, and control activities to secure the delivery of AWS service offerings
* Supports the operating effectiveness of AWS control framework
* Integrates cloud-specific controls
* Applies leading industry practices

### Information security

* Designed to protect
  * Confidentiality
  * Integrity
  * Availability 
* Publishes security whitepaper

### Customer compliance

* Review trusted information and document compliance requirements
* Design and implement control objectives that meet compliance requirements
* Identify and document controls owned by outside parties
* Verify all control objectives are met and all key controls are designed and operating effectively



