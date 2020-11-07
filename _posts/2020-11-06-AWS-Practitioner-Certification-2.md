---
layout: post
title: "AWS Certified Cloud Practitioner Notes: Security and Compliance"
description: “security and compliances in cloud”
categories: [AWS]
tags: [certificate]
redirect_from:
  - /2020/11/06/
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
This post is about **security and compliances**.


---

# Shared Responsibility Model
* **AWS** is responsible for everything **of the cloud**
	This includes protection and maintenance of infrastructure, from hardware to network.

* **Customer** is responsible for everything **in the cloud**
	This includes data encryption to patching servers. Therefore, anything inside the server should be taken care of by the customers, like updating the server's software, improving the software's security and performance, or simply fixing bugs.



# Well-architected framework in AWS
* Detective Controls

Enable traceability so that we can always recall who did what at what time. This includes auditing actions and changes to the environment all the time. There should also be an active monitor alert.

* Infrastructure Protection

Unlike a data center with one layer of strong protection of the building access, security on the cloud is relatively more secure on all infrastructure layers. I was a bit confused when the lecture brought up subnet and load balancer for an example. Isn't the load balancer for avoiding traffic jamming?

[The answer][4] is relatively straightforward. The off-loading function of a load balancer defends an organization against distributed denial-of-service (DDoS) attacks. It does this by shifting attack traffic from the corporate server to a public cloud provider. Furthermore, comparing to hardware defense, software load balancers with cloud off-loadings provide efficient and cost-effective protection. [This post][5] on AWS might be helpful when learning how to encrypt the connection between clients and the load balancer and from the load balancer to your application container running in an ECS cluster. We also need to keep in mind that security is better automated to save time and money when scaling up the system.

* Data Protection

Data has different levels of sensitivity, and we should choose the protection mechanism based on it. Besides, data protection has two stages that we need to consider. One is when the data is at rest like files in S3, and the other one is when the data is in transit like emails between servers. The best practice here is again automation, so we keep people away from data.

* Incident Response

Intervene, investigate, and deal with all the security events actively. Learn from what has happened and update the framework all the time.

* Identity & Access Management (IAM)

Manage all-user identity and access actively. One way to do this is to follow the **principle of least privilege**. This means that we provide only enough information for the users to complete their tasks. We start by giving them the minimum access and grant additional only as necessary.

There are three ways we can use IAM to set access.

	* **Users**
We can create users and assign them very granular permission sets. For example, administrators need console access, and end-users who need content access. A system can also be a user that has programmatic access to data.  


	* **IAM roles**
IAM roles can obtain a set of temporary security credentials to make API calls. If a company has multiple accounts for different projects, they can apply IAM roles to users from another AWS account.


	* **Federated users**
Suppose a company has existing identity management solutions that support SAML 2.0 or create one using AWS’s federation samples. In that case, they can let those identities access the AWS cloud instance without creating an IAM user for each user.


# AWS Compliance Program
In my opinion, this is one of the most impressive services from AWS. It can answer you **if your industry allows AWS for processing and storing data**. For example, highly sensitive patient data in the USA needs to fulfill [Health Insurance Portability and Accountability Act (HIPPA) compliance][6].

I randomly clicked on other programs in other regions, and found the service can be very convenient. As you can see in AWS compliance website, the programs are divided by region of the world. There is still a lot of business that needs to be covered, but it can be beneficial if yours falls in the established ones. For example, I randomly clicked into the [AWS outsourcing guidelines with the Association of Banks in Singapore][7]. They provide a minimum standard of controls and procedures expected by the financial industry in Singapore. Furthermore, they list out the  [approved auditors](https://www.abs.org.sg/docs/library/contact-details-auditors.pdf)  to perform the audit for AWS’ OSPAR.

# Web App Firewall (WAF)
* Serve as usual web firewall
* Protect apps from exploits that could force the app to use excessive resources
* Improve web traffic visibility
WAF monitors the traffic and offers comprehensive logging for use in security automation, analytics, or auditing purposes.
* Easily deploy with Amazon CloudFront and API Gateway


# AWS Shield
* Deal with **Distributed Denial of Service (DDoS) Attack**

This kind of attack tries to make a machine or network resource unavailable temporarily or indefinitely by making excessive repeated access requests. AWS Shield provides detection and automatic mitigations to minimize the effects of a DDoS attack.
* Two tiers of protection and cost
* **Standard tier** (default)
* **Advanced tier**

Shield Advanced provides higher level protections with a 24/7 response team, network and transport layer protections, and automated application traffic monitoring. Shield Advanced also offers financial protection against DDoS related spikes for charges for EC2, elastic load balancers, CloudFront, and Route 53.

# Amazon Inspector
This is an automated security **assessment service** for applications deployed on AWS. The detailed reports can help the security team check for unintended vulnerabilities.

# Amazon Trusted Advisor
* AWS best practices categories: cost optimization, performance, security, fault tolerance, and service limits.
* Based on the best practices, Amazon Trusted Advisor scans and provides **action recommendations**.
* 7 core Trusted Advisor checks
	* S3 bucket permissions
	* security groups
	* specific ports unrestricted
	* IAM use
	* MFA on root account

        AWS gives the option of Multi-Factor Authentication (MFA) to protect accounts. It requires users to sign in with their username and password, and an authentication code from AWS MFA device.

  * EBS public snapshots

    Snapshots are a way to back up with less time and storage. Only the blocks on the device that have changed after the most recent snapshot are saved.
    We can back up data on Amazon Elastic Block Store (EBS) volumes to Amazon Simple Storage Service (S3) by taking point-in-time snapshots.

  * RDS public snapshots

    Relational Database Service also provides back up services.

  * service quotas

    Each AWS account has default quotas. Along with looking up the quota values, we can also request a quota increase from the Service Quotas console. Before I knew this, I had issue launching instances in my region because I was not aware of these quotas.

# GuardDuty
* **Threat detection**
* Monitor for malicious activity and alert through CloudWatch
* Easy deployment


[1]: [Application](https://aws.amazon.com/research-credits/)
[2]: [AWS Certified Cloud Practitioner](https://aws.amazon.com/certification/certified-cloud-practitioner/)
[3]: [Introduction to AWS for Newbies - AWS Newbies](https://awsnewbies.com/)
[4]:https://avinetworks.com/what-is-load-balancing/
[5]:https://aws.amazon.com/blogs/containers/maintaining-transport-layer-security-all-the-way-to-your-container-using-the-application-load-balancer-with-amazon-ecs-and-envoy/
[6]:https://aws.amazon.com/compliance/hipaa-compliance/
[7]:https://aws.amazon.com/compliance/OSPAR/
