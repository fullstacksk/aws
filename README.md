#AWS Notes 
### 1. Tour of Aws Console
---
IAM - Identity Access Management



## AWS CloudShell: Region Availability
It is not yet available in all regions, and you can find the region list here:-

 [click here to check the list](https://docs.aws.amazon.com/cloudshell/latest/userguide/faq-list.html#regions-available)

##User Groups
> A user group is a collection of IAM users. Use groups to specify permissions for a collection of users.

##IAM Users
> An IAM user is an identity with long-term credentials that is used to interact with AWS in an account.

## IAM Roles
> An IAM role is an identity you can create that has specific permissions with credentials that are valid for short durations. Roles can be assumed by entities that you trust.

#IAM Security Tools
---
### IAM Credential Report (Account Level)
> A report that lists all your account's users and the status of their various credentials

###IAM Access Advisor (User Level)
> Access advisor the service permissions granted to a user and when those services were last accessed.

###IAM Guidelines & Best Practices
---

- Don't use the root account except for AWS account setup

- One physical user = One AWS user

- Assign users to groups and assign permissions to groups

- Create a strong password policy

- Use and enforce the use of Multi Factor        Authentication (MFA)

- Create and use Roles for giving permissions to AWS services

- Use Access Keys for Programmatic Access (CLI / SDK)

- Audit permissions of your account with the IAM Credentials Report

- Never share IAM users & Access Keys

##IAM Section - Summary
---

- **Users:** mapped to a physical user, has a password for AWS Console

- **Groups:** contains users only

- **Policies:** JSON document that outlines permissions for users or groups

- **Roles:** for EC2 instances or AWS services

- **Security:** MFA + Password Policy

- **Access Keys:** access AWS using the CLI or SDK

- **Audit:** IAM Credential Reports & IAM Access Advisor

# Amazon EC2
---

- EC2 is one of the most popular of AWS' offering

- EC2 = Elastic Compute Cloud = Infrastructure as a Service

- It mainly consists in the capability of:

- Renting virtual machines (EC2)

- Storing data on virtual drives (EBS)

- Distributing load across machines LB)

- Scaling the services using an auto-scaling group (ASG)

-  Knowing EC2 is fundamental to understand how the Cloud works

## EC2 sizing & configuration options

> Operating System (OS): **Linux**, **Windows** or **Mac OS**

- How much compute power & cores (CPU)

- How much random-access memory (RAM)

- How much storage space:

- Network-attached (EBS & EFS)

- hardware (EC2 Instance Store)

- Network card: speed of the card, Public IP address

- Firewall rules: security group

- Bootstrap script (configure at first launch): EC2 User Data

## EC2 User Data

- It is possible to bootstrap our instances using an EC2 User data script.

- bootstrapping means launching commands when a machine starts

- That script is only run once at the instance first start

- EC2 user data is used to automate boot tasks such as:

- Installing updates

- Installing software

- Downloading common files from the internet

- Anything you can think of

- The EC2 User Data Script runs with the root user

## EC2 instance types: example

| Instance | vCPU |Mem (GiB) |Storage |NetworkPerformance|EBS Bandwidth (Mbps)|
|----------|------|----------|--------|---|---|
| t2.micro | 1    |   1      |EBS-Only|Low to Moderate| - |  
|t2.xlarge|4|16|EBS-On|Moderate| - |
|c5d.4xlarge|16|32|1x400 NVN SSD|Up to 10 Gbps|4,750|
|r5.16xlarge|64|512|EBS Only|20 Gbps|13,600|
|m5.8xlarge|32|128|EBS Only|10 Gbps|6,800|



>**t2.micro is part of the AWS free tier (up to 750 hours per month)**

## EC2 Instance Types - Overview

- You can use different types of EC2 instances that are optimised for different use cases 
[Visit thelink](https://aws.amazon.com/ec2/instance-types/)

    - Compute Optimized
    - General Purpose
    - Memory Optimized
    - Accelerated Computing
    - Storage Optimized


> AWS has the following naming convention:

**m5.2xlarge**

- **m:** instance class

- **5:** generation (AWS improves them over time)

- **2xlarge:** size within the instance class

##EC2 Instance Types - General Purpose

>Great for a diversity of workloads such as web servers or code repositories

Balance between:

- Compute

- Memory

- Networking

- In the course, we will be using the t2.micro which is a General Purpose EC2 instance

General Purpose

> General purpose instances provide a balance of compute, memory and networking resources, and can be used for a variety of diverse workloads. These instances are ideal for applications that use these resources in equal proportions such as web servers and code

## EC2 Instance Types - Compute Optimized

> Great for compute-intensive tasks that require high performance processors:

- Batch processing workloads

- Media transcoding

- High performance web servers

- High performance computing (HPC

- Scientific modeling & machine learnin

- Dedicated gaming servers

**Compute Optimized**

>Compute Oppmund mtances are ideal for compute bound applications that bene from high pertamance procesem belonging to this family as wel pertamana computing HPC) hrbuch prooming Hortloads meda transcoding ghee web servers, high modeling dedicated gaming seners and ad server egnes mane and


## EC2 Instance Types - Memory Optimized

> Fast performance for workloads that process large data sets in memory

 **Use cases:**

- High performance, relational/non-relational databases

- Distributed web scale cache stores

- In-memory databases optimized for Bl (business intelligence)

- Applications performing real-time processing of big unstructured data

**Memory Optimized**

>Menary optmand netances are designed to or fat pertama for work that pros large atata sets in memory


## Introduction to Security Groups

>Security Groups are the fundamental of network security in AWS

- They control how traffic is allowed into or out of our EC2 Instances.

- Inbound traffic

    - www

    - Security

    - EC2 Instance

- Security groups only contain allow rules

- Security groups rules can reference by or by security group

Ultimate AWS Certified Developer Associate 2021 - NEW!

Leave a rating

Your progress ✓

ShareA

Security Groups Deeper Dive

Security groups are acting as a "firewall" on EC2 instances

• They regulate:

• Access to Ports

• Authorised IP ranges - IPv4 and IPv6

Control of inbound network (from other to the instance)

• Control of outbound network (from the instance to other)

|Type|Protocol|Port Range|Source|Description|
|----|--------|----------|------|-----------|
|HTTP|TCP|80|0.0.0.0/0|test http page|
|SSH|TCP|22|122.196.149.85/32|test http page|
|Custom TCP Rule|TCP|4567|0.0.0.0/0|java app|

## Security Groups Good to know

- Can be attached to multiple instances

- Locked down to a region /VPC combination

- Does live "outside" the EC2 - if traffic is blocked the EC2 instance won't see it

- It's good to maintain one separate se city group for SSH access

- If your application is not accessible (time out), then it's a security group issue

- If your application gives a "connection refused" error, then it's an application error or it's not launched

- All inbound traffic is blocked by default

- All outbound traffic is authorised by default


### Classic Ports to know

-  22 = SSH (Secure Shell) - log into a Linux instance

-  21 = FTP (File Transfer Protocol) - upload files into a file share

-  22 = SFTP (Secure File Transfer Protocol) - upload files using SSH

-  80= HTTP - access unsecured websites
- 443 = HTTPS access secured websites

-  3389 = RDP (Remote Desktop Protocol) - log into a Windows instance