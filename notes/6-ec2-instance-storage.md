# EC2 Instance Storage

## EBS Volume
- Elastic Block Store
- network drive you can attach to an instance
- Allows instance to persist data even after termination
- Can only be mounted to one instance at a time
- bound to specific availability zone

Free tier: 30 GB of free EBS storage

Communicates to instance over network
Latency

Can be detached from instance attached to another one quickly

Can move to other AZ by making a snapshot

Billed for provisioned capacity
can increase capacity over time

EBS volume can only be attached to single EC2 instance

Can choose to terminate EBS volume when EC2 instance is terminated

## EBS Snapshots

- Snapshots can be used to
  - restore an EBS volume that has been terminated
  - Copy EBS volumes across AZ regions
- Recommended to detach volume before creating a snapshot

## AMI Overview

- AMI
  - AWS Machine Image
  - A template for launching EC2 instances
  - a customization of an EC2 Instance
  - Add your own software, configuration, OS, and monitoring and bundle into the machine image
  - Faster boot because all software is pre-packaged
  - AMI are built for a specific region
  - can be copied across regions

- PUblic AMI
  - provided by AWS

- Your Custom AMIs

- AMI from AWS Marketplace

Practice steps
- Start EC2 instance
- Customize EC2 instance
- Stop instance
- Build an AMI
- Launch other instances from AMI

---

## EC2 Instance Store

Hard drive storage disk drive that lives on same physical computer as the EC2 instance

- Better I/O performance
- EC2 Instance store lose their storage if they are stopped
- Good for buffer / cache / scratch data / temporary content

- Important to back up and replicate EC2 instance store

- EC2 Instance store can have very high I/O
