
# 3-Tier Web Application Architecture on AWS (Terraform)

This project deploys a highly available 3-tier web application architecture on AWS using Terraform.

The infrastructure is provisioned using Terraform modules to ensure reusability and clean separation of concerns.

## Application Overview

This project implements a highly available, scalable, and secure 3-tier web application architecture on AWS using Terraform.

The application is divided into three logical tiers:

- **Presentation Tier**: An internet-facing Application Load Balancer distributes incoming traffic across EC2 instances deployed in multiple Availability Zones.
- **Application Tier**: Private EC2 instances handle application logic and process requests forwarded from the load balancer.
- **Data Tier**: An Amazon RDS database deployed in private subnets provides persistent and secure data storage.

The infrastructure is fully provisioned using Terraform modules, enabling repeatable deployments, clean separation of concerns, and adherence to Infrastructure as Code (IaC) best practices.
