---
layout: post
title: "AWS Certified Cloud Practitioner Notes: Intro and Cloud Concepts"
description: "General cloud concepts and AWS basics"
categories: [AWS]
tags: [certificate]
redirect_from:
  - /2020/11/03/
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

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
This post is about Cloud concepts.



---

# History

* [Mainframe computer][4]

	The large cabinet,  that houses the  CPU and main  memory of early computers.

* [Virtual machine][5]

	A virtual machine is a computer file, typically called an image, that behaves like an actual computer.
	Multiple virtual machines can run simultaneously on the same physical computer. For servers, the multiple operating systems run side-by-side with a piece of software called a hypervisor (see below) to manage them.

* [Hypervisor][6]

	Hypervisors are virtual machine monitor  that enables numerous virtual operating systems to simultaneously run on a computer system. These virtual machines are also referred as guest machines and they all share the hardware of the physical machine like memory, processor, storage and other related resources. This improves and enhances the utilization of the underlying resources.


---

# Advantages of Cloud

* Benefit from economics of scale

	The usage of the cloud is just like enterprises’ scale of operation. The cost advantages come with the cost per unit of output decreasing with increasing scale.

* No need to guess the capacity

	The infrastructure configuration won’t bother you too much anymore.

* Increase speed and agility
* No maintenance fee for infrastructure
* Go Global in mins

---

# Computing models

* Software as a service (SaaS)

Cloud-based apps over the Internet. Examples are email, calendar, and Adobe.

* Platform as a service (PaaS)

Allow users to deploy and manage apps without hardware. Instead, since the packages are pre-constructed, the  use only needs to execute code to host app. For example, MS Azure, Google App engine, and Heroku.

* Infrastructure as a service (IaaS)

Basic building blocks that are the most flexible to users, and are also the closest to old data center.

# Deployment Models

* Cloud (public)

100% infrastructure is on the cloud. This is suitable for companies that try to avoid costly procurement process.

* On-premises (private)

Like old data center. It is practical for companies that handles credential data or when privacy is important. This kind of model offers fast access to data as well because of the private network.

* Hybrid

It can be like a middle stage of migration or some companies just choose the cloud for backup.

# Design Principles of Cloud Computing

* Well-architected framework: secure, durable, efficient, high performing IT infrastructure

* Avoid unnecessary costs
* Reliability
	* Disaster recovery
	* Incorporate redundancy

		Ants built multiple routes to variety food resources. Same goes to a company to keep the business stays up and running. This metaphor on [this site][7] is amazing. It also covers four levels of redundancy: Hardware-level redundancy, process redundancy (higher availability for more important  processes), network redundancy, and geographic redundancy (to avoid natural disaster or power failure…)

	* Duplicate copied resources
* Efficiency
* Security
	* Automation is the best practice
	* Data protection
	* Traceability (track users’ actions if something bad happens)
	* Access
* Operational Excellence
	* Documentation
	* Refine operational procedures
	* Anticipate failure
	* Update process
	* learn from failures

# Amazon Web Service AWS

AWS started with a bookstore, and later launched web service for third-party shop platform. After some time, AWS became one of the top as service company. The others are MS Azure and Google Cloud.

The service in AWS is flexible, reliable and affordable. AWS provides IT infrastructure.
Resources can be easily accessed using internet.
The pay-as-you-go plans and services save money, time and resources.

# Services by Groups
* Compute services

Compute services include running virtual machines, software with pre-constructed env, hosting website ,  or simply running a function script.

* Storage services

This includes creating shared folder, storing data (txt, image, video) for websites, archiving data, or doing backups.

* Databese sevice

Deal with variety size of data (from relational to non-relational databases, from small to petabyte-scale data).


[1]: [Application](https://aws.amazon.com/research-credits/)
[2]: [AWS Certified Cloud Practitioner](https://aws.amazon.com/certification/certified-cloud-practitioner/)
[3]: [Introduction to AWS for Newbies - AWS Newbies](https://awsnewbies.com/)
[4]: [Mainframe computer - Wikipedia](https://en.wikipedia.org/wiki/Mainframe_computer#Differences_from_supercomputers)
[5]: [What is a Virtual Machine and How Does it Work | Microsoft Azure](https://azure.microsoft.com/en-us/overview/what-is-a-virtual-machine/)
[6]:[Hypervisor in cloud Computing | Hypervisor types | VMware](https://www.cloudoye.com/kb/general/what-is-hypervisor-in-cloud-computing-and-its-types)
[7]: [Redundancy in Cloud Computing Means Checking Four Areas](https://sg.atsg.net/blog/redundancy-in-cloud-computing-means-checking-four-areas)
