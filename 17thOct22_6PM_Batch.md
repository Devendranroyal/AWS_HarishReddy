# AWS_HarishReddy
# Cloud Computing
  Cloud computing is nothing but delivering IT infrastructure like, compute, storage, networking
  etc.. over the internet. It offers a pay-as-you-go model.
  
# Benefits of cloud computing
1. Cost
  a. No upfront investment required, you pay as you go
  b. You get world class infrastructure for low cost.
2. Accessibility
  a. You can access cloud services from anywhere.
3. Agility
  a. We can get our IT resources within a few minutes.
4. Flexibility
  a. If you have changes in terms of capacity planning you can always upsize or
     downsize your infrastructure.
5. Global Scale
  a. You can quickly scale your infrastructure to any geographical location.
6. Security
  a. Cloud computing is secure; both cloud providers and cloud consumers are
     responsible.
7. Maintenance
  a. You do not have to spend time on data centers, and its maintenance.

# Virtual Machine
1. Virtual machine is a software driven server created using hypervisors.
2. Virtual machine will have its own operating system along with its own allocations CPU,
Memory, Dick and Network cards.

# AWS Global Infrastructure
1. Regions
  a. Region is a geographical location where AWS has datacenters
  b. There are about 20+ regions in AWS as of today.
2. Availability Zone (AZs)
  a. Each region is comprised of two or more availability zone
3. Edge locations
  a. It is a network of cache servers.
  
# AWS Account Sign Up
https://aws.amazon.com/free

1. Email id (for example gmail)
2. Your personal details
3. Address.
4. A credit or debit card is required (verification process)
5. PAN card (Optional, no need to provide)
6. Support plan ( Basic Support that is free)

Note: It may take few minutes to 24 hours for getting aws account activated.

# AWS Solutions Architect Associate
# EC2 (Elastic Compute Cloud)
EC2 is a virtual server in the cloud, it offers a wide range of options with different operating
systems and different computer configurations.
1. We wanted to run a website on an EC2 instance.
2. How to decide about CPU/Memory/Disk?
3. For now we will go with freetier options.

# Launch EC2 Instance
Give name, select key pair, make all traffic and create instances.

# Connect to Linux Server (EC2)
1. Select EC2 and click on connect → Connect
2. Connecting from Mac OS
  a. Open terminal
  b. ssh -i ~/Downloads/haritemp.pem ec2-user@<public-ip>
3. Connect from Windows
  a. Use powershell
i. ssh -i ~/Downloads/haritemp.pem ec2-user@<public-ip>

# Install Web server
To run a website a web server is a must, there are a wide variety of web servers available for
different technologies, we will use apache web server for our demo.
1. SSH onto the server (EC2)
2. sudo yum install httpd -y
  a. httpd is package name for apache web server.
3. sudo systemctl start httpd
4. Access apache server from the browser, apache runs on 80 port.

# EC2 Free Tier limits
1. AWS offers 750 running hours of ec2 instances per month.
2. Only t2.micro falls under free tier.
3. You are separately charged for disk (EBS Volume)
  a. 30 GB is free under the free tier.
4. Its hourly billing for some instance types and seconds billing for some instances.

# Amazon Machine Image (AMI)
It is a template which contains operating system & pre configured softwares and tools. You will
find lots of AMIs managed by AWS.

# We use custom AMIs in real time.
# Demo Create Custom AMIs
1. Launch EC2 using existing AMI
2. Install & configure your required tools
  a. sudo yum install git -y
3. Create Image from that
  a. Select EC2 → Actions → Image & Templates → Create Image → provide some
     name and create Image.
4. Delete the EC2 instance after Image is created.

# Locating Custom AMI
  EC2 Dashboard → Images → AMIs
  
# Note: AMIs are region specific, however we can copy AMIs to cross regions.
# Sharing Images
1. By default AMIs are private
2. You can share this with other aws accounts
3. You can make AMIs public (visible for all aws accounts)
# Note: AMI is not only a template it servers as a backup

# Elastic Beanstalk
It is a platform which makes deploying applications easy with few clicks. We have to choose a
platform like tomcat, it supports other platforms like java, php, docker, .Net, golan, many more.
Note: It will not expose ec2, we don’t have to worry about patching.

# EBS(Elastic Block Store)
  EBS is a highly durable, scalable block level store that is a hard disk for ec2 instance.
- Each volume we created in the background has two copies so it is highly durable.
- Scalable means performance.
- EBS is available in specific AZ. and it should be used by ec2 instances in same AZ.
- You can resize EBS volumes(We can only increase the size)

# Demo EBS & EC2
- While launching ec2 instance you get options to select 1 or more EBS volumes

