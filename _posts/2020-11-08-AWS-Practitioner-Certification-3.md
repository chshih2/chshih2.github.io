---
layout: post
title: "AWS Certified Cloud Practitioner Notes: Technology"
description: "main services AWS provides"
categories: [AWS]
tags: [certificate]
redirect_from:
 - /2020/11/08/
---

It has been a year since I got awarded [AWS Cloud Credits for Research][1] last October.
I’m grateful for the opportunity and I have been enjoying using the EC2 service to do basically anything for my research.
To explore more of their services, I decided to take some online courses.
As soon as I started digging in, the enormous information just hit me hard.
AWS is more than virtual services you can request based on your need.
If I can start from basic and take some notes for future reference, it will be quite useful.
In addition, they offer different certifications that offer me some guidance on what to study.
The first certification I’m targeting is [AWS Certified Cloud Practitioner][2], and it covers four domains: Cloud Concepts, Security and Compliance, Technology, and Billing and Pricing.
The course I took is from [AWS Newbies][3].
The note is following the outline of the course, and additional material is added for my own understanding.
This post is about **technology**, meaning all the core services AWS provides..


---

# Deploying on AWS
* **Management Console**

Graphical interface (website)

* **Commnad-line Interface** (CLI)

Run commands to shut down some services, or add new file to some cloud storage. We can create scripts to run on AWS.

* **Software Development Kits** (SDKs)

This allows us to incorporate a wide range of AWS cloud services into our code using a variety of popular programming languages like NODEJS, C++, Java, Ruby, and PHP.

* Infrastructure as code

We can configure and launch specific AWS Cloud services with code, and it helps speeding up the deployment process, and removes the risk of human error. AWS CLI’s and SDK’s can help create an environment that utilize infrastructure as code.

# AWS Global Infrastructure
* **Region**

AWS defines a region as a physical location around the world where they cluster data centers. Each AWS Region consists of multiple, isolated, and physically separate data centers, which they call Availability Zone. Some regions cost more than others. And service level agreements, or SLAs, also vary by region. Other than that, we also need to consider the compliance requirements. All of these may require us to host our resources in specific regions or multiple regions

* **Availability Zone** (AZ)

This is defined as discrete data centers with redundant power, networking, and connectivity in an AWS Region.

*  This setup ensure:
	* High availability: host in multiple AZs
	* Resiliency: have ability to provide uninterrupted performance even during natural
	* Redundancy: have multiple copies of data in different data centers

# Compute
* **Elastic Compute Cloud** (EC2)

EC2 is like virtual servers, but it is more flexible. First the configuration and the storage are all scalable. It allows us to obtain and configure capacity freely. Second, we can even choose between several operating systems. Most importantly, the processors include the most powerful GPU instances as well as the lowest cost-per-inference instances in the cloud. We can choose the processors based on our needs. There are so many options to choose from, so I always check [this post][4] to make sure I pick the right one for my needs. It contains cost and performance for variety of GPU listed on AWS.


* **Elastic Beanstalk**
	* Deploy and scale web applications and services automatically from capacity provision, load balancing, auto scaling to monitoring.
	* Accept a variety of languages, such as, Java, Python, Ruby…
	*  Free and pay only for other AWS resources needed for deployment.
	* Infrastructure as code

* **Elastic Load Balancing**
	* Automatic distribute among servers
	* Fault tolerant
	* Scalable and secure
	* Monitor

* **Lambda**
	* Run a lambda function in response to certain events. For example, take user to certain page after users upload a video.
	* Lambda runs the function and scales the application when the event happens.
	* Pay only for the running time
	* Infrastructure as code

* **Lightsail**
	* Test out projects without deploying from scratch with all the preconfigured operating systems, web apps and development stacks.
	* Simple workload and quick deployments

# Storage
* **Simple Storage Service** (S3)

  S3 allow users to store and protect any amount of data for a range of use cases, such as the data needed in website, apps and backup data.

	* Access control

	* Lifecycle policies

  This means it would automatically transfer files from one storage class to a cheaper one after a certain number of days.

	* Storage Classes
		* Standard class: frequently accessed files
		* Glacier Deep Archive: rarely accessed backup data.
		* S3 Intelligent-Tiering: store data with changing or unknown access patterns
		* S3 Outposts storage class: for meeting data residency requirements, and store data on-premises in the Outposts environment.

