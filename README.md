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