# (FAQ)How do you add additional volumes for existing ec2 instances?
1. Create a new volume in the same AZ as ec2 instance.
2. From the EC2 dashboard, select volume, go to actions and attach to the right ec2
   instance.
3. SSH on to ec2 instance
  a. lsblk
  b. Create a file system on the ebs volume (otherwise we can’t use it)
    i. sudo mkfs.ext4 /dev/xvdf
  c. Create a mount point (it is nothing but a folder)
    i. sudo mkdir /jhc (you can give any name)
  d. Mount the volume on the above folder.
    i. sudo mount /dev/xvdf /jhc/
  e. Automount volume when ec2 is rebooted.
    i. For automounting we must use the /etc/fstab file.
    ii. https://www.redhat.com/sysadmin/etc-fstab
# Resize EBS volume
1. Select the volume and increase the size (from aws console)
  
# Volume performance attributes
1. IOPS (Input Output operations Per Second)
  a. IOPS represents the number of reads and writes per second.
2. Throughput
  a. Throughput represents the amount of data the application can read and write at a time.
3. Previous Generation disks(Magnetic Storage).
  a. Use this if applications are designed to perform on previous generation disks.
  
# Volume Types
https://aws.amazon.com/ebs/volume-types/
1. SSD (Solid State Disk) - This is for IOPS
  a. General Purpose SSD
    i. It is used for setting up dev/test environments
    ii. We can use it for production also if it is not critical, where you do not need
        consistent high performance.
    iii. They charge only for size
  b. Provisioned IOPS SSD
    i. It is designed for mission critical applications
    ii. Where you need consistent high performance.
    iii. They charge you for size of disk plus IOPS (costly)
2. HDD (Hard Drive Disk) - This is for throughput
  a. Throughput Optimized HDD
    i. It is used by data warehouses and big data analytics applications.
    ii. It is for frequently accessed data
  b. Cold HDD
    i. It is also for big data & data warehousing but it is for infrequently accessed data.
    ii. If you put frequently accessed data into it you have to pay more money.
3. Magnetic Storage.
# (FAQ) What is root volume?
  The volume where the operating system is installed.
# (FAQ) What are the volume types supported for root volume
  SSD & General Purpose disks are supported for root volumes.
# Note: HDD is not supported as a root volume
# (FAQ)Can we encrypt EBS volumes?
   Yes.
# (FAQ) Can we encrypt root volumes?
   Yes
#(FAQ) How do you encrypt an existing volume?
  There is no direct option, you have to create a snapshot(backup), from snapshot restore, while
  restoring enable encryption.
# EBS Snapshots
1. Snapshot is EBS volume backup.
2. EBS snapshots are stored in S3.
3. How to move a volume in one AZ to another AZ
  a. Create snapshot → Restore from a snapshot → choose your desired AZ.
# Exercise:
Create EC2 Instance with additional volume of size 50GB, volume type should be general purpose. 
Create an info.txt file on additional volume, this file should contain your name and phone number.
Migrate this volume to another region, in that region launch ec2 and to this ec2 attach the volume and verify info.txt file

# Snapshots are Incremental
EBS snapshots are incremental, only the data that got modified after the previous snapshot is backed up.

# Automate Snapshot Creation - Demo
The project requirement is to take backups every 3 hours.
Earlier this was implemented using python scripts now python is not required it can be
automated using “Data Lifecycle Manager”

# Note: DLM also supports automating AMI creation
# (FAQ) Instance Store
  1. It is ephemeral(temporary)
  2. Instead of EBS, ec2 instances can be launched with an instance store.
  3. Instance store volumes are very cheap
  4. If an ec2 instance is rebooted data on the instance store is lost.
  5. There are use cases for instance store but I do not see them used much in the projects.

# EC2 Instance Types(Certification)
  Let's take randomly one instance type
  c5a.xlarge
  c → Represents Instance Family
  5 → Represents generation (always we should use latest generation)
  a → processor ( AMD processor)
  xlarge → size of the instance
  
# EC2 Instance Families
Instance families are composed of CPU memory and network performances
1. General Purpose
  a. It offers balance of CPU, memory and network performance
  b. It is used for development, testing environments
  c. It is used for setting up web servers, medium databases, virtual desktops, etc..
2. Compute Optimized
  a. It provides a high ratio of CPU for better cost, use it for CPU intensive workloads.
  b. Web servers, batch jobs, analytics etc..
3. Storage Optimized
  a. It provides a high ratio of IOPS, it is ideal for databases and data warehouses
      where IOPS is the dominant performance attribute.
