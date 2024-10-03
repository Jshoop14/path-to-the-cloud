
# AWS CloudFormation and S3 Bucket Creation Summary

## Repository Setup
1. **Created a new repository** on GitHub for this project and **cloned it** to my local machine using PowerShell.
   - Used the command: `git clone https://github.com/<your-username>/<your-repo-name>.git` to clone the repository locally.

## YAML and CloudFormation
2. **Defined a YAML template** for AWS CloudFormation to create an S3 bucket.
   - The YAML file included definitions for resources and properties like `BucketName` and `AccessControl`.
   - Learned that **bucket names are globally unique**, meaning no two S3 buckets across AWS can have the same name.

### YAML Template for S3 Bucket in VS Code:
```yaml
AWSTemplateFormatVersion: '2010-09-09'
Description: CloudFormation template to create an S3 bucket

Resources:
  MyS3Bucket:
    Type: 'AWS::S3::Bucket'
    Properties:
      BucketName: my-cloudformation-bucket-2024
      AccessControl: Private
```
   - Edited the YAML file in **VS Code** and saved it as `cloudformation-bootcamp.yaml`.
   - Used VS Code extensions for **YAML syntax** and **AWS CloudFormation** to improve development and linting experience.

## CloudFormation Concepts
3. **Deployed the template** using AWS CloudFormation.
   - Created a stack from the template, which represents the set of AWS resources defined in the YAML file.
   - Worked with CloudFormation **templates**, **stacks**, and **changesets**:
     - **Templates**: Define the AWS resources and configurations.
     - **Stacks**: Are created from templates and represent the deployed resources.
     - **Changesets**: Allow reviewing changes before they are applied to a stack.

## Working with the Stack
4. Verified the creation of the **S3 bucket** in AWS:
   - The bucket was successfully created with private access control as specified in the YAML template.
   - Managed and monitored the CloudFormation stack using the AWS Console and CLI.

## Next Steps
Moving forward, I plan to explore more advanced CloudFormation features and dive into using **Terraform** as another infrastructure-as-code tool.