* Elastic Block Store (EBS)
	* Extra storage that can be attached to an EC2 instance
	* Automatically replicated within their AZ, so they are more durable.

* Snowball
	* Hardware solution for big amount of data (that might take years to upload)
	* Regular Snowball: 50 Terabytes
	* Snowball Mobile: 100 Petabytes

* Storage Gateway
	* By installing a virtual machine onto an on-premises data centers host server, Gateway creates a gate that connects the on-site users and devices to the resources stored in AWS Cloud. This can reduce latency when everybody is uploading and downloading files using the same limited network.

	* File Gateway

	Files are saved as objects on S3. It is 1 to 1 representation of each file. The gateway asynchronously updates the objects in S3.

	* Volume Gateway

	File are saved in blocks that are like virtual hard drive. These blocks can be backed up as EBS snapshots.
		* Store volume: complete copy on premises, backup snapshots on AWS
		* Cached volume: most recent access on-premises, complete copy on AWS

	*  Tape Gateway
	This save backups on digital tape cartilages stored on S3. Data is stored locally then asynchronously uploaded to S3. The data can then be archived using Amazon Glacier, and we only need to pay for storage and data retrieval.

	* Quicker access -> more expensive

Tape Gateway is slow and cheap, while S3 Glacier is fast and expensive.

# Database
* DynamoDB
	* This service automatically scale up and down database based on users needs.
	* It is server-less.
	* This scalable NoSQL database service is used by Snapchat, Lyft and Netflix.

* Relational Database Service (RDS)
	* This service deals with scalable relational database.
	* Works with Aurora, the AWS’s own relational database engine

* Aurora
	* It’s a relational database engine that is MySQL and PostgreSQL compatible.
	* It offers monitoring and migration services.

* Amazon Redshift
	* Data warehouse level of storage service
	* Security is built in, and data encryption can be done easily with common compliance requirements like HIPAA.


# Network and Content Delivery
* AMZ Virtual Private Cloud (VPC)
	* The virtual private cloud is just like someone’s home network
		* The modem <-> the internet gateway
		* The router <-> the route table
		* The network’s firewall <-> the network access control list
		* Laptops and tablets <-> EC2 instances

* CloudFront
	* To load websites and applications for end users faster, there are content delivery networks (CDNs) on the internet. It is a system of distributed servers around the world that delivers website and application content to end users based on factors like location of the user, origin of the website or application, and the location of the content delivery server.
	* Amazon CloudFront achieve faster loading speed by using edge locations to cache files and resources for quicker retrieval.
	* This allows users to download the resources from somewhere closer.

* Route 53
	* It routes end users to your internet applications inside and outside of AWS, like a DNS service
	* Basic functions are domain registration, domain name system, or DNS, service, health checking of web application accessibility, and auto naming for service discovery.

# Management Tools
* Cloud Formation
	* allow users to create templates to set resources in a certain way.
	* CloudFormation is free. We only pay for the resources we use when we run the service, like the EC2 instances or S3 bucket storage.
	* Infrastructure as Code: provision anything using a simple text file written in JSON or YAML.
	* Version control is also available.

* Cloud Trail
	* Track user activity and API usage.
	* Log and monitor account activities
	* Simplify compliance audits
	* We can use CloudTrail to automatically respond to security vulnerabilities.

* Cloud Watch
	* System-wide visibility into resource utilization, application performance and operational health.
	* We can set up CloudWatch alarms to automatically make changes using pre-defined triggers.




[1]: [Application](https://aws.amazon.com/research-credits/)
[2]: [AWS Certified Cloud Practitioner](https://aws.amazon.com/certification/certified-cloud-practitioner/)
[3]: [Introduction to AWS for Newbies - AWS Newbies](https://awsnewbies.com/)
[4]:[Choosing the right GPU for deep learning on AWS | by Shashank Prasanna | Towards Data Science](https://towardsdatascience.com/choosing-the-right-gpu-for-deep-learning-on-aws-d69c157d8c86)
