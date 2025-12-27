# Terraform Interactive

This is my collection of Terraform examples and learning modules covering AWS infrastructure, Docker containers, and various Terraform concepts. This repository serves as a hands-on learning resource for Terraform best practices, patterns, and real-world implementations.

## 📋 Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Repository Structure](#repository-structure)
- [AWS Terraform Modules](#aws-terraform-modules)
- [Docker Terraform Examples](#docker-terraform-examples)
- [EC2 Tasks](#ec2-tasks)
- [IAM Tasks](#iam-tasks)
- [Advanced Configurations](#advanced-configurations)
- [Usage](#usage)
- [Contributing](#contributing)

## 🎯 Overview

This repository contains practical Terraform examples organized by topic and use case. Each module demonstrates specific Terraform concepts, AWS services, or infrastructure patterns that can be used as reference implementations or learning materials.

## 🔧 Prerequisites

Before using these Terraform configurations, ensure you have:

- **Terraform** >= 0.12 installed ([Download](https://www.terraform.io/downloads))
- **AWS CLI** configured with appropriate credentials
- **Docker** installed (for Docker-related examples)
- Basic understanding of Terraform syntax and AWS services

## 📁 Repository Structure

```
terraform-interactive/
├── aws-terraform/          # AWS infrastructure examples
├── terraform-docker/       # Docker container examples
├── terraform-ec2-tasks/    # EC2-specific tasks
├── terraform-iam-tasks/    # IAM-specific tasks
├── terraform-test/         # Testing configurations
├── tf-spot-autoscaling-ec2/ # Spot instance autoscaling
└── tf-spot-blueprint-eks/   # EKS with spot instances
```

## ☁️ AWS Terraform Modules

### EC2 Instances

#### `ec2-datasource/`
Demonstrates using data sources to fetch AMI IDs and key pairs dynamically.

**Key Features:**
- AMI data source lookup for Amazon Linux 2
- Key pair data source
- Security group configuration
- User data scripts for application installation

**Files:**
- `ec2_instance.tf` - EC2 instance resource
- `ami_datasource.tf` - AMI data source
- `key_pair_data_source.tf` - Key pair data source
- `security_group.tf` - Security group definitions
- `app1-install.sh` - User data script

#### `ec2-for-each/`
Shows how to use `for_each` to create multiple EC2 instances across availability zones.

**Key Features:**
- Dynamic instance creation using `for_each`
- Availability zone distribution
- Data source for availability zones

#### `ec2-map-loops/`
Demonstrates using map-based loops for EC2 instance creation.

**Key Features:**
- Map-based iteration patterns
- Multiple instance configurations

#### `ec2-null-resource/`
Explores the `null_resource` provisioner for executing local commands.

**Key Features:**
- Local-exec provisioners
- Command execution with different interpreters
- Environment variables
- Dependency management with `depends_on`

### S3 Website Hosting

#### `aws-s3-website/`
Complete S3 static website hosting configuration.

**Key Features:**
- Public-read bucket ACL
- Bucket policy for public access
- Website configuration (index/error documents)
- Tagging support
- Force destroy enabled (testing only)

**Files:**
- `main.tf` - S3 bucket resource
- `variables.tf` - Input variables
- `outputs.tf` - Output values
- `terraform.tfvars` - Variable values

### Auto Scaling Groups

#### `aws-asg/`
Auto Scaling Group configuration with launch templates.

**Key Features:**
- Launch configuration
- Target group integration
- Health check configuration
- Instance refresh with rolling strategy
- VPC zone identifier

### IAM

#### `IAM/`
IAM user and group management examples.

**Key Features:**
- IAM user creation
- IAM policy definition
- Policy attachments
- IAM groups configuration

**Files:**
- `iam-user.tf` - User and policy resources
- `iam_groups/groups.tf` - Group configurations

### Remote Backend

#### `remote-backend-s3/`
Configuration for using S3 as a Terraform remote backend.

**Key Features:**
- S3 backend configuration
- State file management

### API Gateway

#### `tf-api/`
Terraform API Gateway configuration examples.

## 🐳 Docker Terraform Examples

### Basic Docker Operations

#### `docker-main-basic/`
Basic Docker container management with Terraform.

**Key Features:**
- Docker image pulling
- Container creation
- Port mapping
- Random string generation for unique names
- Join function usage

#### `docker-module/`
Modular Docker configuration demonstrating Terraform module structure.

**Key Features:**
- Module-based architecture
- Reusable Docker image module
- Input/output variables
- Provider configuration

**Structure:**
```
docker-module/
├── main.tf              # Root module
├── variables.tf         # Root variables
├── outputs.tf           # Root outputs
└── image/               # Image submodule
    ├── main.tf
    ├── variables.tf
    └── outputs.tf
```

### Advanced Docker Concepts

#### `splat-expression/`
Demonstrates Terraform splat expressions (`[*]`) for accessing multiple resource attributes.

**Key Features:**
- Splat expressions for lists
- Multiple container creation with `count`
- Output formatting

#### `var-validation/`
Shows variable validation rules in Terraform.

**Key Features:**
- Input validation
- Custom error messages
- Type constraints

#### `map-lookup/`
Map data structure usage and lookup functions.

**Key Features:**
- Map variables
- Lookup functions
- Dynamic value selection

#### `multiple-resources-count/`
Creating multiple resources using the `count` meta-argument.

**Key Features:**
- Count-based resource creation
- Index-based naming

#### `dynamic-ingress/`
Dynamic block usage for security group rules.

**Key Features:**
- Dynamic blocks
- Flexible ingress rules

## 🖥️ EC2 Tasks

Practical EC2 implementation tasks with real-world scenarios.

### `ec2-task1/`
WordPress EC2 instance with Route53 DNS configuration.

**Key Features:**
- EC2 instance with WordPress
- Key pair management
- Security group configuration
- Route53 DNS record
- User data scripts
- Monitoring enabled

## 🚀 Advanced Configurations

### Spot Instances & EKS

#### `tf-spot-blueprint-eks/`
Complete EKS cluster configuration with spot instance node groups.

**Key Features:**
- EKS cluster creation
- Multiple spot instance node groups
- IAM roles for EKS cluster and nodes
- VPC, subnets, and networking
- Security groups
- Multiple instance type support (c3/c4/c5, m3/m4/m5, r3/r4/r5)
- Capacity type: SPOT

**Resources:**
- EKS Cluster
- 3 Node Groups with different instance families
- VPC with 5 subnets across availability zones
- Internet Gateway and Route Tables
- IAM roles and policies

#### `tf-spot-autoscaling-ec2/`
EC2 autoscaling with spot instances configuration.

## 📖 Usage

### Getting Started

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd terraform-interactive
   ```

2. **Navigate to a specific module:**
   ```bash
   cd aws-terraform/ec2-datasource
   ```

3. **Initialize Terraform:**
   ```bash
   terraform init
   ```

4. **Review the execution plan:**
   ```bash
   terraform plan
   ```

5. **Apply the configuration:**
   ```bash
   terraform apply
   ```

### Module-Specific Usage

#### AWS S3 Website
```bash
cd aws-terraform/aws-s3-website
terraform init
terraform plan -var-file="terraform.tfvars"
terraform apply
```

#### Docker Containers
```bash
cd terraform-docker/docker-main-basic
terraform init
terraform apply
```

#### EKS Cluster
```bash
cd tf-spot-blueprint-eks
terraform init
terraform plan
terraform apply
```

### Variable Configuration

Most modules use `terraform.tfvars` files for variable values. Create or modify these files to customize configurations:

```hcl
# Example terraform.tfvars
bucket_name = "my-unique-bucket-name"
region      = "us-east-1"
```

## ⚠️ Important Notes

1. **Cost Awareness:** Some configurations create billable AWS resources. Always review costs before applying.

2. **Security:** 
   - Review security group rules before applying
   - Some examples use `force_destroy = true` - remove this in production
   - Key pairs and credentials should be managed securely

3. **Testing Environment:** Many configurations are designed for testing/learning. Review and adapt for production use.

4. **State Management:** Consider using remote backends (S3) for state management in team environments.

5. **Provider Versions:** Check `versions.tf` or provider blocks for required provider versions.

## 🧪 Testing

The `terraform-test/` directory contains configurations for testing Terraform functionality.

## 📝 Best Practices Demonstrated

- **Data Sources:** Using data sources instead of hardcoding values
- **Variables:** Proper variable usage and validation
- **Outputs:** Useful output definitions
- **Modules:** Modular code organization
- **Loops:** `for_each` and `count` for resource iteration
- **Provisioners:** Local-exec for external commands
- **Dependencies:** Proper `depends_on` usage
- **State Management:** Remote backend configuration

## 🔍 Key Terraform Concepts Covered

- ✅ Data Sources
- ✅ Variables and Outputs
- ✅ Modules
- ✅ `for_each` and `count` meta-arguments
- ✅ Splat Expressions
- ✅ Dynamic Blocks
- ✅ Null Resources
- ✅ Provisioners
- ✅ Remote State
- ✅ Variable Validation
- ✅ Map and Lookup Functions
- ✅ Join and String Functions

## 🤝 Contributing

This is a learning repository. Feel free to:
- Add more examples
- Improve documentation
- Fix issues
- Share best practices

## 📚 Additional Resources

- [Terraform Documentation](https://www.terraform.io/docs)
- [AWS Provider Documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Docker Provider Documentation](https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs)

## 📄 License

This repository is for educational purposes. Use at your own discretion.

---

**Happy Terraforming! 🚀**
