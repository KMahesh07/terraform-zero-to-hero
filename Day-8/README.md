# MIGRATION TO TERRAFORM & DRIFT DETECTION
https://youtu.be/-4IMy5ihiiU
# How to use Terraform import? 
- Terraform import is a command that allows you to import existing infrastructure resources into your Terraform configuration so that you can manage them using Terraform. 
- This is useful when you have existing resources that were created outside of Terraform, and you want to start managing them with Terraform without destroying and recreating them. Here are the steps to use terraform import with an example:

## Step 1: Create a Terraform Configuration

First, create a new directory for your Terraform configuration and create a .tf file for your resources.
-  Let's assume you want to import an existing AWS EC2 instance. Create a file named main.tf:
```bash
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"  # Replace with the AMI ID of your existing EC2 instance
  instance_type = "t2.micro"
}

```
In this example, we have a basic Terraform configuration that defines an AWS provider and an AWS EC2 instance resource.

## Step 2: Initialize the Terraform Configuration

Run the following command to initialize your Terraform configuration and download the necessary providers:

```bash
terraform init
```
## Step 3: Import the Existing Resource

Now, you need to use the terraform import command to import your existing resource. The syntax for terraform import is as follows:

```bash
terraform import RESOURCE_TYPE.NAME IMPORT_ID
```

- RESOURCE_TYPE: The Terraform resource type you want to import (e.g., aws_instance).
- NAME: A name you choose for this resource within Terraform.
- IMPORT_ID: The identifier of the existing resource you want to import. This varies depending on the resource type.

- For an AWS EC2 instance, the IMPORT_ID would typically be the EC2 instance ID. Let's assume the EC2 instance ID is i-0123456789abcdef0. Run the following command to import the resource:

```bash

terraform import aws_instance.example i-0123456789abcdef0

```
Terraform will associate the imported resource with the specified aws_instance.example in your configuration.

## Step 4: Plan and Apply

- Now that the resource is imported, you can use Terraform as you normally would. Run the following commands to plan and apply your Terraform configuration:

```bash
terraform plan
terraform apply
```
Terraform will analyze your configuration and make any necessary changes to bring the imported resource under Terraform management. In this case, if there are any differences between your existing EC2 instance and the Terraform configuration (e.g., instance type or security groups), Terraform will attempt to make those changes.

## Step 5: Verify

- After applying the Terraform configuration, you can verify that the imported resource is being managed by Terraform by checking the Terraform state:

```bash
terraform show
```
This will display the current state of your infrastructure, including the imported resource
