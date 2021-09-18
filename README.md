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

## What's an EBS Volume?

> An EBS (Elastic Block Store) Volume is a network drive you can attach to your instances while they run

- It allows your instances to persist data, even after their termination

- They can only be mounted to one instance at a time (at the CCP level)

- They are bound to a specific availaty zone

- Analogy: Think of them as a "network USB stick"

- Free tier: 30 GB of free EBS storage of type General Purpose (SSD) or Magnetic per month

- It's a network drive (i.e. not a physical drive)

- It uses the network to communicate the instance, which means there might be a bit of latency

- It can be detached from an EC2 instance and attached to another one quickly

- It's locked to an Availability Zone (AZ)

- An EBS Volume in us-east-la cannot be attached to us-east-ib

- To move a volume across, you first need to snapshot it

- Have a provisioned capacity (size in GBs, and IOPS)

- You get billed for all the provisioned capacity

- You can increase the capacity of the drive over time

## EBS Delete on Termination attribute


>Controls the EBS behaviour when an EC instance terminates

- By default, the root EBS volume is deleted (attribute enabled)

- By default, any other attached EBS volume is not deleted (attribute disabled)

- This can be controlled by the AWS console / AWS CLI

- Use case: preserve root volume when instance is terminated

## EBS Snapshots

- Make a backup (snapshot) of your EBS volume at a point in time

- Not necessary to detach volume to do snapshot, but recommended

- Can copy snapshots across AZ or Region

# AMI Overview
---

AMI = Amazon Machine Image

AMI are a customization of an EC2 instance

- You add your own software, configuration, operating system, monitoring... • Faster boot / configuration time because all your software is pre-packaged

- AMI are built for a specific region (and can be copied across regions)

- You can launch EC2 instances from:

- A Public AMI: AWS provided

- Your own AMI: you make and maintain them yourself

- An AWS Marketplace AMI: an AMI someone else made (and potentially sells)

## AMI Process (from an EC2 instance)

- Start an EC2 instance and customize it

- Stop the instance (for data integrity)

- Build an AMI - this will also create EBS snapshots

- Launch instances from other AMIS

## EC2 Instance Store

- EBS volumes are network drives with good but "limited" performance

- If you need a high-performance hardware disk, use **EC2 Instance Store**

- Better I/O performance

- EC2 Instance Store lose their storage if they're stopped (ephemeral)

- Good for buffer / cache/ scratch data / temporary content

- Risk of data loss if hardware fails

- Backups and Replication are your responsibility

## EBS Volume Types

> EBS Volumes come in 6 types

- gp2/gp3 (SSD): General purpose SSD volume that balances price and performance for a wide variety of workloads

- iol /io2 (SSD): Highest-performance SSD volume for mission-critical low-latency or high-throughput workloads

- stl (HDD): Low cost HDD volume designed for frequently accessed, throughput intensive workloads

- scl (HDD): Lowest cost HDD volume designed for less frequently accessed workloads

- EBS Volumes are characterized in Size | Throughput | IOPS (I/O Ops Per Sec)

- When in doubt always consult the AWS documentation - it's good!

- Only gp2/gp3 and io1/io2 can be used as boot volumes

## EBS Volume Types Use cases General Purpose SSD

- Cost effective storage, low-latency

- System boot volumes, Virtual desktops, Development and test environments

- 1 GiB 16 TiB

- gp3:
    - Baseline of 3,000 IOPS and throughput MiB/s

    - Can increase IOPS up to 16,000 and throughput up to 1000 MiB/s independently

- gp2:

    - Small gp2 volumes can burst IOPS to 3,000

- Size of the volume and IOPS are linked, max IOPS is 16,000

- 3 IOPS per GB, means at 5,334 GB we are at the max IOPS

## EBS Volume Types Use cases Provisioned IOPS (PIOPS) SSD

- Critical business applications with sustained IOPS performance

- Or applications that need more than 16,000 IOPS

- Great for databases workloads (sensitive to storage perf and consistency)

- iol/io2 (4 GiB - 16 TiB):

    - Max PIOPS: 64,000 for Nitro EC2 insta & 32,000 for other

    - Can increase PIOPS independently fron, storage size

    - io2 have more durability and more IOPS per GiB (at the same price as iol)

- io2 Block Express (4 GiB-64 TiB):

    - Sub-millisecond latency

    - Max PIOPS: 256,000 with an IOPS:GIB ratio of 1,000:1

- Supports EBS Multi-attach
