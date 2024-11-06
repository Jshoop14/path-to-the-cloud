### Lab: Benefits of Infrastructure as Code (IaC)

**Summary**:
This lab walks through the process of deploying and managing AWS infrastructure using both manual methods and Terraform. The key objective is to demonstrate the benefits of Infrastructure as Code (IaC) for simplifying cloud adoption, automating infrastructure provisioning, and reducing manual errors.

**Key Benefits of IaC**:
- **Simplification of Cloud Adoption**: IaC makes cloud adoption easier by automating many manual steps.
- **Automation of Approved Requests**: Infrastructure requests can be automated, reducing delays caused by manual ticketing.
- **Capacity On-Demand**: IaC allows on-demand infrastructure provisioning, often through self-service capabilities for developers.
- **Standardization and Consistency**: IaC drives consistency throughout an organization, reducing errors and increasing efficiency.

**Lab Tasks**:

1. **Create a New VPC**:
   - Set up a Virtual Private Cloud (VPC) in the `us-east-1` region for a proof of concept environment.

2. **Create Public and Private Subnets**:
   - Deploy public and private subnets across three Availability Zones for redundancy and failover testing.

3. **Deploy an Internet Gateway (IGW)**:
   - Attach an Internet Gateway to the VPC to provide internet access for the public subnets.

4. **Provision a NAT Gateway**:
   - Set up a NAT Gateway to provide outbound internet connectivity for private subnets while keeping them inaccessible from outside.

5. **Configure Route Tables**:
   - Create and configure route tables to ensure traffic is properly routed between public and private subnets.

6. **Delete the VPC Resources**:
   - Manually delete the VPC and all associated resources.

7. **Prepare Files and Credentials for Terraform**:
   - Create `main.tf` and `variables.tf` files to define the infrastructure and prepare AWS credentials for Terraform deployment.

8. **Set Credentials for Terraform**:
   - Set environment variables for AWS access keys to authenticate Terraform actions.

9. **Deploy Infrastructure Using Terraform**:
   - Use `terraform init`, `terraform plan`, and `terraform apply` to automate the creation of the same infrastructure setup.

10. **Clean Up AWS Resources Using Terraform**:
    - Run `terraform destroy` to remove all the resources created, ensuring a clean environment without residual costs.

**Benefits of Using Terraform for IaC**:
- **Automation**: Automates the deployment of cloud resources, saving time and reducing manual errors.
- **Idempotency**: Ensures that applying changes multiple times yields the same result, making changes predictable and consistent.
- **Scalability**: Using Terraform, deploying infrastructure across multiple environments or accounts becomes efficient and repeatable.

**Note**: Remember to add `.terraform/`, `terraform.tfstate`, `terraform.tfstate.backup`, and `Benefits of IaC Lab.md` to your `.gitignore` file to avoid committing sensitive state information and unnecessary files.
