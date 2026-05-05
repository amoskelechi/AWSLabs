# Terraform Lab — Automated AWS VPC Infrastructure
=====================================================

## What This Lab Does
Uses Terraform (Infrastructure as Code) to automatically build
an AWS networking setup that would normally take 30+ minutes
to create manually through the AWS Console.

## Resources Created (12 Total)
- 1 Custom VPC (10.0.0.0/16)
- 2 Public Subnets (us-east-1a and us-east-1b)
- 2 Private Subnets (us-east-1a and us-east-1b)
- 1 Internet Gateway
- 1 Public Route Table (routes traffic to IGW)
- 1 Private Route Table (local traffic only)
- 4 Route Table Associations

## Prerequisites
- Terraform installed (v1.5.0 or higher)
- AWS CLI installed and configured
- AWS credentials (Access Key and Secret Key)

## Steps Followed

### Step 1 - Clone the Lab Repository
git clone https://github.com/Nikiobilor/cloud-eng-program.git
cd cloud-eng-program

### Step 2 - Configure AWS Credentials
aws configure
# Entered AWS Access Key ID
# Entered AWS Secret Access Key
# Set default region to us-east-1
# Set output format to json

### Step 3 - Initialize Terraform
terraform init
# Downloads the AWS provider plugin (hashicorp/aws v5.100.0)
# Creates .terraform.lock.hcl file to lock provider versions

### Step 4 - Preview the Infrastructure Plan
terraform plan
# Shows exactly what Terraform will create before applying
# Output confirmed: Plan: 12 to add, 0 to change, 0 to destroy

### Step 5 - Apply and Build the Infrastructure
terraform apply
# Typed 'yes' to confirm
# Terraform built all 12 resources automatically in under 60 seconds
# Output confirmed: Apply complete! Resources: 12 added, 0 changed, 0 destroyed

## Terraform Outputs After Apply
- vpc_id                = vpc-0f677b6242bceb1e8
- vpc_cidr              = 10.0.0.0/16
- internet_gateway_id   = igw-0a2ce2d4246c2a50a
- public_subnet_ids     = [subnet-081468f219ca71910, subnet-0b09b85b750cf9549]
- private_subnet_ids    = [subnet-062a998741cfb8e5e, subnet-0cb6df27a589a533c]
- public_route_table_id = rtb-0e6ee3162d4d5ce9e
- private_route_table_id= rtb-08179f440e54adb17

### Step 6 - Destroy the Infrastructure (Cleanup)
terraform destroy
# Typed 'yes' to confirm
# All 12 resources deleted cleanly to avoid AWS charges

## Key Terraform Commands Learned
| Command          | What it does                              |
|------------------|-------------------------------------------|
| terraform init   | Downloads required provider plugins       |
| terraform plan   | Previews what will be created             |
| terraform apply  | Builds the infrastructure on AWS         |
| terraform destroy| Tears down all created resources         |

## Files in This Lab
| File          | Purpose                                      |
|---------------|----------------------------------------------|
| main.tf       | Defines all AWS resources to be created      |
| variables.tf  | Defines input variables with default values  |
| outputs.tf    | Defines what info to display after apply     |
