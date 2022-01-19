# Create EC2 Instance

launch EC2 instance running linux

- Pick a Machine image
  - operating system
  - version
  - hardware

- Pick instance type
  - picking a size (CPU, memory, storage, network capabilities)

- Number of instances
- Network configuration
- IAM roles
- Declare "User Data"
  - To be run on machine boot

- Select storage capacity
- Add tags
- Configure security groups
  - Open ports for various connection types
    - SSH, HTTP, HTTPS, TCP, UDP, SMTP
  - specify allowed IP addresses

---

## EC2 Instance Types Basics

[https://aws.amazon.com/ec2/instance-types/](https://aws.amazon.com/ec2/instance-types/)

m5.2xlarnge

m - instance class
5 - generation
2xlarnge - size within the instance class

---

### EC2 Instance Types

General purpose
- web servers
- code repositories
- ie. t2.micro

Compute optimized
- Batch processing workloads
- Media transcoding
- High performance web servers
- High performance computing (HPC)
- Scientific modeling & machine learning
- Dedicated gaming servers

Memory Optimized
- fast performance
- High performance, relational/non-relational databases
- Distributed web scale cache stores
- In-memory databases optimized for BI (business intelligence)
- Applications performing real-time processing of big unstructured data

Storage Optimized
- storage intensive tasks
- High frequency online transaction processing (OLTP) systems
- Relational & NoSQL databases
- Cache for in-memory databases (for example, Redis)
- Data warehousing applications
- Distributed file systems

All Instances compared 
[https://instances.vantage.sh](https://instances.vantage.sh)

---

## Intro To Security Groups

- Firewall on EC2 instance
- Control how traffic is allowed into and out of EC2 instances
- All inbound traffic blocked by default
- All outbound traffic is authorized by default

regulate
- access to ports
- authorize IP ranges IPv4 / IPv6
- control of inbound network
- control of outbound network

Security Group
- can be attached to multiple instances
- locked down to  region / VPC combination
- lives outside of the EC2 instance
  - if a traffic is blocked, EC2 instance will not register that traffic

Best Practice
- Maintain separate security group for SSH access

- If app is not accessible, most likely a security group issue

- If application gives "connection refused" error
  - application error
  - application not launched

Can reference a security group in a security group rule
- Can specify traffic is authorized from resource in particular security group

---

## Ports to Know

Can specify ports instance Will accept traffic from

- SSH - 22 - Secure Shell - log into a Linux instance
- FTP - 21 - File transfer protocol - upload files into a file share
- SFTP - 22 - Secure File Transfer Protocol - uploads files using SSH
- HTTP - 80 - Access unsecured websites
- HTTPS - 443 - Access secured websites
- RDP - 3389 - Remote Desktop Protocol - log into Windows instance

---

## Security Groups

Security Groups Tab
- Can view settings for a security group
- Inbound rules
- Outbound rules

---

## SSH

Allows us to connect to, control remote machine from command line

CLI utility to be useed by Mac, Linux, or Windows >=10
for Windows < 10 - use putty

EC2 Instance Connect
can be used for all operating systems

---

## Steps to SSH 

1. Move .pem file to proper location. Could be in project directory

2. Update permissions of .pem file

Currently has permission 0644
Change to 0400

`chmod 0400 path/to/.pem-file`

3. SSH into EC2 instance
`ssh -i path/to/.pem-file <username>@<public-ip-address>`

4. Exit
`cmd+d`

---

## SSH Troubleshooting

Connection timeout
- related to filewall
- Ensure security group has SSH enabled
- Ensure security group is assigned to EC2 instance
- If above has been addressed, could be a personal, or corporate firewall blocking the connection
- Can use EC2 Instance connect

Connection refused
- instance is reachable, but no SSH utility is running on the instance
- Try restarting the instance
- terminate the instance and create a new one - use Amazon Linux 2

Permission denied
- using the wrong security key or not using a security key
- using the wrong user - user should be ec2-user for Amazon Linux 2 EC2 instance

- EC2 instance could be stopped or restarted, changing the public IP

- Connect using EC2 Connect instead

- EC2 Instance comes with aws cli instanned

## EC2 Instance Connect

Can connect from instance window

## EC2 Instance Demo Roles

`whoami` - see user logged in

## Best Practice
- Never want to attach user credentials directly to a EC2 instance
  - never enter personal public / private access keys into EC2 instance
- **Attach IAM Role to EC2 instance instead**
  - within EC2 instance - Actions > Security > Modify IAM Role

---

## EC2 Instance Launch Types (purchasing options)

### On Demand Instance
- For short workload
- predictable pricing
- Linux / Windows - billing per second after first minute
- Other OSs - billing per hour
- High cost
- No upfront payment
- No long-term commitment
- Recommended for short term and uninterrupted workloads

### Reserved Instances
- 75% discount compared to on-demand
- Can be used for
  - 1 year
  - 3 years
- Can purchase
  - no upfront
  - partial upfront
  - all upfront
- Must specify instance type in beginning
- can get cost savings if know you will use an instance for long term
  - Reserved Instances - long workloads
- Recommended if you know application will be in a steady state

### Convertable Reserved Instance
- 54% discount
- can change instance type over time
- must commit from 1 - 3 years


### Scheduled Reserved Instances
- depricated
- reserved on a schedule, hourly, daily, etc...
- Have been depricated
- must commit from 1 - 3 years

### Spot Instances
- Can be 90% discount
- short workloads
- cheap
- price can change over time
- best for workloads that resilient to failure
  - data analysis
  - batch jobs
  - image processing
  - distributed workloads
- not recommended for critical workload or database

### Dedicated Host
- Book entire physical server
- control instance placement
- can help address complience requirements
- reduce costs by allowing you to use existing server-bound software licenses
- 3 year reservation

### EC2 Dedicated Instances
- Running on hardware that is dedicated to you
- may share hardware with other instances in same account
- per instance billing







