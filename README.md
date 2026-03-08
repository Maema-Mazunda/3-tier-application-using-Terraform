AWS 3-Tier Architecture with Terraform

A production-ready, multi-AZ 3-tier web application infrastructure provisioned entirely with Terraform.


Architecture
                        Internet (0.0.0.0/0)
                               │
                               │ HTTP :80
                    ┌──────────▼──────────┐
                    │  Application Load   │
                    │     Balancer        │
                    │      alb-sg         │
                    └────┬──────────┬─────┘
                         │          │
               ┌─────────▼──┐  ┌────▼───────────┐
               │Public Sub 1│  │ Public Sub 2   │
               │10.0.1.0/24 │  │ 10.0.2.0/24   │
               │us-east-1a  │  │ us-east-1b    │
               └────────────┘  └───────────────┘
                         │          │
                    ┌────▼──────────▼─────┐
                    │   TIER 1 — WEB      │
                    │  Auto Scaling Group  │
                    │  EC2 · t2.micro      │
                    │  Apache HTTPD        │
                    │  min:2  max:4        │
                    │  web-sg              │
                    └────┬──────────┬─────┘
                         │          │
               ┌─────────▼──┐  ┌────▼───────────┐
               │Private Sub1│  │ Private Sub 2  │
               │10.0.3.0/24 │  │ 10.0.4.0/24   │
               │us-east-1a  │  │ us-east-1b    │
               └────────────┘  └───────────────┘
                         │          │
                    ┌────▼──────────▼─────┐
                    │  TIER 2 — DATABASE  │
                    │   RDS MySQL 8.0     │
                    │   Multi-AZ          │
                    │   db.t3.micro       │
                    │   db-sg · :3306     │
                    └─────────────────────┘

Security Groups
Internet ──► alb-sg  (port 80, open)
                │
                ▼
             web-sg  (port 80 from alb-sg only)
                │
                ▼
              db-sg  (port 3306 from web-sg only)

Network Layout
ResourceCIDRZoneAccessVPC10.0.0.0/16——Public Subnet 110.0.1.0/24us-east-1aInternet-facing (ALB)Public Subnet 210.0.2.0/24us-east-1bInternet-facing (ALB)Private Subnet 110.0.3.0/24us-east-1aInternal (EC2 + RDS)Private Subnet 210.0.4.0/24us-east-1bInternal (EC2 + RDS)

Stack
LayerServiceConfigLoad BalancerAWS ALBHTTP :80, public subnetsWeb TierEC2 + ASG + Launch Templatet2.micro, Apache HTTPD, min:2 max:4DatabaseRDS MySQL 8.0db.t3.micro, 20GB, Multi-AZ

Getting Started
Prerequisites

Terraform >= 1.0
AWS CLI configured with IAM permissions for EC2, RDS, VPC, and ELB

Deploy
bashgit clone https://github.com/Maema-Mazunda/Self-healing-Architecture-.git
cd Self-healing-Architecture-

terraform init
terraform plan
terraform apply
Destroy
bashterraform destroy