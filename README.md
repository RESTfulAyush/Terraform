# Terraform Project Setup

## Prerequisites
Before working with Terraform, ensure you have the following installed:

- **Terraform**: Download and install Terraform
- **AWS CLI**: Install and configure AWS CLI to interact with AWS resources
- **Git**: Ensure Git is installed for version control
- **Text Editor**: Use a code editor like VS Code, IntelliJ, or Vim

## Setup Instructions

### 1. Clone the Repository
```sh
# Clone an existing repository
$ git clone <repository-url>
$ cd <repository-folder>
```

### 2. Initialize Terraform
Run the following command to initialize Terraform, which downloads required provider plugins and sets up the backend.
```sh
$ terraform init
```

### 3. Validate Configuration
Before applying the configuration, validate the Terraform files.
```sh
$ terraform validate
```

### 4. Plan Execution
Check what changes Terraform will make to your infrastructure.
```sh
$ terraform plan
```

### 5. Apply Changes
Execute the plan to create or update the resources.
```sh
$ terraform apply
```
Confirm by typing `yes` when prompted.

### 6. Destroy Resources (If Needed)
To delete the deployed resources, use:
```sh
$ terraform destroy
```

## Best Practices
- **Use Git Ignore**: Prevent sensitive files from being committed by adding `terraform.tfstate`, `.terraform/`, `.DS_Store`, and private keys to `.gitignore`.
- **Manage State Remotely**: Store Terraform state in an S3 bucket with DynamoDB for locking.
- **Modularize Code**: Use modules for reusable infrastructure components.
- **Follow IAM Best Practices**: Use least privilege principles when assigning permissions.
