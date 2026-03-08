AWS 3-Tier Highly Available Architecture (Terraform)

This project deploys a production-style 3-tier architecture on AWS using Terraform.
It demonstrates high availability, scalability, and security best practices using Infrastructure as Code.

The infrastructure is deployed across multiple Availability Zones and includes load balancing, auto scaling, and a managed database.

Architecture Overview

This architecture follows the classic three-tier model:

Presentation Tier – Application Load Balancer

Application Tier – Auto Scaling EC2 instances

Data Tier – Managed relational database

Key AWS services used:

Amazon Virtual Private Cloud

Application Load Balancer

Amazon EC2 Auto Scaling

Amazon Elastic Compute Cloud

Amazon Relational Database Service

AWS Internet Gateway

Architecture Diagram
                    Users
                      │
                      ▼
              Internet Gateway
                      │
                      ▼
            Application Load Balancer
              (Public Subnets)
              AZ-1a        AZ-1b
                │             │
                ▼             ▼
           Web Tier Auto Scaling Group
            EC2 Instances (Apache)
          Private Subnet    Private Subnet
             AZ-1a             AZ-1b
                │
                ▼
            Application Layer
                │
                ▼
         Amazon RDS MySQL (Multi-AZ)
Key Features
High Availability

Infrastructure deployed across multiple Availability Zones

Load balancing distributes traffic between instances

Auto Scaling Group maintains healthy instance count

Scalability

Auto Scaling automatically adjusts capacity

Stateless EC2 instances allow horizontal scaling

Security

Layered Security Groups control traffic between tiers

Database is deployed in private subnets

RDS is not publicly accessible

Infrastructure as Code

Entire environment provisioned using Terraform

Fully reproducible and version controlled

Network Architecture
VPC

CIDR Block:

10.0.0.0/16
Subnets
Subnet	CIDR	AZ	Purpose
Public Subnet 1	10.0.1.0/24	us-east-1a	Load Balancer
Public Subnet 2	10.0.2.0/24	us-east-1b	Load Balancer
Private Subnet 1	10.0.3.0/24	us-east-1a	Application
Private Subnet 2	10.0.4.0/24	us-east-1b	Application + DB
Security Architecture

Traffic flow:

Internet
   │
   ▼
ALB Security Group
   │
   ▼
Web Security Group
   │
   ▼
App Security Group
   │
   ▼
DB Security Group

This creates layered security between tiers.

Compute Layer

The application layer uses:

EC2 instances launched via Launch Templates

Instances run Apache HTTP Server

Instances are managed by Auto Scaling Group

Startup script installs and runs Apache:

yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "Hello from Multi-AZ ASG" > /var/www/html/index.html
Database Layer

The data tier uses:

MySQL on Amazon RDS

Multi-AZ deployment

Private subnet placement

Benefits:

Automatic failover

Managed backups

No direct internet access

Terraform Resources Used

Main Terraform components:

aws_vpc
aws_subnet
aws_internet_gateway
aws_route_table
aws_security_group
aws_lb
aws_lb_target_group
aws_lb_listener
aws_launch_template
aws_autoscaling_group
aws_db_subnet_group
aws_db_instance
Deployment Instructions
1️⃣ Clone the repository
git clone https://github.com/yourusername/aws-3tier-terraform
cd aws-3tier-terraform
2️⃣ Initialize Terraform
terraform init
3️⃣ Plan deployment
terraform plan
4️⃣ Deploy infrastructure
terraform apply
Skills Demonstrated

This project demonstrates practical experience with:

AWS networking

Multi-AZ architecture

Load balancing

Auto scaling

Infrastructure as Code

Terraform

Secure VPC design

Future Improvements

Possible enhancements:

Add NAT Gateway

Add private application tier

Implement CI/CD pipeline

Add CloudWatch monitoring

Store secrets in AWS Secrets Manager

Author

Maema Mazunda

Aspiring Cloud Engineer focused on AWS architecture, automation, and infrastructure reliability.