🏗 Architecture Diagram

(Add your diagram image here in your repo)

![Architecture](architecture-diagram.png)

Architecture flow:

        Internet
            │
            ▼
     Internet Gateway
            │
            ▼
   Application Load Balancer
      (Public Subnets)
        AZ-1a     AZ-1b
          │         │
          ▼         ▼
    Auto Scaling Group
       EC2 Instances
      (Private Subnets)
          │
          ▼
     Amazon RDS MySQL
        (Multi-AZ)

Services used:

Amazon Virtual Private Cloud

Application Load Balancer

Amazon EC2 Auto Scaling

Amazon Elastic Compute Cloud

Amazon Relational Database Service

🌐 Network Architecture

VPC CIDR

10.0.0.0/16
Tier	Subnet	CIDR	Availability Zone
Public	Subnet 1	10.0.1.0/24	us-east-1a
Public	Subnet 2	10.0.2.0/24	us-east-1b
Private	Subnet 1	10.0.3.0/24	us-east-1a
Private	Subnet 2	10.0.4.0/24	us-east-1b
🔐 Security Architecture

Layered security between tiers.

Internet
   │
   ▼
ALB Security Group
   │
   ▼
Web Security Group
   │
   ▼
Application Security Group
   │
   ▼
Database Security Group

Security principles used:

✅ Least privilege access
✅ Private database tier
✅ Controlled tier-to-tier communication

⚙ Compute Layer

EC2 instances are deployed using:

Launch Templates

Auto Scaling Group

Multi-AZ placement

User data installs Apache automatically:

yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "Hello from Multi-AZ ASG" > /var/www/html/index.html
🗄 Database Layer

Database tier runs on:

MySQL on Amazon Relational Database Service

Features:

Multi-AZ deployment

Managed backups

Private subnet isolation

No public internet access

📦 Terraform Resources

Main Terraform resources used:

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
🚀 Deployment

Clone the repository

git clone https://github.com/yourusername/aws-3tier-terraform
cd aws-3tier-terraform

Initialize Terraform

terraform init

Plan infrastructure

terraform plan

Deploy infrastructure

terraform apply
📈 Skills Demonstrated

✔ AWS networking (VPC, Subnets, Routing)
✔ Multi-AZ architecture
✔ Load balancing
✔ Auto scaling
✔ Secure cloud architecture
✔ Infrastructure as Code
✔ Terraform