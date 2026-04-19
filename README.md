# USF Database Design & Administration — Lab Portfolio

Hands-on labs completed as part of ISM 4212: Database Design & Administration 
at the University of South Florida (Fall 2024).

Labs cover cloud infrastructure provisioning, relational database design, 
SQL transactions, distributed database concepts, and cloud-hosted database 
administration using AWS.

---

## Lab 01 – AWS EC2: Cloud Virtual Server Provisioning & MySQL Installation

### Overview
Provisioned a cloud-based Windows virtual server using AWS EC2 and configured 
it to host a publicly accessible MySQL database instance. This lab demonstrated 
the fundamentals of cloud infrastructure setup, security group configuration, 
and remote server administration.

### Environment
- AWS EC2 (t2.medium, Windows Server 2022 Base)
- AWS Management Console
- MySQL Workbench (local client)
- Remote Desktop Protocol (RDP)
- VPC Security Groups

### What I Did
1. Logged into AWS Academy and launched an EC2 instance running Windows 
   Server 2022 with a t2.medium instance type
2. Generated and stored a key pair (PEM file) for encrypted authentication
3. Configured VPC inbound security group rules to allow MySQL/Aurora 
   connections from any IPv4 source (port 3306)
4. Connected to the running Windows Server instance via Remote Desktop 
   Protocol using a decrypted administrator password
5. Installed MySQL Server on the cloud instance
6. Configured MySQL to accept remote connections
7. Connected MySQL Workbench from my local machine to the cloud-hosted 
   MySQL instance using the public IPv4 address: `54.221.52.178`
8. Loaded and executed the HR schema script to create and populate 
   relational tables

### Key Concepts Demonstrated
- Cloud virtual machine provisioning (EC2 instance launch and configuration)
- VPC security group management and inbound firewall rule configuration
- Remote server administration via RDP
- Public/private IP addressing in cloud environments
- Cloud-hosted relational database setup and remote client connectivity
- Security tradeoffs in public cloud database exposure

### Skills Applied
AWS EC2, Windows Server 2022, VPC Security Groups, RDP, MySQL, 
MySQL Workbench, Cloud Infrastructure, Remote Administration

---

## Lab 02 – AWS RDS: Managed Cloud Database Provisioning

### Overview
Provisioned a managed MySQL database instance using AWS Relational Database 
Service (RDS). This lab demonstrated the operational advantages of managed 
cloud database services compared to self-hosted virtual server databases, 
including automated patching, built-in replication, and simplified connectivity.

### Environment
- AWS RDS (MySQL engine, Single DB instance)
- AWS Management Console
- MySQL Workbench (local client)
- VPC Security Groups

### What I Did
1. Created an AWS RDS MySQL instance via the AWS Management Console
2. Configured instance settings: Single DB instance, MySQL engine, 
   t2.micro class, public accessibility enabled
3. Created a new VPC security group (named "RDS") to manage inbound 
   access rules for the managed database
4. Waited for instance status to transition from "Creating" to "Available"
5. Retrieved the public endpoint address: 
   `vornheder.crm66suuspoe.us-east-1.rds.amazonaws.com`
6. Configured a MySQL Workbench connection using the RDS endpoint, 
   master username, and credentials
7. Successfully connected to the managed cloud database
8. Loaded the HR schema and verified table creation via `SHOW TABLES FROM hr`

### Key Concepts Demonstrated
- Managed database services vs. self-hosted alternatives
- RDS instance configuration and availability zone deployment
- Cloud endpoint addressing and remote database connectivity
- VPC security group configuration for managed services
- Operational benefits of managed services: automated updates, 
  built-in replication, no OS management overhead

### Skills Applied
AWS RDS, MySQL, MySQL Workbench, VPC Security Groups, Cloud Database 
Administration, Endpoint Configuration

---

## Conceptual Foundation — Distributed & Cloud Databases (Module 13)

These labs were completed in the context of Module 13, which covered:

- Database transactions (BEGIN, COMMIT, ROLLBACK) and data integrity
- Concurrency strategies and locking mechanisms
- Centralized vs. distributed database architectures
- Horizontal partitioning (sharding) and replication strategies
- Cloud database implementation from design to deployment

The AWS labs applied these concepts in a real cloud environment, reinforcing 
the distinction between centralized, distributed, and managed cloud database 
models.

---

## Course Context
**Course:** ISM 4212 — Database Design & Administration  
**Institution:** University of South Florida, Muma College of Business  
**Semester:** Fall 2024  
**Topics Covered Across Course:** Entity-relationship modeling, SQL (DDL/DML), 
normalization, indexing, views, execution plans, transactions, concurrency, 
distributed databases, cloud provisioning, database security and administration
