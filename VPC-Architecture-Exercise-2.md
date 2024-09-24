
# VPC Project in AWS Exercise 2

## Step 1: Creating the VPC
I created a **Virtual Private Cloud (VPC)** based on the **diagram** designed earlier. The VPC allows me to create an isolated network in AWS, where I can launch resources like EC2 instances with fine-grained control over networking. 
The **VPC** was assigned a **CIDR block** (such as `10.0.0.0/16`), which allocates IP addresses for subnets inside the VPC.

## Step 2: Setting up Bastion Hosts
A **bastion host** (sometimes called a jump box) is a special-purpose EC2 instance used to securely connect to instances in **private subnets**. Since the private instances don’t have direct internet access, the bastion serves as a middleman.
I created a **key pair** for SSH authentication with the bastion host. AWS key pairs consist of a public and private key and are essential for secure SSH access to EC2 instances.

## Step 3: Selecting the VPC and Subnets
I launched the bastion host in **public subnet 1** of the VPC. Since public subnets are connected to the **Internet Gateway (IGW)**, they allow inbound and outbound traffic to the internet.
When launching the instance, I opted to **auto-assign a public IP**, enabling the bastion host to communicate with the internet.

## Step 4: Configuring Security Groups
A **Security Group (SG)** acts as a virtual firewall for EC2 instances. I created an SG for the bastion host to manage which IP addresses can access it via **SSH (port 22)**.
The inbound rule allowed access from my **private local IP** (e.g., my workstation’s IP address), restricting unauthorized external access.

## Step 5: Launching the Bastion Host
After setting up the security groups and network configurations, I **launched the instance**.
I then **grabbed the public IP** of the bastion host from the AWS console and connected to it via SSH from my local machine using the command:
```bash
ssh -i bastion.pem ec2-user@<bastion-public-ip>
```

## Step 6: Testing Route Table for Public Subnet
After connecting to the instance, I **deleted the route from public subnet 1** to the Internet Gateway (IGW). This broke the internet connectivity of the instances in that subnet, making it impossible to SSH into the bastion host.
To confirm, I attempted to reconnect via SSH and verified that it **failed**, as there was no route to the internet.
I then **re-added the route** to the IGW, and connectivity was restored, allowing me to connect to the bastion host once again.

## Step 7: Creating EC2 Instances in Private Subnets
Next, I created EC2 instances in **private subnets** 1 and 2. These subnets don’t have direct access to the internet (no Internet Gateway), but the instances inside can communicate with each other.
Ideally, different **key pairs** would be used for each instance for added security, but for simplicity, I used the **same key pair as the bastion host** for SSH access.

## Step 8: Configuring Security Groups for Private Instances
I created **Security Groups** for the EC2 instances in **Availability Zone 1** and **Availability Zone 2**, naming them descriptively (e.g., **EC2App1** for the instance in private subnet 1).
To enable communication between the bastion host and **EC2App1**, I updated the **Security Group** to allow SSH access from the bastion host's SG.
Additionally, I added an **inbound rule** to **EC2App2** allowing **ICMP (ping) traffic** from **EC2App1**. This was done to test connectivity between the two private instances.

## Step 9: Testing SSH and Internal Communication
I **SSH’d into EC2App1** from the bastion host using the private IP:
```bash
ssh -i bastion.pem ec2-user@10.0.130.250
```
Once logged into EC2App1, I **pinged EC2App2** to verify internal communication:
```bash
ping 10.0.152.108
```
This confirmed that the two instances could communicate over the private network, showing that the routing and security group configuration were correct.

## Step 10: Disconnecting Communication Between the Two EC2 Instances
To simulate a scenario where communication between the private instances is restricted, I **deleted the security group rule** allowing traffic between EC2App1 and EC2App2.
After removing the rule, I tried **pinging EC2App2** from EC2App1 again and found that the communication was no longer possible. This demonstrated the effect of changing security group configurations on instance communication.

## Step 11: Terminating the Instances
To avoid unnecessary costs, I **terminated** all the instances after testing. This is an essential practice when working in AWS, especially with EC2, as instances running with attached resources (like storage) can accumulate charges.

## Conclusion:
This exercise walked through the process of setting up a secure and scalable VPC environment in AWS, with both public-facing and internal resources. By configuring bastion hosts, security groups, and testing internal communication, I verified the effectiveness of the VPC setup and its network isolation for different tiers of the application.
