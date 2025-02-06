# AWS CLF-02 exam notes

![alt text](images/aws-logo.jpg 'AWS logo')

## Seven Advantages to Cloud

- 1. Cost effective - Pay on demand
- 2. Global - Launch anywhere in the world
- 3. Secure - Cloud servvices can be secure by default
- 4. Reliable - Data backup, disaster recovery, data replication, fault tolerance
- 5. Scalable - Increae or decrease resources and services based on demand
- 6. Elastic - Automate scaling during spikes and drop in demand
- 7. Current - The underlying hardware and managed software is patched, upgraded and replaced by the cloud provider without interruption to you

## AWS Global Infrastructure

The AWS Global Infrastructure is globally distributed hardware and datacenters that are physically networked together to act as one large resource for the end customer

## Global Infrastructure

### Regions

When you choose a region there are four factors you need to consider:

1. What Regulatory Compliance does this region meet?
2. What is the cost of AWS services in this region?
3. What AWS services are available in this region?
4. What is the distance or latency to my end-users?

#### Regional Services

AWS scope their AWS Management Console on a selected Region. This will determine where an AWS service will be launched what will be seen within an AWS Service's console (you generally don't explicitly set the Region for a service at the time of creation).

#### Global Services

Some AWS Services operare across multiple regions and the region will be to "Global" - e.g, Amazon S3, CloudFront, Route53, IAM.

For these global services at the time of creation:

- There is no concept of region (IAM user)
- A single region must be explicitly chosen (S3 Bucket)
- A group of regions are chosen (CloudFront Distribution)

### Availablility Zones

- A region has multiple Availability Zones. An AZ is made up of 1 or more datacenters.
- All AZs in an AWS Region are interconnected with high-bandwidth, low-latency networking, over fully redundant, dedicated metro fiber providing high throughput, low-latency networking between
- All traffic between AZs is encrypted
- AZs are within 100lm (60 miles) of each other

### Fault Tolerance

**What is a fault domain?**
A fault domain is a section of a network that id vulnerable to damage if a critical device or system fails. The purpose of a fault domain is that if a failure occurs it will not cascade outside that domain, limiting the damage possible.

**What is a fault level?**
A fault level is a collecion of fault domains

The scope of a fault domain could be:

- Specific servers in a rack
- An entire rack in a datacenter
- An entire room in a datacenter
- The entire datacenter in a building

It's up to the Cloud Service Provider (CSPs) to define the boundaries of the domain.

Each Amazon is designed to completely **isolated** from the other Amazon Regions.

- This achieves the greatest possbile fault tolerance and stability.

Each AZ is _isolated_, but the AZs in a Region are connected through low-latency links

Each AZ is designed as an **independent failure zone**

<blockquote>A "Failure Zone" is AWS describing a Fault Domain</blockquote>

**Failure Zone:**

- AZs are physically separated within a typical metropolitan region and are located in lower risk flood plains
- Discrete uninterruptible power supply (UPS) and onsite backup generation facilities
- Data centers located in different AZs are designed to be supplied by independent substations to reduce the risk of an event on the power grid impacting more than one AZ
- AZs are all redundnatly connected to multiple tier-1 transit providers

**Multi-AZ for High Availability**
If an application is partitioned across AZs, companies are better isolated and protected from issues such as **power outages, lightning strikes, tornadoes, earthquakes, and more.**

### AWS Global Network

The AWS Global Network represent the **interconnections between AWS Global Infrastructure**, commonly referred to as the "The Backbone AWS". Think of it as a private expressway, where things can move very fast between datacenters.

- **Edge Locations**: can act as on and off ramps to the AWS Global Network
- **AWS Global Accelerator**, **AWS S3 Transfer Acceleration**: uses Edge Locations as an on-ramp to quickly reach AWS resources in other regions by traversing the fast AWS Global Network
- **Amazon Cloudfront (CDN)**: uses Edge Locations as an off-ramp, to provide at the Edge Storage and computer near the end user
- **VPC Endpoints**: ensuring your resources stay within the AWS Network and do not traverse over the public internet

## Point Of Presence (POP)

- **Points of Presence (POP)** is an intermediate location between an AWS Region and the end user, and this location could be a datacenter or collection of hardware.
- For AWS a Point of Presence is a data center owned by AWS or a trusted partner that is utilized by AWS Services related for content delivery or expediated upload.

PoP resources are:
• Edge Locations
• Regional Edge Caches

**Edge Locations** are datacenters that hold cached (copy) on the most popular files (eg. web pages,images and videos) so that the delivery of distance to the end users are reduce <br/>
**Regional Edge Locations** are datacenters that hold much larger caches of less-popular files to reduce a full round trip and also to reduce the cost of transfer fees.

**Scenario:**

- S3 Bucket (Your Origin)

1.  Edge Location & Regional Edge Cache
2.  Edge Location (left and right path)
3.  End User (left and right path)

- PoPs are live at the edge/intersection of two networks
- Tier 1 network is a network that can reach every other network on the Internet without purchasing IP transit or paying for peering.
- AWS Availability Zones are all redundantly connected to multiple tier-1 transit providers

**The following AWS Services use PoPs for content delivery or expediated upload:**

- **Amazon CloudFront** is a Content Delivery Network (CDN) service that:
- 1. You point your website to CloudFront so that it will route requests to nearest Edge Location cache
- 2. Allows you to choose an origin (such as a web-server or storage) that will be source of cached
- 3. Caches the contents of what origin would returned to various Edge Locations around the world

- **Amazon S3 Transfer Acceleration** allows you to generate a special URL that can be used by end users to upload files to a nearby Edge Location. Once a file is uploaded to an Edge Location, it can move much faster within the AWS Network to reach S3.
- 1. Once a file is uploaded to an Edge Location, it can move much faster within the AWS Network to reach S3.

- **AWS Global Accelerator can find the optimal path from the end user to your web-servers**
- 1. Global Accelerator are deployed within Edge Locations so you send user traffic to an Edge Location instead of directly to your web-application.

### AWS Direct Connect

AWS Direct Connect is **a private/dedicated connection between your datacenter, office, co-location and AWS**. <br/>
Direct Connect has two very-fast network connection options:

1.  Lower Bandwidth 50MBps-500MBps
2.  Higher Bandwidth 1GBps or 10GBps

<blockquote>A co-location (aka carrier-hotel) is a data 000 center where equipment, space, and bandwidth
are available for rental to retail customers</blockquote>

- Helps reduce network costs and increase bandwidth throughput. (great for high traffic networks)
- Provides a more consistent network experience than a typical internet- based connection. (reliable and secure)

## Direct Connect Locations

