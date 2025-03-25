# AWS-EC2-Deployment-Projects-P2
# AWS EC2 Features Portfolio

[Table of Contents](#table-of-contents)

## Table of Contents

* [Introduction](#introduction)
* [IP Address Behavior in EC2](#ip-address-behavior)
* [Elastic IP Configuration](#elastic-ip)
* [EC2 Placement Groups](#placement-groups)
* [Elastic Network Interfaces (ENIs)](#elastic-network-interfaces)
* [EC2 Hibernate Feature](#ec2-hibernate)
* [Conclusion](#conclusion)

<a name="introduction"></a>
## Introduction

This portfolio demonstrates hands-on experience with key Amazon EC2 features. Each section documents a practical implementation of different EC2 capabilities, including IP addressing, placement strategies, network interfaces, and hibernation. These demonstrations highlight my ability to configure and optimize EC2 instances for various real-world scenarios.

<a name="ip-address-behavior"></a>
## IP Address Behavior in EC2

### Demonstration Overview

In this demonstration, I explored the behavior of public and private IP addresses in EC2 instances, specifically focusing on:

* Connecting to instances using public vs. private IPs
* Observing IP address changes during instance restart cycles

### Implementation Steps

1.  Launched an EC2 instance with both public and private IPv4 addresses
2.  Successfully connected to the instance using the public IPv4 address via SSH
3.  Attempted (unsuccessfully) to connect using the private IPv4 address from outside the AWS network
4.  Stopped and restarted the instance to observe IP address behavior
5.  Documented the public IPv4 address change while the private IPv4 remained static

![Public IP Connection](Images/public-ip-connection.png)
![IP Address Change](Images/ip-address-change.png)

### Key Findings

* Public IPv4 addresses are required for external internet connectivity
* Private IPv4 addresses only work within the AWS network environment
* When an instance is stopped and started, it receives a new public IPv4 address, private IPv4 addresses remain unchanged through stop/start cycles

### Business Application

This knowledge is critical for designing reliable network architectures in AWS. Understanding IP address persistence helps avoid connectivity issues when instances undergo maintenance cycles.

<a name="elastic-ip"></a>
## Elastic IP Configuration

### Demonstration Overview

This demonstration addressed the limitation of changing public IP addresses by implementing Elastic IPs, focusing on:

* Allocating and associating Elastic IPs with EC2 instances
* Testing IP persistence during instance stop/start cycles
* Understanding Elastic IP pricing implications

### Implementation Steps

1.  Allocated a new Elastic IP from Amazon's IPv4 address pool
2.  Associated the Elastic IP with a running EC2 instance
3.  Confirmed the public IPv4 address now matched the Elastic IP value
4.  Stopped and restarted the instance
5.  Verified the public IPv4 address remained unchanged
6.  Disassociated and released the Elastic IP to avoid charges

![Elastic IP Allocation](Images/elastic-ip-allocation.png)
![Elastic IP Association](Images/elastic-ip-association.png)

### Key Findings

* Elastic IPs provide persistent, static public IP addresses
* These IPs remain associated with instances through stop/start cycles
* Unused Elastic IPs incur charges (~$3.50/month)
* AWS Free Tier includes 750 hours per month of public IPv4 addresses

### Business Application

Elastic IPs are essential for services requiring constant accessibility through a fixed address, such as public-facing web applications, DNS configurations, and services with strict firewall rules.

<a name="placement-groups"></a>
## EC2 Placement Groups

### Demonstration Overview

In this demonstration, I configured different placement group strategies to optimize instance placement according to specific requirements:

* Cluster placement for high-performance computing
* Spread placement for critical applications
* Partition placement for distributed workloads

### Implementation Steps

1.  Created three different placement groups:
    * `my-high-performance-group` using the cluster strategy
    * `my-critical-group` using the spread strategy (rack level)
    * `my-distributed-group` using the partition strategy (4 partitions)
2.  Demonstrated how to launch instances within each placement group

![Placement Groups Creation](Images/placement-groups-creation.png)
![Placement Groups Launch](Images/placement-groups-launch.png)

### Key Findings

* Cluster placement groups: Position instances close together for maximum network performance
* Spread placement groups: Distribute instances across separate racks for maximum availability
* Partition placement groups: Group instances into logical partitions, useful for distributed applications

### Business Application

Proper placement group selection directly impacts application performance and availability:

* High-Performance Computing (HPC) and low-latency applications benefit from cluster placement
* Critical applications requiring high availability benefit from spread placement
* Large distributed applications (Hadoop, Cassandra) benefit from partition placement

<a name="elastic-network-interfaces"></a>
## Elastic Network Interfaces (ENIs)

### Demonstration Overview

This demonstration explored the creation and management of Elastic Network Interfaces for advanced networking capabilities:

* Creating and attaching custom ENIs to EC2 instances
* Implementing network failover by moving ENIs between instances
* Understanding ENI lifecycle management

### Implementation Steps

1.  Launched two EC2 instances, each with a primary network interface
2.  Created a custom ENI with a description "demo ENI"
3.  Selected an appropriate subnet and security group
4.  Attached the custom ENI to one EC2 instance, providing a secondary private IP
5.  Detached the ENI from the first instance (using force detach)
6.  Re-attached the ENI to the second instance
7.  Terminated both instances and observed ENI behavior; with both instances terminated, the Demo ENI persisted and was not removed / deleted

![ENI Creation](Images/eni-creation.png)
![ENI Attachment](Images/eni-attachment.png)

### Key Findings

* Custom ENIs persist independently of instance lifecycle
* ENIs can be moved between instances to facilitate network failover
* ENIs created alongside instances are automatically deleted when instances terminate
* Custom ENIs provide greater control over private IPv4 addressing

### Business Application

ENIs enable sophisticated networking scenarios such as:

* Creating management networks separated from application traffic
* Implementing network failover for high-availability workloads
* Attaching multiple security groups to a single instance
* Preserving IP addresses during instance replacement

<a name="ec2-hibernate"></a>
## EC2 Hibernate Feature

### Demonstration Overview

This demonstration implemented and tested EC2 hibernation to preserve instance state between stop/start cycles:

* Configuring hibernation requirements
* Testing the preservation of RAM state
* Verifying hibernation using the uptime command

### Implementation Steps

1.  Launched an EC2 instance with hibernate behavior enabled
2.  Ensured the root EBS volume was encrypted
3.  Verified adequate storage for RAM contents (8GB volume > 1GB RAM)
4.  Connected to the instance and ran the uptime command
5.  Hibernated the instance
6.  Started the instance again
7.  Verified that uptime continued from before hibernation

![Hibernate Configuration](Images/hibernate-configuration.png)
![Uptime Verification](Images/uptime-verification.png)

### Key Findings

* Hibernation preserves the instance's RAM state on the EBS volume
* From the OS perspective, hibernation is not a full shutdown
* Hibernation requires an encrypted root volume
* The root volume must have sufficient space to store RAM contents

### Business Application

Hibernation provides valuable capabilities for:

* Preserving application state without keeping instances running
* Reducing startup time for complex applications
* Maintaining long-running processes through instance stops
* Pre-warming applications to avoid cold starts

<a name="conclusion"></a>
## Conclusion

This portfolio demonstrates practical experience with key AWS EC2 features that are essential for designing robust cloud infrastructure. Through these hands-on demonstrations, I've developed skills in:

* Managing IP addressing and connectivity
* Optimizing instance placement for performance and availability
* Implementing advanced networking through ENIs
* Utilizing hibernation for state preservation

These capabilities enable the creation of EC2-based solutions that are reliable, performant, and cost-effective for a wide range of business applications.
 
