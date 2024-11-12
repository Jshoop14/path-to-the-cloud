### Terraform Cheat Sheet

#### Basic Commands

- **`terraform init`**: Initializes a Terraform configuration. Downloads plugins and sets up the working directory.
- **`terraform validate`**: Validates the configuration files for syntax correctness.
- **`terraform plan`**: Creates an execution plan, showing the resources that will be created, updated, or destroyed.
- **`terraform apply`**: Applies the changes required to reach the desired state of the configuration.
- **`terraform destroy`**: Destroys all resources managed by the current configuration.
- **`terraform fmt`**: Formats the code to the standard style.
- **`terraform show`**: Shows the current or past Terraform state.
- **`terraform output`**: Displays the output variables of your Terraform configuration.
- **`terraform state`**: Interacts with the state file. Useful for manipulating resources manually.

#### File Structure

- **`main.tf`**: The main Terraform configuration file, used to define resources.
- **`variables.tf`**: Defines input variables used in the configuration.
- **`outputs.tf`**: Defines output values that can be used to pass information to other configurations.
- **`provider.tf`**: Defines the cloud providers (e.g., AWS, Azure, GCP) to use in the configuration.
- **`data.tf`**: Fetches data from existing infrastructure (e.g., AMIs).

#### Common Resource Syntax

```hcl
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  tags = {
    Name = "ExampleInstance"
  }
}
```
- **`resource`**: The resource block to create or manage a resource.
- **`aws_instance`**: Resource type, here an EC2 instance.
- **`example`**: The name of the resource.

#### Variables

- **Defining Variables**:
  ```hcl
  variable "instance_type" {
    description = "The type of instance to use"
    type        = string
    default     = "t2.micro"
  }
  ```
- **Using Variables**:
  ```hcl
  resource "aws_instance" "example" {
    instance_type = var.instance_type
  }
  ```

#### Outputs

- **Defining Outputs**:
  ```hcl
  output "instance_ip" {
    description = "The public IP address of the instance"
    value       = aws_instance.example.public_ip
  }
  ```
- **Usage**: Outputs provide useful information after running `terraform apply`.

#### Data Sources

- **Using Data Sources**:
  ```hcl
  data "aws_ami" "ubuntu" {
    most_recent = true

    filter {
      name   = "name"
      values = ["ubuntu/images/hvm-ssd/ubuntu-focal-20.04-amd64-server-*"]
    }

    owners = ["099720109477"]
  }
  ```
- **Purpose**: Data sources are used to reference existing resources, such as finding the latest AMI.

#### Providers

- **Defining a Provider**:
  ```hcl
  provider "aws" {
    region = "us-east-1"
  }
  ```
- **Purpose**: Providers are plugins that Terraform uses to interact with cloud platforms or services.

#### State Management

- **`terraform state list`**: Lists all resources in the state.
- **`terraform state show <resource>`**: Shows details about a specific resource.
- **`terraform state rm <resource>`**: Removes a resource from the state.

#### Backends

- **Local State**: Stores `terraform.tfstate` in the working directory.
- **Remote State**: Recommended for collaboration. Can be stored in S3, Azure Blob Storage, etc.
  ```hcl
  terraform {
    backend "s3" {
      bucket = "my-terraform-state"
      key    = "path/to/my/key"
      region = "us-east-1"
    }
  }
  ```

#### Modules

- **Using Modules**:
  ```hcl
  module "vpc" {
    source = "terraform-aws-modules/vpc/aws"
    version = "3.0.0"
    name   = "my-vpc"
    cidr   = "10.0.0.0/16"
  }
  ```
- **Purpose**: Modules are reusable sets of Terraform resources that can be easily integrated into multiple configurations.

#### Best Practices

1. **Use Version Control**: Always use version control for your Terraform code.
2. **Use Remote State Storage**: Store the state remotely to enable team collaboration.
3. **Organize Code into Modules**: Use modules to create reusable and maintainable code.
4. **Secure State File**: State files may contain sensitive information; make sure they are secured.
5. **Run `terraform plan` Before `apply`**: Always check the execution plan before applying changes to avoid surprises.

#### Useful Tips

- **Formatting**: Run `terraform fmt` to keep your code clean and consistent.
- **State File Security**: Do not commit your state file (`terraform.tfstate`) to version control.
- **Variable Files**: Use `terraform.tfvars` to define variable values for different environments.
- **Environment Variables**: You can set credentials or other values using environment variables (e.g., `AWS_ACCESS_KEY_ID`).

#### Common Errors

- **Error: No valid credential sources found for AWS Provider**: Make sure your AWS credentials are configured properly (`~/.aws/credentials` or environment variables).
- **Error: Resource already exists**: Terraform cannot import existing resources automatically; use `terraform import`.

#### Commands for Collaboration

- **`terraform state push` / `terraform state pull`**: Useful for sharing state between team members.
- **`terraform lock`**: Locks the state to prevent concurrent modifications.