4. Memory Optimized.
  a. It offers high ratio of memory and use it for memory intensive workloads, for
     example SAP HANA(in-memory), Redis (in-memory), MemcacheD(in-memory), Hadoop Spark
5. Accelerated Computing.
  a. It is used for applications that heavily depend on graphics cards.
  
# EC2 Instance purchase options
It is important because it decides your overall cost.
We will go through different purchase options and when to use them.
1. On-Demand instance
  a. It is a highly flexible instance that you can launch/terminate at any time.
  b. You may not have a long term commitment, you may need them just for few
     hours or a few days.
  c. You are not billed when the ec2 instance is stopped.
2. Reserved Instances
  a. We have to give long term commitment like 1,3 years
  b. You get significant discounts in return for long term commitments
  c. Your bill is fixed, there is no change in that.
  d. AWS will not take reserved instances back, however you can sell them in AWS Marketplace.
  e. Payment Options
    i. No Upfront
    ii. Partial Upfront, remaining in monthly billing.
    iii. Full upfront.
3. Dedicated Hosts
  a. Dedicated hosts allows customers to BYOL (Bring Your Own License)
  b. Customers will lower costs by bringing their own license.
4. Savings Plans
  a. You should give commitment in terms of spending that is for example 10$/hour, in
     return you receive up to 72% discount
5. Spot Instances
  a. AWS allocates EC2 instance from unused capacity
  b. You get up to 90% discounts
  c. It has spot interruption, where aws takes your instance by giving 2 minutes notice
  d.There are two types of spot request
    1. One time
      a. If spot interruption occurs this is the end of request
    2. Persistent Request
      a. If spot interruption occurs the spot request will be still active, if your criteria
         matches it can launch a spot instance again.
         
# VPC (Virtual Private Cloud)
- VPC is virtual data center in AWS cloud
- VPC spans a region (example Mumbai)
- You can create multiple VPCs
- We can create a maximum 5 VPCs per region, 5 is the soft limit, if required we can
  request to increase this limit.
- No cost for VPC

# Create VPC
To create VPC we should understand CIDR (Classless Inter Domain Routing)
There are two types of CIDRs
1. IPV4 that uses 32 bits (I will cover)
  a. x.x.x.x/32
  b. Each ‘x’ represents an octet that is 8 bits
  c. /32 we can call this as a netmask
2. IPV6 that uses 128 bits (I’m not covering)

# Choosing CIDRs with best practices
1. Choose private ip range
  a. 192.168.0.0 to 192.168.255.255
  b. 172.16.0.0 to 172.31.255.255
  c. 10.0.0.0 to 10.255.255.255
2. Is this 172.15.0.0/24 in private ip space?
  a. No
3. Is this 10.20.0.0/24 in private ip space?
  a. Yes
  
# A typical network architecture for simple web application
1. Create VPC with one subnet
  a. CIDR for VPC → 10.200.0.0/24
  b. How many ips we get is 2 to the power of 8 = 256
  c. Create one subnet 10.200.0.0/24
  d. In every subnet 5 ips are blocked by aws for its internal usage.
2. Create VPC with two subnets
  a. CIDR for VPC → 10.200.0.0/24
  b. How many ips we get is 2 to the power of 8 = 256
  c. Create first subnet → 10.200.0.0/25
  d. Create second subnet → 10.200.0.128/25
3. Create VPC with three subnet with minimum 1000 ips
  a. VPC CIDR → 172.20.0.0/22 → 1024
  b. Subnet one CIDR → 172.20.0.0/23
  c. Subnet two CIDR → 172.20.2.0/24
  d. Subnet three CIDR → 172.20.3.0/24

# Note:
1. CIDR range should be between /28 and /16
2. Always use private IP range
3. Don't overlap VPC CIDRs with other VPCs and on-premise networks.

# (FAQ)What is a public subnet?
- A subnet which is configured with internet-gateway is public subnet
- A subnet that is exposed to the internet is called a public subnet.

# Internet Gateway
1. Is a VPC component that provides inbound/outbound internet connection to the subnet(s)

# Demo - Create VPC with one public subnet
1. Create VPC with 172.20.0.0/20
2. Create Subnet with 172.20.0.0/24
3. Create Internet Gateway (attach to VPC)
4. Configure internet gateway in the route table

# Few more points about internet gateway
1. Internet gateways redundant and highly scalable, it's taken care by amazon
2. Usually problems will not occur in internet gateway, even if problems occur we have nothing to do.
3. We can use only one internet gateway per VPC.

# Instance Types used in one of the projects
1. r5.2xlarge
2. m4.2xlarge
3. t3.micro

# Demo - Launch EC2 instance into above VPC
  