- Direct Connect Locations are trusted partnered datacenters that you can establish a dedicated high speed, low-latency connection from your on-premise to AWS.
- eg: You would use the AWS Direct Connect service to order and establish a connection to a company datacenter

### Local Zones

- Local Zones are datacenters located very close to a densely populated area to provide single-digit millisecond low latency performance (eg. 7ms) for that area.
  **The purpose of Local Zone is the support highly-demanding applications sensitive to latencies:**
- 1. Media & Entertainment
- 2. Electronic Design Automation
- 3. AdTech
- 4. Machine Learning

<blockquote>To use Local Zones you need to Opt-in</blockquote>

### Wavelength Zones

- AWS Wavelength Zones allows for **edge-computing on 5G Networks**. Applications will have **ultra-low latency** being as close as possible to the users
- AWs has paretnered with various Telecom companies to utilize their 5G networks (Verizon, KDDI, Vodafone)

**Scenario:**
You create a Subnet tied to a Wavelength Zone and then you can launch Virtual Machines (VMs) to the edge of the targeted 5G Networks.

### Wavelength Zones

**What is Data Residency?**
The physical or geographic location of where an organization or cloud resources reside.

**What is Compliance Boundaries?**
A regulatory compliance (legal requirement) by a government or organization that describes where data and cloud resources are allowed to reside

**What is Data Sovereignty?**
Data Sovereignty is the jurisdictional control or legal authority that can be asserted over data because it's physical location is within jurisdictional boundaries

**For workloads that need to meet compliance boundaries strictly defining the data residency of data and cloud resources in AWS you can use:**

- 1. **AWS Config** is a Policy as Code service. You can create rules to continuous check AWS resources configuration. If they deviate from your expectations you are alerted or AWS Config can in some cases auto-remediate.
- 2. **IAM Policies** can be written explicitly deny access to specific AWS Regions. A Service Control Policy (SCP) are permissions applied organization wide.
- 3. **AWS Outposts** is physical rack of servers that you can put in your data center. Your data will reside whenever the Outpost Physically resides

### GovCloud (US)

**What is GovCloud?**
A Cloud Service Provider (CSP) generally will offer an isolated region to run FedRAMP workloads.

- AWS GovCloud Regions allow customers to host sensitive Controlled Unclassified Information and other types of regulated workloads.

### Sustainability

**THE CLIMATE PLEDGE**
Amazon co-founded the Climate Pledge to achieve Net-Zero Carbon Emissions by 2040 across all of Amazon's business (this includes AWS)

**AWS Cloud's Sustainability goals are composed of three parts:**

1. Renewable Energy
   - AWS is working towards having their AWS Global Infrastructure powered by 100% renewable energy by 2025.<br/>
2. Cloud Efficiency
   - AWS's infrastructure is 3.6 times more energy efficient than the median of U.S. enterprise data centers surveyed.<br/>
3. Water Stewardship

- Direct evaporative technology to cool our data center
- Use of non-potable water for cooling purposes (recycled water)
- On-site water treatment allows us to remove scale-forming minerals and reuse water for more cycles
- Water efficiency metrics to determine and monitor optimal water use for each AWS Region
  <br/>
  AWS purchases and retires environmental attributes to cover the non-renewable energy for AWS Global Infrastructure:
  • Renewable Energy Credits (RECs)
  • Guarantees of Origin (GOs)

### AWS Ground Station

**AWS Ground Station** is a fully managed service that lets you control satellite communications, process data, and scale your operations without having to worry about building or managing your own ground station infrastructure

Use cases for Ground Station:

- weather forecasting
- surface imaging
- communications
- video broadcasts

To use Ground Station:

- You schedule a Contact (select satellite, start and end time, and the ground location)
- Use the AWS Ground Station EC2 AMI to launch EC2 instances that will uplink and downlink data during the contact or receive downlinked data in an Amazon S3 bucket.

**Scenario:**
A company reaches an agreement with a Satellite Imagery Provider to take satellite photos of a specific region. They use AWS Ground Station to communicate that company's Satellite and download the S3 image data.

### AWS Outposts

- **AWS Outposts** is a fully managed service that offers the same AWS infrastructure, AWS services, APIs, and tools to virtually any datacenter, co- location space, or on-premises facility for a truly consistent hybrid experience.
- **AWS Outposts** is rack of servers running AWS Infrastructure on your physical location

**What is a Server Rack?**

- A frame design to hold and organize IT equipment.

**Rack Heights**

- U stands for "rack units" or "U spaces" with is equal to 1.75 inches. The industry standard rack size is 48U (7 Foot Rack)
  **Full-size rack cage is 42U high**
- Equipment is typically: 1U, 2U, 3U, or 4U high

AWS Outposts comes in 3 form factors: 42U, 1U and 2U

- **42U:** AWS delivers it to your preferred physical site fully assembled and ready to be rolled into final position. It is installed by AWS and the rack needs to be simply plugged into power and network.
- **1U:** suitable for 19-inch wide 24-inch deep cabinets AWS Graviton2 (up to 64 vCPUs) 128 GiB memory 4 TB of local NVMe storage
- **2U:** suitable for 19-inch wide 36-inch deep cabinets, Intel processor (up to 128 vCPUs) 256 GiB memory 8TB of local NVMe storage

## Cloud Architecture

**What is a Solutions Architect?** <br/>
A role in a technical organisation that architects a technical solution using multiple systems via researching, documentation, experimentation.

**What is a Cloud Architect?** <br/>
A solutions architect that is focused soley on architecting technical solutions using cloud services <br/>
A cloud architect needs to understand the following terms and factor them into their designed architecture based on the business requirements:

1. **Availability** - your ability to ensure a service remains available (HA)
2. **Scalability** - your ability to grow rapidly or unimpeded
3. **Elasticity** - your ability to shrink and grow to meet the demand
4. **Fault Tolerance** - your ability to prevent a failure
5. **Disaster Recovery** - your ability to recover from a failure (Highly Durable)

A Solution Architect needs to always consider the following business factors: <br/>

- (Security) How secure is this solution?
- (Cost) How much is this going to cost?

### High Scalability

Your ability to **increase your capacity** based on the increasing demand of traffic, memory and computing power

1. **Vertical Scaling** - scaling up (Upgrade to a bigger server)
2. **Horizontal Scaling** - scaling out (Add more servers of the same size)

### High Availability

Your ability for your service to **remain available** by ensuring there is \*no single point of failure and/or ensure a certain level of performance
<br/>

**Service usage:** <br/>

