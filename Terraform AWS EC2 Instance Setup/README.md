# Terraform AWS EC2 Instance Setup

This Terraform configuration sets up an AWS EC2 instance with a security group that allows SSH and HTTP access.

## Prerequisites
- AWS CLI installed and configured
- Terraform installed
- An AWS account with appropriate IAM permissions

## Files Overview

### `instance.tf`
Defines an AWS EC2 instance with:
- AMI ID specified via a variable (`var.amiID`)
- Instance type `t3.micro`
- Security group attached (`dove-sg`)
- Availability zone defined via `var.zone1`

It also ensures the instance is always in a started state.

### `instID.tf`
- Fetches the most recent Ubuntu 22.04 AMI ID from AWS.
- Outputs the AMI ID for reference.

### `provider.tf`
- Configures AWS as the provider.
- Uses the region specified in `vars.tf`.

### `Secgrp.tf`
Defines a security group (`dove-sg`) with:
- **Ingress rules:**
  - Allows SSH (port 22) from any IP.
  - Allows HTTP (port 80) from any IP.
- **Egress rules:**
  - Allows all outbound IPv4 and IPv6 traffic.

### `vars.tf`
Defines variables for:
- AWS Region (`region`)
- Availability Zone (`zone1`)
- AMI ID map for different regions

## How to Use

### 1. Initialize Terraform
```sh
terraform init
```

### 2. Plan the Deployment
```sh
terraform plan
```
This command previews the changes that Terraform will apply.

### 3. Apply the Configuration
```sh
terraform apply
```
This command deploys the infrastructure.

### 4. Destroy Resources (If Needed)
```sh
terraform destroy
```
Removes all created resources.

## Notes
- Update the `amiID` variable in `vars.tf` if a different AMI is needed.
- Modify security group rules in `Secgrp.tf` as per security best practices.
