# EC2 Instance Storage

## EBS Volume
- Elastic Block Store
- network connected hard drive you can attach to an instance
- Allows instance to persist data even after termination
- Can only be mounted to one instance at a time
- bound to specific availability zone

Uses
- database storage
- streaming workloads
- big data applications
- log processing

- Free tier: 30 GB of free EBS storage

- Communicates to EC2 instance over network
- low latency 
- Must live in same AZ as EC2 instance

- Can be detached from instance attached to another one quickly
- Can move to other AZ by making a snapshot
- can increase capacity over time
- EBS volume can only be attached to single EC2 instance
- Can choose to terminate EBS volume when EC2 instance is terminated

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

---

## EBS Volume Type

### General Purpose SSD

- can be used as boot volumes (storing the OS of the EC2)

gp2/gp3
- general perpose SSD volume
- wide variaty of workloads
- virtual desktops
- dev / test environments

gp3
- baseline of
  - 3000 IOPS
  - throughput of 125 MiB/s
- Can increase (independently) to
  - 16000 IOPS
  - 1000 MiB/s

---

### Provisioned IOPS
- Critical business app
- needs sustained IOPS performance
- more than 16000 IOPS
- Good for database workloads
- Support EBS multi-attach
- can be used as boot volumes (storing the OS of the EC2)

io1 / io2 (4GiB - 16TiB)
- Highest performance SSD volumes for mission-critical low latency, high-throughput
- Max PIOPS
  - 64,000 for Nitro EC2 instance
  - 32,000 for other
- io2
  - has more durability
  - more IOPS per GiB at same price as io1

- io2 Block Express
  - sub-milliseccond latency
  - Max PIOPS - 256,000
  - 1000 IOPS per GiB

---

### Hard Disk Drives (HDD)

- Cannot be boot volume
- 125 MiB 16 TiB

- Throughput optimized HDD (st1)
  - low cost
  - used for Big data, data warehouses, log processing
  - Max throughput - 500 MiB/s
  - Max IOPS - 500

- Cold HDD (sc1)
  - lowest cost
  - for less frequently accessed workloads
  - Max throughput - 250 MiB/s
  - Max IOPS - 250

Only gp2 / gp3 and io1/io2 can be used as boot volumes
- Boot volume stores the root OS of the EC2 instance

---

## EBS Multi-Attach

only available with io1 / io2 

- Attach same EBS volume to multiple EC2 instances
- must be in the same AZ
- each instance has read / write permission to volume
- Used for
  - to achieve higher application availability in clustered applications
  - When app must manage concurrent write / operations
- must use a file system that is cluster aware

---

## EFS - Elastic File Systtem

- A Managed 'Network File System' (NFS)
- Can be mounted on many EC2 instances **across many AZs**
- High availability
- scalability
- expensive - 3x cost of gp2

- Use case
  - content management
  - web serving
  - data sharing
  - Wordpress

- Uses NFSv4.1 protocol
- Uses security group to control access
- Only compatible with Linux AMIs
- Encryption at rest using **KMS**

- Uses a POSIX file system (~Linux) with a standard file API

**Selling Point**
- EFS scales automatically
- pay only for what you use
- no capacity planning needed

---

## EFS - Performance and Storage Classes

- Supports 1000s of concurrent NFS clients
- 10 GB+ throughput

Performance modes
- 1). general purpose - lower latency
  - web servers, CMS
- 2). Max I/O - higher latency, throughput, highly parallel
  - big data, media processing

Throughput mode
  - Bursting
    - 50 MiB/s for each TB
    - burst up to 100 MiB/s

  - Provisioned
    - set throughput regardless of storage size
    - can set high througput even if we have small storage

Storage Tiers
  - standard
    - frequent file access
  - infrequent access
    - low price to store files
    - cost to retrieve files

---

## EFS Demo

- Create an EFS
- Create new security group to EFS
- Attach to EFS

- Create 2 EC2 instances
- Create new security group for EC2
  - attach to both

- update security setting for security group attached to EFS
  - allow inbound from EC2 to EFS
  - new inbound rule
    - add type - NFS
    - source - the security group attached to EC2

- SSH into 2 EC2 instances

- in each EC2 instance
  - install amazon efs utils
  - create efs directory
  - mount efs drive using EFS mount helper
  - within efs drive create a file
  - write to the file
  - file is accessible from both instances

## EBS vs EFS

Elastic Block Storage vs Elastic File Storage

EBS volumes
- only attached to single instance at a time
- except io1 / io2 - can be attached to many instances in same AZ
- io1 - can increase IO independently
- by default root EBS volume of instance is terminated when the EC2 instance is terminated

To migrate EBS volume across AZ
- take snapshot while EBS is not running or not taking a lot of traffic
- restore the snapshot in another AZ

EFS
- Allows for mounting 100s of EC2 instances across AZs
- Only for linux instances (uses POSIX file system)
- EFS is more expensive than EBS
- higher latency
- Can leverage infrequent access for cost savings
  - move less used files to separate EFS store

Instance Store
- highest I/O
- data is destroyed when EC2 instance is stopped / terminated











