Client → IGW → ALB → EC2 → RDS → EC2 → ALB → IGW → client


## 1. VPC and network

VPC: 10.0.0.0/16

Subnets:
- Public Subnet 1 (10.0.1.0/24) – with access to the internet, deployed ALB with ASG
- Public Subnet 2 (10.0.3.0/24) - with access to the internet, deployed ALB with ASG

- Private Subnet 1 (10.0.2.0/24) – primary RDS
- Private Subnet 2 (10.0.4.0/24) – standby RDS


Security Groups: 
Public Subnets: 
	- allow inbound/outbound HTTP/HTTPS traffic from/to internet - ALB/EC2
	- allow outbound traffic from EC2 to database
Private Subnets:
	- allow inbound/outbound MySQL traffic from/to EC2 only 
 

## 2. Database

Amazon RDS MySQL Multi-AZ - located in private subnets:
- Primary: Private Subnet 1
- Standby: Private Subnet 2


## 3. Application and compute

- EC2 deployed in Public Subnets

- ELB with ALB for HTTP/HTTPS traffic
- ASG for leverage high traffic


## 4. Storage

S3 Bucket to store backup and static files


## 5. Security

- IAM and Roles to control access
- Security Group - for private subnets with no permission to access from internet
- Multi-AZ RDS