- Elastic Load Balancer: A load balancer allows you to evenly distribute traffic to multiple servers in one or more datacenter. If a datacenter or server becomes unavailable (unhealthy) the load balancer will route the traffic to only available datacenters with servers. <br/>
  Running your workload across multiple **AZs** ensures that if 1 or 2 **AZs** become unavailable your service/applications remain available.

### High Elasticity

Your ability to automatically increase or decrease your capacity based on the current demand of traffic, memory and computing power
<br/>

**Horizontal Scaling:** <br/>

1. Scaling Out - Add more servers of the same size
2. Scaling In - Removing underutilised servers of the same size

**Service usage:** <br/>

- Auto Scaling Groups (ASG): is an AWS feature that will automatically add or remove severs based on scaling rules you define based on metrics <br/>

Vertical Scaling is generally hard for traditional architecture so you'll usually only see horizontal scaling described with **Elasticity**

### Highly Fault Tolerant

Your ability for your service to ensure there is **no single point of failure**. Preventing the chance of failure
<br/>

**Fail-overs** is when you have a plan to **shift traffic** to a redundant system in case the primary system fails <br/>

**Service usage:** <br/>

- RDS Multi-AZ: is when you run a duplicate standby database in another AZ in case your primary database falls.

A common example is having a copy (secondary) of your database where all ongoing changes are synced. The secondary system is not in-use until a **fail-over** occurs and it becomes the primary database.

### Business Continuity Plan (BCP)

A **business continuity plan** (BCP) is a document that outlines how a business will continue operating **during an unplanned disruption in services**

- Recovery Point Objective (RTO)
- Recovery Time Objective (RPO)

### Disaster Recovery options

![alt text](images/disaster_recovery.png 'Disaster Recovery Options diagram')

### RTO

![alt text](images/RTO.png 'RTO diagram')

**Recovery Time Objective (RTO)** is the maximum delay between the interruption of service and restoration service. This object determines what is considered an acceptable time window when service is unavailable and is defined by the organisation.

### RPO

![alt text](images/RPO.png 'RPO diagram')

- **Recovery Point Objective (RPO)** is the maximum acceptable amount of time since the last data recovery point.
- This objective determines what is considered an aceptable loss of data between the last recovery point and the interruption of service and is defined by the organisation

## Management and Developer Tools

### AWS API ✅ <br/>

(cover what API endpoints there are make requests too. Not commonly dealt with)

### AWS Management Console

- The AMS Management Console is a **web-based** unified console
- **Build, manage, and monitor everything** from simple web apps to complex cloud deployments

### AWS Account ID

- Every AWS Account has a unique Account ID.
- Account ID can be easily found vy dropping down the current user in global navigation
  <br/>
  The AWS Account ID is used:
- When loggin in with a non-root user account
- Cross-account roles
- Support cases
- Generally good practice to keep your Account ID private as it is one of many components used to identify an account for attack by a malicious actor

### AWS Resource Name (ARNs)

- **Amazon Resource Names (ARN)** uniquely identify AWS resources. <br/>
  The ARN have following formations:
- `arn:partition:service:region:account-id:resource-id`
- `arn:partition:service:region:account-id:resource-type/resource-id`
- `arn:partition:service:region:account-id:resource-type:resource-id`

Partition:

- aws: AWS Regions
- aws-cn: AWS Regions
- aws-us-gov: AWS GovCloud (US) Regions

Service - Identifies the service:

- ec2
- s3
- iam

Region - which AWS resource

- us-east-1
- ca-central-1

Account ID

- 121212121212
- 123456789012

Resource ID:

- user/Bob
- instance/i-1234567890abcdef0

In the AWS Management Console its common to be able to copy the ARN to your clipboard
<br/>

```
arn:aws:s3:::my-bucket
```

### Paths in ARNs

- Resource ARNs can include a path
- Paths can include a wildcard character, namely an asterisk(\*)

**IAM Policy ARN Path**<br/>
`arn:aws:iam::123456789012:user/Development/product_1234`

<br/>

**S3 ARN Path**<br/>
`arn:aws:s3:::my_corporatae_bucket/Development`

### AWS Command Line Interface (CLI)

AWS Command Line (Interface) allows users to programatically interact with the AWS API via entering **single or multi-line commands** into a shell or terminal <br/>

- The AWS CLI is a python executable program
- Python is required to install AWS CLI

### AWS SDK

- A SDK is a **collection of software development tools** in one installable package
- You can use **AWS SDK** to programatically create, modify, delete or interact with AWS resources

### AWS CloudShell

**AWS CloudShell** is a **browser-based** built into the AWS Management Console. (AWS CloudShell is scoped per region, Same crdential as logged in user. Free Service)
<br/>

**Preinstalled Tools**

- AWS CLI, Python, Noe.js, git, make , pip, sudo, tar, tmux, vim + more
  **Storage included**
- 1GB of storage free per AWS Region
  **Saved files and settings**
- Files saved in your home directory are available in future sessions for the same AWS Region
  **Shell Environments**
- Bash, PowerShell, Zsh

\*AWS CloudSherll is available in select regions

### Infrastructure as Code (IAC)

You write configuration script to **automate** creating, updating or destroyign cloud infrastructure

- IaC is a blueprint fo your infrastructure
- IaC allows you to easily **share, version or inventory** your Cloud Infrastructure

**AWS CloudFormation (CFN)** - CFN is a Declarative IaC tool

- What you see is what you get (explicit)
- More verbose, but zero chance of mis-configuration
- Uses scripting languages (JSON, YAML)

**AWS Cloud Dvelopment Kit (CDK)** - CDN is an Imperative IaC tool

- You say what you want, and the rest is filled (Implicit)
- Les verbose, you could end up with mis-configuration
- Uses scripting languages (JSON, YAML)
- Does more than Declarative
- Uses programming languages

### Access Keys

**Access Keys** is a _key secret_ required to have programmatic access to AWS resources when interaction with the AWS API outside of the AWS Management Console

## Shared Responsibility Model

The **Shared Responsibility Model** is a _cloud security framework_ that defines the security obligations of the customer versa the Cloud Service Provider (CSP - e.g: AWS)

### AWS Shared Responsibility Model

- Customers are responsible for Security **IN** the cloud
- AWS is responsible for Security **OF** the cloud

![alt text](images/srm.jpg 'AWS Shared Responsibility Model')

### Types of Cloud Computing Responsibility

![alt text](images/types-of-cc-responsibilities.jpg 'AWS Types of Shared Responsibility')

### Compute

![alt text](images/srm-compute.png 'Shared Responsibility Model - Compute')

### Compute - Diagram

![alt text](images/srm-compute-diagram.png 'Shared Responsibility Model - Compute Diagram')

### Shared Responsibility Model

The **Shared Responsibility Model** is a simple visualisation that helps determine what the customer is responsible for and what the CSP is responsible for related to AWS.
<br/>

- The customer is responsible for the data and the **configuration** of access controls that reside in AWS.
- The customer is responsible for the **configuration** of cloud services and granting access to users via permissions.
- CSP is generally responsible for the underlying Infrastructure
  <br/>
- **Responsibility of in the cloud:** If you can configure or store it then you (the customer) are responsible for it.
- **Responsibility of the cloud:** If you can not configure it then CSP is responsible for it.

![alt text](images/srm.png 'Shared Responsibility Model Diagram')

## Computing Services

**Elastic Compute Cloud (EC2)** allows you to launch Virtual Machines (VM) <br/>
What is a Virtual Machine?<br/>
A Virtual Machine (VM) is an emulation of a physical computer using software. <br/>
Server Virtualization allows you to easily: create, copy, resize or migrate your server. <br/>
Multiple VMs can run **on the same physical server** so you can share the cost with other customers <br/>
(Imagien if your server or computer was an executable file on your computer)
<br/>
EC2 is highly configurable server, where you can choose **AMI** that affects options such as:

- The amount of CPUs
- The amount of Memory (RAM)
- The amount of Network Bandwidth
- The OS
- Attach multipl,e virtual hard-drives for storage (eg - Elastic Book Store)

(**An Amazon Machine Image** is a predefined configuration for a Virtual Machine)
<br/>
EC2 is considered **the backbone of AWS** because the majority of AWS services are using EC2 as their underlying servers (eg - S3, RDS, DynamoDB, Lambdas)

<br/>

**Computing Services Diagram**
<br/>

![alt text](images/computing-services.png 'Computing Services List Diagram')

### High Performance Computing Services

**The Nitro System** - A combination of **dedicated hardware and lightweight hypervisor** enabling faster innovation and enhanced security. All new EC2 instances use Nitro System. <br/>

- Nitro Cards: specialised cards for VPC, EBS and Instance Storage and controller card
- Nitro Security Chips: integrated into mothetrboard. Protects hardware resources
- Nitro Hypervisor: lightweight hypervisor Memory and CPU allocation Bare Metal-like performance
  <br/>

**Bare Metal Instance**: you can launch EC2 instance that have no hypervisor so you can run workloads directly on the hardware for maximum performance and control. The **M5 and R5** EC2 instances run bare metal. <br/>

**Bottlerocket**: is a Linux-based open-source operation system that is purpose-built by AWS for running containers on Virtual Machines or bare metal hosts.<br/>

**What is High Performance Computing (HPC)?**: a cluster of hundreds of thousands of servers with fast connections between each of them with the purpose of boosting computing capacity. <br/>

**AWS ParallelCluster**: is an AWS-supported open soruce cluster management tool that makes it easy for you to deploy and manage High Performance Computing (HPC) clusters on AWS <br/>

### Edge and Hybrid Computing Services

**What is Edge Computing?** <br/>
When you push your computing workloads outside of your networks to run close to the destination location. (eg - Pushing computing to run on phones, IoT Devices, or external servers not within your cloud network)
<br/>

**What is Hybrid Computing?** <br/>
When you're able to run workloads on both your on-premise datacenter and AWS Virtual Private Cloud (VPC)
<br/>

**AWS Outposts** is a <strong>physical rack of servers</strong> that you can put in your datacenter. AWS Outposts allows you to use AWS API and Services such as EC2 right in your datacenter.<br/>

**AWS Wavelength** allows you <strong>to build and launch your applications in a telecom datacenter</strong>. By doing this your apps wit have ultra-low latency since they will be pushed over a 5G Network and be closest as possible to the end user.<br/>

**VMWare Cloud on AWS** allows you to <strong>manage on-premise virtual machines using VMWare</strong> as EC2 instances. The data-center must be using VMWare for Virtualisation.<br/>

**AWS Local Zones** are <strong>edge datacenters located outside of an AWS region</strong> so you can use AWS closer to end destination.<br/>

### Cost and Capacity Management Computing Services

![alt text](images/cost-capacity-management-computing-services.png 'Computing Services List Diagram')

## Storage

### Types of Storage

![alt text](images/types-of-storage.png 'Types of Storage Diagram')

<br/>

### Introduction to S3

![alt text](images/intro-to-S3.png 'Intro to S3 Diagram')

<br/>

### AWS Snow Family

AWS Snow Family are **storage and compute devices used to physically move data in our out the cloud** when moving data over the internet or private connection - when it's to slow, difficult or costly

![alt text](images/snow-family.png 'Snow Family Diagram')

<br/>

### AWS Storage Services

![alt text](images/storage-services-1.png 'AWS Storage Services - 1')

![alt text](images/storage-services-2.png 'AWS Storage Services - 2')

## Databases

- A database is a **data-store that stores semi-structure and structured data** <br/>
- A database is more **complex data stores** because it <strong>requires using formal design and modeling techniques</strong> <br/>
  Database can be generally categorised as either:
  _Relational Databases_:
- Structured data that stronly represents tabular data (tables, rows & columns)
  _Non-Relational Databases_:
- Semi-structuted that may or may not distantly tabular data
  <br/>
  Databases have a rich set of functionality:

1. Specialised language to query (retrieve data)
2. Specialised modelling strategies to optimise retrieval for different use cases
3. More fine tune control over the transformation of the data into useful data structures or reports

<br/>

Normally a database infers someone is using a **relational row-oriented data store**

### Data Warehouse

A relational datastore designed for **analytical workloads**, which is generally **column-oriengted data-store**
<br/>

- Companies will have _terabytes and millions of rows of data_, and they need a fast way to be able to produce analytics reports.
  <br/>

Data warehouses generally perform **aggregation**:

- Data warehouses are optimised around columns since they need to quickly aggregate column data
  <br/>
  Data warehouses are generally designed to be HOT:
- Hot means they can return queries very fast even though they have vasts amount of data
  <br/>
  Data warehouses are infrequently accessed meaning they aren't intented for real-time reporting but maybe once or twice a day or once a week to generate business and user reports
  <br/>
  A data warehouse needs to consume data from a relational database on a regular basis

### NoSQL Database Services

![alt text](images/nosql-db-services.png 'NoSQL Database Services')

### Relational Databse Services

![alt text](images/relational-db-services.png 'Relational Database Services')

### Other Database Services

![alt text](images/other-db-services.png 'Other Database Services')

## Networking

### Cloud-Native Networking Services

![alt text](images/cloud-native-networking-services.png 'Cloud-Native Networking Services')

### Enterpirse/Hybrid Networking Services

![alt text](images/enterprise-networking-services.png 'Enterpirse/Hybrid Networking Services')

### Virtual Private Cloud (VPC) and Subnets

**Virtual Private Cloud (VPC)** is a logically isolated section of the AWS Network, where you launch your AWS resources. You choose a _range of IPs using CIDR Range_.
<br/>

**CIDR Range**: A "CIDR range" in the cloud refers to a block of IP addresses defined using Classless Inter-Domain Routing (CIDR) notation
<br/>

- **Subnets** are a logical partition of an IP network into multiple smaller network segments. _You are breaking up your IP range for VPC_ into smaller networks. <br/>
- Subnets _need to have a smaller CIDR range than the VPC_ that represent their portion (eg - Subnet CIDR Range 10.0.0.0/24 = 256 IP Addresses)
  <br/>

- **A Public Subnet** is one that can reach the internet
- **A Private Subnet** is one that cannot reach the internet

![alt text](images/vpc-subnets.png 'Virtual Private Cloud (VPC) and Subnets')

### Security Groups vs NACLs

**Network Access Control Lists (NACLs)**:

- Acts as a virtual _firewall at the subnet level_
- You create _Allow and Deny rules_
- eg: Block a specific IP address known for abuse

<br/>

**Security Groups**:

- Acts as a virtual _firewall at the instance level_
- Implicitly denies all traffic. _You create only Allow rules_
- eg: Allow an EC2 instance access on port 22 for SSH
- eg: <strong>You cannot block a single IP address</strong>

![alt text](images/security-groups-nacls.png 'Security Groups vs NACLs')

## EC2

- **Elastic Compute Cloud (EC2)** is a _highly configurable virtual server/machine_.
- EC2 is resizable **compute capacity**. It takes minutes to launch new instances.
- Anything and everything on AWS uses EC2 instances underneath.

![alt text](images/ec2.png 'Introduction to EC2')

### EC2 Families

**What are Instance Families?**

- Instance families are different combinations of CPU, Memory, Storage and Networking capacity
- Instance families allow you to choose the appropriate combination of capacity to meet your application's unique requirements
- Different instance families are different because of the varying hardware used to give them their unique properties
- Commonly instance families are called _Instance Types_ but an instance type is a combination of size and family

![alt text](images/ec2-instance-families.png 'EC2 Instance Families')

### EC2 Instance Types

An instance type is a particular _instance size and instance family_
<br/>

A common pattern for instance sizes:

- nano
- micro
- small
- medium
- large
- xlarge
- 2xlarge
- 4xlarge
- 8xlarge
- ...
  <br/>

There are many exceptions to this pattern for sizes:

- c6g.metal: is a bare metal machine
- C5.9xlarge: is not a power of 2 or even number size

### EC2 Instance Sizes

EC2 Instance Sizes **generally double** in price and key attributes

### EC2 - Dedicated Host

**Dedicated Hosts** are single-tenant EC2 instances designed to let you Bring-Your-Own-License (BOYL) based on _machine characteristics_

![alt text](images/ec2-dedicated-host.png 'EC2 - Dedicated Host')

### EC2 Tenancy

EC2 has 3 levels of tenancy

- _Dedicated Host:_ your server lives here and you have control of the physical attributes
- _Dedicated Instance:_ your server always lives here
- _Default:_ your instance lives here until reboot

![alt text](images/ec2-tenancy.png 'EC2 Tenancy')

### EC2 Pricing Models

There are 5 different ways to pay for EC2 (Virtual Machines)

1. On-Demand (Least Commitment)
2. Spot (Biggest Savings)
3. Reserved (Best Long-term)
4. Dedicated (Most Expensive)

_AWS Savings Plan_ is another way to save but can be used for more than just EC2

### **On-Demand**

**On-Demand** is a _Pay-As-You-Go (PAYG) model_, where you consume compute and then you pay

- When you launch an EC2 instance, it is _by default_ using _On-Demand_ pricing
- On-Demand has _no up-front payment_ and _no long-term commitment_
- You are charged by the _second (min of 60 seconds)_ of the _hour_
- When looking up pricing it will always show EC2 pricing is the _hourly rate_

<br/>

- **On-Demand** is for applications where the workload is for _short-term_, _spikey_ or _unpredictable_
- When you have a _new app_ for development or you want to run experiment

### **Reserved Instances (RI)**

Designed for applications that have a _steady-state, predictable usage_, or require _reserved capacity_ <br/>
Reduced Pricing is based on _Term_ x _Class Offering_ x _RI Attributes_ x _Payment Option_ <br/>

#### Term - The longer the term the greater savings

- You commit to a _1 year_ or _3 year_ contract
- When it expires, your instance will use On-Demand with no interruption to service

#### Class - The less flexible the greater savings

- _Standard_: up to _75%_ reduced pricing compared to On-Demand. You can modify _RI Attributes_
- _Covertible_: up to _54%_ reduced pricing compared to On-Demand. You can exchange RI based on _RI Attributes_ if greater or equal in value
  <br/>
  AWS no longer offers Scheduled RI57

#### Payment Options - The greater upfront the greater the savings

- _All Upfront_: full payment is made at the start of the term
- _Partial Upfront_: a portion of the cost must be paid upfront and the remaining hours in the term are billed at a discounted hourly rate
- _No Upfronot_: you are billed a disocunted hourly rate for every hour within the term, regardless of whether the Reserved Instance is being used
  <br/>

- _RIs_ can be _shared between multiple accounts within an AWS Organisation_
- _Unused RIs_ can be sold in the _Reserved Instance Marketplace_

![alt text](images/purchase-RI.png 'Purchase an RI')

### **Reserved Instances (RI) - RI Attributes**

**RI Attributes (aka Instance Attributes)** are limited based on Class Offering, and can affect the final price of an RI instance.
<br/>

There are 4 RI Attributes:

1. _Instance Type_: for example, m4.large. This is composed of the instance family (for example, m4) and the instance size (for example, large)
   <br/>

2. _Region_: the region in which the Reserved Instance is purchased
   <br/>

3. _Tenancy_: whether your instance runs on shared (default) or single-tenant (dedicated) hardware
   <br/>

4. _Platform_: the operating system (for example, Windows or Linux/Unix)

### **Regional and Zonal RI**

When you purchase a RI, you determine the _scope_ of the Reserved Instance <br/>
(The scope **does not affect the price**)
<br/>

#### _Regional RI_ - purchase for a Region

- does not reserve capacity
- RI discount applies to instance usage in any AZ in the Region
- RI discount applies to instance usage within the instance family, regardless of size. Only supported on Amazon Linux/Unix Reserved Instances with default tenancy
- You can queue purchases for Regional RI

#### _Zonal RI_ - purchase for an AZ

- reserves capacity in the specified AZ
- RI discount applies to instance in the selected AZ (No AZ flexibility)
- No instance size flexibility. RI discounts applies to instance usage for the specified instance type and size only
- You can't queue purchases for Zonal RI

### **Reserved Instances (RI) - RI Limits**

There is a limit to the number of Reserved Instances that you can purchase per month
<br/>

_Per month_ you can purchase:

- _20_ Regional RIs <i>per Region</i>
- _20_ Zonal RIs <i>per AZ</i>

<br/>

**Regional Limits**

- You cannot exceed your running On-Demand Instance limit by purchasing Regional RIs. The default On-Demand Instance limit is 20
- Before purchasing RI ensure your On-Demand limit is equal to or greater than your RI you intend to purchase
  <br/>

**Zonal Limits**

- You can exceed your running On-Demand Instance limit by purchasing Zonal RIs
- If you already haev 20 running On-Demand Instances and you purchase 20 Zonal RIs, you can launch a further 20 On-Demand Instances that match the specifcations of your Zonal RIs

### Capacity Reservations

EC2 instances are backed by different kinds of hardware, and so there is a _finite amount of servers_ available within an AZ per instance type or family
<br/>

**Capacity Reservation** is a service of EC2 that allows you to _request a reserve of EC2 instance type_ for a specific Region and AZ
<br/>

- The reserved capacity is charged at the selected instance type's On-Demand rate whether an instance is running in it or not
- You can also use your Regional RIs with your Capacity Reservatioons to benefit from billing discounts

### Standard vs Convertible RI

There are some key differences between _Standard_ and _Convertible_

![alt text](images/std-vs-convertible.png 'Standard vs Convertible RI')

### RI Marketplace

EC2 Reserved Instance Marketplace allows you to _sell your unused Standard RI_ to recoup your RI spend for RI you do not intend or cannot use
<br/>

- Reserved Instances can be sold after they have been active for at least 30 days and once AWS has received the upfront payment (if applicable).
- You must have a US bank account to sell Reserved Instances on the Reserved Instance Marketplace.
- There must be at least one month remaining in the term of the Reserved Instance you are listing.
- You will retain the pricing and capacity benefit of your reservation until it's sold and the transaction is complete.
- Your company name (and address upon request) will be shared with the buyer for tax purposes.
- A seller can set only the upfront price for a Reserved Instance. The usage price and other configuration (e.g.,
  instance type, Availability Zone, platform) will remain the same as when the Reserved Instance was initially purchased.
- The term length will be rounded down to the nearest month. For example, a reservation with 9 months and 15 days remaining will appear as 9 months on the Reserved Instance Marketplace.
- You can sell up to $20,000 in Reserved Instances per year. If you need to sell more Reserved Instances.
- Reserved Instances in the GovCloud region cannot be sold on the Reserved Instance Marketplace.

### Spot Instances

AWS has _unused compute capacity_ that they want to maximise the utility of their idle servers
<br/>
(It's like when a hotel offers booking discounts to fill vacant suites or planes offer discounts to fill vacant seats)
<br/>

- Spot Instances provide a discount of _90%_ compared to On-Demand Pricing
- Spot Instances can be terminated if the computing capacity is needed by other On-Demand customers
- Designed for applications that have flexible start and end times or applications that are only feasible st _very low_ compute costs
  <br/>

**AWS Batch** is an easy and convenient way to use Spot Pricing
<br/>

**Termination Conditions**<br/>

- Instances can be terminated by AWS _at anytime_
- If your instance is _terminated by AWS_, **YOU DO NOT GET CHARGED** for a partial hour of usage
- If _you terminate_ an instance **YOU WILL STILL BE CHARGED** for any hour that it ran

### Dedicated Instances

Dedicated Instances is designed to meet regulatory requirements
<br/>

- When you have strict _server-bound licensing_ that won't support multi-tenancy or cloud deployments you use **Dedicated Hosts**.

Types: <br/>
_Multi-tenant:_

- when customers are running workloads on the same hardware
- _virtual isolation_ is what separate customers
  _Single-tenant:_
- when a single customer has dedicated hardware
- _physical isolation_ is what separates customers
  <br/>
  Dedicated can be offered for: <br/>

* On-demand
* Reserved (up to 60% savings)
* Spot (up to 90% savings)
  <br/>

You choose tenancy when you _launch_ your EC2
<br/>

_Enterprises_ and _Large Organisations_ may have security concerns or obligations about sharing the same hardware with other AWS Customers

### AWS Savings Plan

_Savings Plan_ offers you the similar discounts as Reserved Instances (RIs) but _simplifies the purchasing process_ <br/>

There are 3 types of Savings Plans:

- Compute Savings Plans
- EC2 Instance Savings Plans
- SageMaker Savings Plans
  <br/>
  You can choose 2 different terms:
- 1 year
- 3 year
  <br/>
  You can choose the following Payment Options
- All Upfront
- Partial Upfront
- No Upfront
  (You can choose an hourly commitment)
  <br/>

AWS Savings Plan has 3 different savings types:
_Compute_

- Compute Savings Plans provide the most flexibility and help to reduce your costs by up to 66%
- These plans automatically apply to EC2 instance usage, AWS Fargate, and AWS Lambda service usage regardless of instance family size, AZ, region, OS or tenancy
  _EC2 Instances_
- Provied the lowest prices, offering savings up to 72% in exchange for commitment to usage of indiidual instance families in a region
- Auto reduces your cost on the selected instance family in that region regardless of AZ size, OS or tenancy
- Give you the flexibility to change your usage between instances within a family in that region
  _SageMaker_
- Helps you reduce SageMaker costs by up to 64%
- Auto apply to SageMaker usagr regardless of instance familu, size, component, or AWS region

## Zero Trust Model

The model operates on the principle of _"trust no one, verify everything"_
<br/>

Malicious actors being able to by-pass conventional _acess controls_ demonstrates traditional security measures are no longer sufficient
<br/>

In the Zero Trust Model _Identity_ becomes the primary security perimeter <br/>

**What is the Primary Security Perimeter?** <br/>

- The primary or new security perimeter defines the first line of defense and its security controls that protect a company's cloud resources and assets
  <br/>

**Network-Centric (Old Way):**

- Traditional security focused on firewalls and VPNs since there were few employees or workstations outside the office or they were in specific remote offices
  <br/>

**Identity-Centric (New Way):**

- Bring-your-own-device, remote workstations is much more common
- Cannot trust if the employee is in a secure location (identity based security controls like MFA, or providing provisional access based on the level of risk from where, when and what a user wants to access)
  <br/>

<blockquote>Identity-Centric does not replace but *augments* Network-Centric security</blockquote>

### Zero Trust om AWS

**Identity Security Controls** you can implement on AWS to meet the Zero Trust Model <br/>
**AWS Identity and Access Management (IAM)**

- IAM Policies
- Permission Boundaries
- Service Control Policies (Organisation-wide Policies)
- IAM Policy Conditions
  - aws:SourceIp -> restrict on IP Address
  - aws:RequestedRegion -> restrict on region
  - aws:MultiFactorAuthPresent -> restrict if MFA is turned off
  - aws:CurrentTime -> restrict access based on time of day
  <br/>
  <blockquote>AWS does not have ready-to-use identity controls that are intelligent, which is why AWS is considered to not have a true Zero Trust offering for customers, and 3rd-party services need to be used</blockquote>
  <br/>
  A collection of AWS Services can be setup to intelligent-ish detection of identity concerns but requires expert knowledge
  1. **AWS CloudTrail**: tracks all API calls
  2. **AWS GuardDuty**: detects suspicious or malicious activity based on CloudTrail and other logs
  3. **AWS Detective**: used to analyse, investigate and quickly identify security issues (can ingest findings from Guard Duty)

### Zero Trust on AWS with 3rd Parties

AWS does technically implement a Zero Trust Model but does not allow for intelligent identity security controls <br/>
_Third Party Identity solutions:_

- Azure Active Directory (Azure AD)
- Google BeyondCorp
- JumpCloud
  (all have more intelligent security controls for real-time detection)

### Directory Service

**What is directory service?** <br/>
A service that maps the _name of network resources to their network addresses_
<br/>

- A directory service is shared information infrastructure for _location, managing, administrating and organising_ resources
- Is a critical component of a network operating system
- A directory server (name server) is a server which provides a directory service
- Each resource on the network is considered an object by the directory server.
- Information about a particular resource is stored as a collection of attributes associated with that resource or object

### Active Directory

To give organisations the ability to manage multiple on-premises inftrastructure components and systems using a single identity per user

![alt text](images/active-directory.png 'Active Directory')

### Identity Providers (IdPs)

- A system that creates, maintains and manages identity information for principals and provides authentication services to applications withiin a _federation_ or distributed network
- A trusted provider of your user identity that lets you use authetentication to access other services

<blockquote>

_Federated identity_ is a method of linking a user's identity across multiple separate identity management systems

</blockquote>

(examples - OpenID, OAuth2.0, SAML: _Single-Sign-On via web browser_)

### Single-Sign-On

**Single-sign-on** is an authentication scheme that _allows a user to log in wih a single ID and password to different systems and software_
<br/>

<blockquote>

SSO allows IT departments to adminstrate a single identity that can access many machines and cloud services

</blockquote>

_Login for SSO is seamless, where once a user is logged into their primarry directory, as soon as they utilise this software they are not presented with a login screen_

### Lightweight Directory Access Protocol (LDAP)

An open, vendor-neutral, industry standard _application protocol for accessing and maintaining distributed directory information services_ over an Internet Protocol (IP) network
<br/>

- A common use of LDAP is to provide a central place to store usernames and passwords
- LDAP enables for _same sign-in_. Same sign-on allows users to use a single ID and password, but they have to enter it in everytime they want to login

**Why use LDAP when SSO is more convenient?** <br/>

- Most SSO systems are using LDAP
- LDAP was not designed natively to work with web applications
- Some systems only support integration with LDAP and not SSO

![alt text](images/LDAP.png 'LDAP Architecture')

### Security Keys

**What is a Security Key?** <br/>
A secondary device used as a second step in the authentication process to gain access to a device workstation or application (example - Yubikey)

### AWS Identity and Access Management (IAM)

AWS Identity and Access Management (IAM) you can create and manage AWS users and groups, and use permissions to allow and deny their access to AWS resources <br/>

_IAM Policies_: JSON documents which grant permissions for a specific user, group, or role to access services. Policies are attached to **IAM Identities** <br/>
_IAM Permission_: The API actions that can or cannot be performed. They are represented in the IAM Policy document

<hr/>

#### IAM Identities

_IAM Users_: End users who log into the console or interact with AWS resources programatically or via clicking UI interfaces <br/>
_IAM Groups_: Group up your users so they all share permission levels of the group (Admins, Developers, etc.) <br/>
_IAM Roles_: Roles grant AWS resources permissions to specific AWS API actions. Associate policies to a role and then assign it to an AWS resource <br/>

#### Principle of Least Privilege (PoLP)

**Principle of Least Privilege (PoLP)** is the computer security concept of providing a user, role, or application the least amount of permissions to perform a operation or action <br/>
_Just-Enough-Access:_

- Permitting only the exact actions for the identity to perform a task
  <br/>

_Just-In-Time:_

- Permitting the smallest length of duration an identity can use permissions
  <br/>

_Risk-based adaptive policies:_

- Each attempt to access a resource generates a risk score of how likely the request is to be from a compromised source
- The risk score could be based on many factors (eg - device, user location, IP address, what service is being accessed and when)

### AWS Account Root User

Administrative Tasks _that only the Root User can perform:_

- Change your account settings
- Close your AWS account
- Change or Cancel AWS Support Plan

### AWS Single-Sign On

**AWS Single-Sign On (AWS SSO)** is where you create, or connect, your workforce identities in AWS _once_ and manage access centrally across your AWS organisation

![alt text](images/aws-sso.png 'AWS SSO')

## Application Integration

**What is Application Integreation?** <br/>
Application Integration is the process of letting two independent applications communicate and work with each other, commonly facilitated by an intermediate system
<br/>

<blockquote>

Cloud workloads encourage systems and services to be loosely coupled and so AWS has many service for the specific purpose of application integration

</blockquote>
<br/>

Common systems or design patterns utilised for Application Integration generally are:

- Queueing
- Streaming
- Pub/Sub
- API Gateways
- State Machine
- Event Bus

### Queueing

**What is a Messaging System?** <br/>

- Used to provide async communication and decouple processes via messages / events
- From a sender and receiver ( producer and consumer)
  <br/>

**What is a Queueing System?** <br/>

- A messgaing system that generally will delete messages once they are consumed
- Simple communication. _Not Real-time_
- Have to pull. _Not reactive_
  <br/>

**Simple Queueing Serviec (QSS)**: fully managed _queueing service_ that enables you to decouple and scale microservices, distributed systems, and serverless applications
<br/>

Use Cases:

- You need to queue up transaction emails to be sent (eg - SignUp, Reset Password)

### Streaming

**What is streaming?** <br/>

- Multiple consumers can _react_ to events (messages)
- Events live in the stream for long periods of time, so complex operations can be applied
- **Real-time**
  <br/>

**Amazon Kinesis:** is the fully managed solution for collection, processing, and analysing streaming data in the cloud

![alt text](images/aws-kinesis.png 'AWS Kinesis - Streaming')

### Pub/Sub

**What is Pub/Sub?** <br/>

- Publish-subscribe pattern commonly implemented in _messaging systems_
- In a pub/sub system, the sender of messages (_publishers_) do not send their messages directly to receivers
- They send their messages to an _event bus_. The event bus categorises their messages into groups
- The receivers of messages (_subscribers_) subcribe to these groups
- Whenever new messages appear within their subscription the messages are immediately delivered to them

![alt text](images/pub-sub.png 'Pub/Sub')
<br/>

- Publishers have no knowledge of who their subscribers are
- Subscribers do _not pull_ for messages
- Messages are instead automatically and immediately _pushed_ to subscribers
- Messages and events are interchangeable terms in pub/sub

Use Case:

- a real-time chat system
- web-hook system

**Simple Notificaton Service (SNS):** is a highly available, secure, fully managed _pub/sub messaging_ service that enables you to _decouple_ microservices, distributed systems, and serverless applications

### API Gateway and Amazon API Gateway

**What is an API Gateway?** <br/>

- A program that sits between a single-entry point and multiple backends
- Allows for throttling, logging, routing logic or formatting of the request and repsonse
  <br/>

**Amazon API Gateway:** is a solution for _creating secure APIs_ in your cloud environment at _any scale_. Create APIs that act as a front door for applications to access data, business logic, or functionality from back-end services

![alt text](images/aws-api-gateway.png 'Amazon API Gateway')

### State Machines and AWS Step Functions

**What is a State Machine?** <br/>
An abstract model which decides how one state moves to another based on a series of conditions. _Think of a state machine like a flow chart_
<br/>

_What is AWS Step Functions?_ <br/>

- Coordinate multiple AWS Services into a serverless workflow
- A graphical console to visualise the components of your application as a series of steps
- Automatically triggers and tracks each step, and retries when there are errors, so your application executes in order as expected, every time
- Logs the state of each step, so when things go wrong, you can diagnose and debug problems quickly

### Event Bus and Amazon Event Bridge

**What is an Event Bus?** <br/>
_Receives events_ from a source and _routes events_ to a target based on <strong>rules</strong>

![alt text](images/event-bus.png 'Event Bus')
<br/>

**EventBridge** is a _serverless_ event bus service that is used for application integration by _streaming real-time_ data to your applications (formeerly called Amazon CloudWatch Events)
<br/>

![alt text](images/amazon-event-bridge.png 'Amazon Event Bridge')
<br/>

### Application Integration Services

![alt text](images/application-integration-services.png 'Application Integration Services')

## Containers

### VMs vs Containers

**VMs:**

- VMs _do not_ make best use of space
- Apps are not isolated, which could cause _config conflicts, security problems or resource hogging_
  <br/>

**Containers:**

- Containers allow you to run multiple apps which are virtually isolated from each other
- Launch new containers and configure OS Depdencies per container

![alt text](images/vm-vs-container.png 'VMs vs Containers')

### Container Services

![alt text](images/container-services.png 'Container services')

## Governance

### Organisations and Accounts

**AWS Organisations** allow the creation of new AWS acounts. Centrally manage billing, control access, compliance, security, and share resources across your AWS accounts
<br/>

**Root Account User:** is a single sign-in identity that has complete access to all AWS services and resources in an account. Each account has a Root Account User
<br/>

**Organisaton Units:** are a group of AWS accounts within an organisation which can also contain other organisational units - creating a hierarchy
<br/>

**Service Control Policies:** give central control over the allowed permissions for all accounts in your organisation, helping to ensure your accounts stay within your organisation's guidelines
<br/>

- AWS Organisations must be turned on, and once turned on it cannot be turned off
- You can create as many AWS Accounts as you like, one account will be the Master/Root Account

<blockquote>

_AWS Account_ is not the same as _User Acount_

</blockquote>

![alt text](images/aws-orgs.png 'AWS Organisations')

### AWS Control Tower

- Helps _Enterprises_ quickly set-up a secure, _AWS multi-account_
- Provides you with a _baseline environment_ to get started with a _multi-account architecture_
  <br/>

**Landing Zone**
A landing zone is a baseline environment following well-architected and best practices to start launching production ready workloads

- AWS SSO enabled, Centralised logging for AWS CloudTrail, cross-account security auditing
  <br/>

**AWS Factory**

- Automates provisioning of new accounts in your organisation
- Standardise the provisioning of new accounts with pre-approved network configuration and region selections
  <br/>

**Guardrails**

- Pre-packaged governance rules for security, operations, and compliance that customers can select and apply enterprise-wide or to specific groups of accounts

<blockquote>

_AWS Control Tower_ is the replacement for retired _AWS Landing Zones_

</blockquote>

### AWS Config

_AWS Config_ is a Compliance-as-Code framework that allows us to manage change in your AWS accounts on a _per region bases_ <br/>

**When should you use AWS Config?** <br/>

- I want this _resource_ to stay _configured_ a _specific way_ for compliance
- I want to _keep track_ of configuration _changes_ to resources
- I want _a list of all resources_ within a region
- I want to _analyse potential security_ weaknesses, you need detailed historical information

**What is Change management?** <br/>
Change management in the context of Cloud Infrastructure is when we have _formal process_ to:

- Monitor changes
- Enforce changes
- Remediate changes

![alt text](images/aws-config.png 'AWS Config')

### AWS Quick Starts

_AWS Quick Starts_ are _Prebuilt templates_ by AWS and AWS partners to _help deploy wide range of stacks_

<blockquote>

Reduce hundreads of manual procedures into just a few steps

</blockquote>
<br/>

A Quick Start is composed of 3 parts:

1. A reference architecture for the deployment
2. AWS CloudFormation templates that automate and configure the deployment
3. A deployment guide explaining the architecture and implementation in detail

### Tagging

_A tag_ is a _key and value pair_ that you can assign to AWS resources
<br/>

Tags allow you to organise your resources such as:
<br/>

_Resource management_
_Cost management and optimisation_

- Specific workloads, environmnets (eg - Developer Environments)
- Cost tracking, Budgets, Alerts
  _Operations management_
- Business commitments and SLA operations (eg - Mission Critical Services)
  _Security_
- Classification of data and security impact
  _Governance and regulatory compliance_
  _Automation_
  _Workload optimisation_
