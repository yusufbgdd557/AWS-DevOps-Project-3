# AWS DevOps Project 3 : Automating EC2 Deployment with Terraform on AWS

This project uses Terraform to create an EC2 instance on AWS, specifically with the Amazon Linux 2 AMI. Below are the detailed steps of how the project was executed.

## Steps to Reproduce

1. **Create EC2 Instance to Use as the Machine**  
   First, create an EC2 instance that will be used as the machine where Terraform will be installed.

2. **Install Terraform on Amazon Linux 2**  
   Install Terraform using the following commands:
   ```bash
   sudo yum install -y yum-utils shadow-utils
   sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
   sudo yum -y install terraform
   ```

3. **Verify AWS CLI Installation**  
   AWS CLI might already be installed by default on Amazon Linux 2. You can verify by running:
   ```bash
   aws --version
   ```
   If it's not installed, run:
   ```bash
   sudo yum install -y aws-cli
   ```

4. **Create Project Directory**  
   Create a directory for your Terraform project:
   ```bash
   mkdir my-terraform-project
   cd my-terraform-project
   ```

5. **Create Configuration Files**  
   Use the `touch` command to create empty Terraform files:
   ```bash
   touch main.tf variables.tf
   ```

6. **Edit Configuration Files**  
   Open and edit the configuration files using `vim`:
   ```bash
   vim main.tf
   vim variables.tf
   ```
   - Press `i` to insert text.
   - After editing, press `esc` followed by `:wq` to save and exit.

7. **Configure AWS Credentials**  
   Run the following command to configure access to your AWS account:
   ```bash
   aws configure
   ```
   Provide your access key, secret key, region, and output(i.e. JSON) format.

8. **Initialize Terraform**  
   Initialize Terraform in your project directory:
   ```bash
   terraform init
   ```

9. **Validate Configuration**  
   Validate your Terraform configuration:
   ```bash
   terraform validate
   ```

10. **Plan Terraform Execution**  
    Generate and review an execution plan:
    ```bash
    terraform plan
    ```

11. **Apply Terraform Configuration**  
    Apply the configuration to create your EC2 instance:
    ```bash
    terraform apply
    ```

12. **Verify EC2 Creation**  
    After Terraform completes, verify that your EC2 instance is running by checking the AWS Console.

## `main.tf` Configuration

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_name

  tags = {
    Name = "Second EC2"
  }
}
```

## `variables.tf` Configuration

```hcl
variable "ami_id" {
  description = "The AMI to use to install it inside the EC2 instance"
  default     = "ami-02c21308fed24a8ab"
}

variable "instance_type" {
  description = "Instance type"
  default     = "t2.micro"
}

variable "key_name" {
  description = "Key pair file name"
  default     = "connectionkeypair" # use your keypair 
}
```


## Project Screenshots

1. **Terraform Installed and AWS Configured**  
   Terraform installation and AWS account configuration have been completed successfully.  
   ![Screenshot 1](https://github.com/user-attachments/assets/32df7ccb-e514-4760-8093-ade40b356ade)
   
   ![Screenshot 8](https://github.com/user-attachments/assets/995bfba6-7909-4b9c-812a-1aa9ba5f4646)

3. **Instance Created**  
   EC2 instance has been created using Terraform. Verification through the AWS console confirms that the instance is running as expected.  
   ![Screenshot 2](https://github.com/user-attachments/assets/40cf6fc6-e7de-4f37-b3a6-8c186de9fadb)
   
   ![Screenshot 3](https://github.com/user-attachments/assets/a1b397a3-893d-41d8-9856-1629e32d497e)

5. **Instance Destroyed**  
   The EC2 instance was successfully destroyed, and verification through the AWS console confirms its termination.  
   ![Screenshot 4](https://github.com/user-attachments/assets/2d8ded63-1cef-4897-b479-f1106dac2cfa)
   
   ![Screenshot 5](https://github.com/user-attachments/assets/374e0307-beb3-4116-9e57-529800105b3c)

---
