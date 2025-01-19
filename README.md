## Seven Advantages to Cloud

## 1. Cost effective - Pay on demand

## 2. Global - Launch anywhere in the world

## 3. Secure - Cloud servvices can be secure by default

## 4. Reliable - Data backup, disaster recovery, data replication, fault tolerance

## 5. Scalable - Increae or decrease resources and services based on demand

## 6. Elastic - Automate scaling during spikes and drop in demand

## 7. Current - The underlying hardware and managed software is patched, upgraded and replaced by the cloud provider without interruption to you

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
