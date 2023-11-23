# Amazon EC2
- EC2 is one of the most popular service
- EC2 = Elastic Compute Cloud = Infrastructure as a Service
- It mainly consists in the capability of:
  - Renting Virtual Machines (EC2)
  - Storing data on virtual drives (EBS)
  - Distrubuting load across machines (ELB)
  - Scaling the services usign an auto-scaling group (ASG)
- Knowing EC2 is fundamental to understand how the cloud works
  
## EC2 sizing and configuration options
- Operating system (OS): Linux, Windows or MacOS
- How much compute power and cores (CPU)
- How much random-access memory (RAM)
- How much storage space:
  - Network-attached (EBS and EFS)
  - Hardware (EC2 Instance Store)
- Network card: speed of the card, Public IP address
- Firewall rules: security group
- Bootstrap script (configure at first launch): EC2 user data

## EC2 User Data
- It is posssible to bootstrap our instances using an EC2 User data script
- Bootstrapping means launching commands when a machine starts
- That script is only run once at the instance first start
- EC2 user data is used to automate boot tasks such as:
  - Installing updates
  - Installing software
  - Downloading common files from the internet
  - Anything you can think of
- The EC2 User Data script runs with the root user

## EC2 Instance Types
- AWS has the following naming conventions
  - m5.2xlarge
    - m: instance class
    - 5: generation (AWS improves them over time)
    - 2xlarge: size within the instance class

### General purpose
- Great for a diversity of workloads such as web servers or code repositories
- Balance between:
  - Compute
  - Memory
  - Networking
  
### Compute Optimized
- Great for compute-intensive tasks that require high performance processors:
  - Batch processing workloads
  - Media transcoding
  - High performance web servers
  - High performance computing (HPC)
  - Scientific modeling and machine learning
  - Dedicated gaming servers

### Memory Optimized
- Fast performance for workloads thath process large data sets in memory
- Use cases:
  - High performance, relational/non-relational databases
  - Distributed web scale cache stores
  - In-memory databases optimized for BI (business intelligence)
  - Applications performing real-time processing of big unstructured data

### Storage Optimized
- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
- Use cases:
  - High frequency online transactions processing (OLTP) systems
  - Relational and NoSQL databases
  - Cache for in-memory databases (like Redis)
  - Data warehousing applications
  - Distributed file systems

## Introduction to Security Groups
- Security Groups are the fundamental of network security in AWS
- They control how traffic is allowed into or out of our EC2 Instances.
- Security groups only contain allow rules
- Security groups rules can reference by IP or by security group

- **Security Groups are acting as a "firewall" on EC2 instances**
- They regulate:
  - Access to Ports
  - Authorised IP ranges - IPv4 and IPv6
  - Control of inbound network (from other to instance)
  - Control of outbound network (from the instances to other)

- Good to know about Security Groups
  - Can be attached to multiple instances
  - Locked down to a region/VPC combination
  - Does live "outside" the EC2 - if traffic is blocked the EC2 instance won't see it
  - It's good to maintain one separate security group for SSH access
  - **It's good to maintain one separate security group for SSH access**
  - If your application is not accessible (time out), then it's a security group issue
  - If your application fives a "connection refuse" error, then it's an application error or it's not launched
  - All inbound traffic is blocked by default
  - All outbund traffic is authorised by default

## EC2 Instances Purchasing Options
- **On-Demand Instances** short workload, predictable pricing, pay by second
- **Reserved (1 and 3 years)**
  - Reserved Instances - long workloads
  - Convertible Reserved Instances - long workloads with flexible instances
- **Savings Plans (1 and 3 years)** - Commitment to an amount of usage, long workload
- **Spot Instances** - Short workloads, cheap, can lose instances (less reliable)
- **Dedicated Hosts** - book an entire physical server, control instance placement
- **Dedicated Instances** - no other customers will share your hardware
- **Capacity Reservations** - reserve capacity in a specific AZ for any duration

### EC2 On Demand
- Pay for what you use:
  - Linux or Windows - billing per second, after the first minute
  - All other operating systems - billing per hour
- Has the highest cost but no upfront payment
- No long-term commitment
- **Recommended for short-term and un-interrumped workloads, where you can't predict how the application will behave**

### EC2 Reserved Instances
- Up to 72% discount compared to On-Demand
- You reserve a specific instance attributes (Instance Type, Region, Tenancy, OS)
- **Reservation Period** - 1 year (+ discount) or 3 years (+++ discount)
- **Payment Options** - No Upfront (+), Partial Upfront (++), All upfront (+++)
- **Reserved Instance's scope** - Regional or Zonal (reserve capacity in an AZ)
- Recommended for steady-state usage applications (think database)
- You can buy and sell in the Reserverd Instance Marketplace

### Convertible Reserved Instance
- Can change the EC2 instance type, instance family, OS, scope and tenancy
- Up to 66% discount

### EC2 Savings Plans
- Get a discount based on long-term usage (up to 72% - Same as RIs)
- Commit to a certain type of usage ($10/hour for 1 or 3 years)
- Usage beyond EC2 Savings Plans is billed at the On-Demand price

- Locked to a specific instance family and AWS regions (e.g: M5 in us-east-1)
- Flexible across:
  - Instance Type
  - OS
  - Tenancy

### EC2 Spot Instances
- Can get a discount of up to 90% compared to On-Demand
- Instances that you can "lose" at any point of time if your max price is less than the current spot price
- The **MOST cost-efficient** instances in AWS

- **Useful for workloads that are resilient to failiure**
- **Not suitable for critical jobs or databases**

### EC2 Dedicated Hosts
- A physical server with EC2 instance capacity fully dedicated to your use
- Allow you address compliance requirements and use your existing server-bound software licences (per-socketm per-core, pe--VM software licences)
- **Purchasing Options**:
  - On-demand - pay per second for active Dedicated Host
  - Reserved - 1 or 3 years (No Upfront, Partia Upfront, All Upfront)
  - The most expensive option
- Useful for software that have complicated licensing model (BYOL - Bring Your Own Licence)
- Or for companies that have strong regulatory or compliance needs

### EC2 Dedicated Instances
- Instances run on hardware tath's dedicated to you
- May share hardware with other instances in same account
- No control over instance placement (can move hardware after Start/Stop)

### EC2 Capacity Reservations
- Reserve On-Demand instances capacity in a specific AZ for any duration
- No time commitment (create/cancel anytime), no billing discounts
- You always have access to EC2 capacity when you need it
- Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ


