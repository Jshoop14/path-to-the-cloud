# VPC Architecture Design Exercise 1 and 2(Weeks 5 & 6)

## Objective
The objective of this exercise was to design and implement a secure and highly available VPC architecture in AWS. The application needed a public-facing web component, while the backend database needed to be secured in private subnets.

## Architecture Diagram
![VPC Architecture Diagram](./images/VPC-Diagram.png)

## VPC Design
- **VPC CIDR Block**: We chose `10.0.0.0/16` as the CIDR block, providing ample IP addresses for the subnets.
- **Subnets**: Two public subnets and four private subnets, distributed across two Availability Zones for high availability.
  - **Public Subnets**: Used for Internet Gateway and NAT Gateway.
  - **Private Subnets**: Hosts the EC2 instances (application servers) and DynamoDB (databases).

## Security Measures
- **Internet Gateway**: Configured for public-facing components (web servers).
- **NAT Gateway**: Allows instances in private subnets to access the internet for updates.
- **Route Tables**: Configured to ensure proper routing for public and private subnets.
- **Private Subnet Security**: Ensures the database is accessible only from the application servers within the private subnet.

## Documentation
- **High Availability**: By distributing public and private subnets across two AZs, we ensure redundancy and fault tolerance.
- **Security**: Databases reside in private subnets, shielded from direct internet access, with access restricted to the application servers.
- **Scalability**: The VPC design allows for easy scaling by adding more subnets or modifying CIDR ranges.

[VPC Architecture Exercise](./VPC-Architecture-Exercise-2.md)
