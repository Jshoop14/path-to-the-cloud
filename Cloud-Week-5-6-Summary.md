# Week 5 & 6: AWS Fundamentals

## AWS Global Infrastructure
- **Regions**: Physical locations worldwide with clusters of data centers.
- **Availability Zones (AZs)**: Isolated locations within a region, providing redundancy and reliability.
- **Local Zones**: Extend AWS infrastructure closer to users for latency-sensitive applications.
- **Edge Locations**: Used by services like AWS CloudFront to deliver content with low latency.
- **Multi-AZ Deployments**: Best practice for high availability and disaster recovery.

## Public vs Private Subnets
- **Public Subnets**: Typically used for front-end services that need direct internet access.
- **Private Subnets**: Used for back-end services like databases that don’t need internet exposure.
- **Multi-Tier Applications**: Deployed with public subnets handling web traffic and private subnets managing internal processing and data storage.

## Amazon VPC (Virtual Private Cloud)
- **What is a VPC**: A customizable virtual network within AWS.
- **CIDR Blocks**: IP range for your VPC (e.g., `10.0.0.0/16`).
- **CIDR Notation**: Explains how IP addresses and subnets are expressed (e.g., `/24` for a subnet mask).
- **Subnets within a VPC**: Divides your VPC into smaller, isolated networks.
- **Route Tables**: Manage how traffic is directed between subnets and outside the VPC.
  - **Custom Route Tables**: Created to direct traffic differently than the main route table.
- **Internet Gateway**: Provides internet access to public subnets.
- **NAT Gateways**: Allows private subnets to access the internet for updates without exposing them to the public.
- **Security Groups (SG)**: Virtual firewalls controlling traffic to your instances.
- **NACL (Network Access Control Lists)**: Stateless firewalls for controlling traffic at the subnet level.

## AWS IAM (Identity and Access Management)
- **MFA (Multi-Factor Authentication)**: Adds an extra layer of security for users.
- **Integration and Federation**: Federating user identities from external sources into AWS.
- **Key IAM Concepts**:
  - **Users**: Individuals who can interact with AWS.
  - **Groups**: Collections of users with common permissions.
  - **Roles**: Temporary access policies for AWS resources.
  - **Permissions & Policies**: Define what actions users and roles can perform in AWS.
  - **Identity Federation**: Allows users to log in using external identity providers (e.g., Google, Active Directory).

## Conclusion:
This exercise emphasized creating a secure and scalable VPC setup in AWS with bastion hosts, public and private subnets, NAT gateways, and proper security configurations to control traffic and access.


## VPC Architecture Design Exercise

In this exercise, we designed a secure VPC architecture with high availability across two Availability Zones (AZs), utilizing various AWS services such as EC2, NAT Gateways, Internet Gateways, and DynamoDB.

For the complete exercise, please see the dedicated VPC Architecture section:
[VPC Architecture Exercise](./VPC-Arcitecture-Exercise.md)

## VPC Project in AWS Exercise 2
**Objective**: Create a secure VPC architecture based on the designed diagram from earlier.

1. **Created the VPC**:
   - Launched a **bastion host** to securely connect to instances in private subnets.
   - **Key pair** created to authenticate the connection.
   - Selected the **public subnet 1** for bastion, ensuring it has a public IP assigned.
   - **Security Group**: Configured to allow SSH access from the local IP.

2. **Connected to EC2 Instance**:
   - **Public IP** for the bastion host was grabbed, and SSH was initiated from the local machine.

3. **Testing VPC Connectivity**:
   - Deleted the route from **public subnet 1** to the **Internet Gateway** and tested if the instance could be accessed (could not).
   - Re-added the route, and the connection was successful again.

4. **Private Subnet EC2 Instances**:
   - Launched EC2 instances in **private subnets** 1 and 2.
   - For simplicity, used the **bastion host's key pair** to connect to them.
   - Security groups allowed SSH access between the bastion and the private instances.

5. **Verifying Communication**:
   - Pinged **EC2App2** from **EC2App1** to verify internal communication between private subnets.
   - Removed security group permissions between the two instances, verifying that they could no longer communicate (ping failed).
   
6. **Termination**:
   - Terminated the instances to prevent unnecessary costs.
