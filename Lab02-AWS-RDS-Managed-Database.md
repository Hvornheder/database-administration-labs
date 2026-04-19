# Lab 02: AWS RDS — Managed Cloud Database Provisioning

## Overview

This lab focused on provisioning a fully managed MySQL database instance
using AWS Relational Database Service (RDS) and connecting to it remotely
using MySQL Workbench.

The objective was to understand the operational advantages of managed cloud
database services compared to the self-hosted approach in Lab 01, including
automated patching, built-in replication, simplified connectivity, and
elimination of OS-level administration overhead.

This exercise reinforced cloud database architecture concepts including
endpoint addressing, managed availability, and VPC-based access control.

---

## Environment

- AWS Management Console (AWS Academy Sandbox)
- AWS RDS — MySQL engine, Single DB instance
- VPC Security Groups (new group: "RDS")
- MySQL Workbench (local client)
- RDS Endpoint: `vornheder.crm66suuspoe.us-east-1.rds.amazonaws.com`
- Region: us-east-1 (N. Virginia)

---

## Methodology

1. Logged into AWS Academy and launched the Sandbox environment via the
   AWS Management Console.

2. Navigated to **Services → Database → RDS** and clicked **Create Database**.

3. Configured the RDS instance:
   - Engine: MySQL
   - Availability: Single DB instance
   - DB Instance Identifier: `vornheder`
   - Master Username: USF NetID
   - Authentication: Self-managed password
   - Instance class: Default (free tier eligible)
   - Storage: Default settings retained

4. Configured connectivity settings:
   - Public access: **Enabled** (to allow external MySQL Workbench connections)
   - VPC Security Group: Created new group named `RDS`

5. Under Additional Configuration:
   - Disabled automatic backups
   - Disabled encryption (development environment)

6. Clicked **Create Database** and monitored the dashboard until instance
   status changed from **Creating** to **Available**.

7. Retrieved the public endpoint address from the Connectivity & Security tab:
   `vornheder.crm66suuspoe.us-east-1.rds.amazonaws.com`

8. Opened MySQL Workbench locally and created a new connection:
   - Connection name: AWS RDS
   - Hostname: `vornheder.crm66suuspoe.us-east-1.rds.amazonaws.com`
   - Username: NetID credentials
   - Successfully established connection to the managed cloud database

9. Created the HR schema, selected it as the default schema, and executed
   the HR table creation script.

10. Verified successful table creation using:
```sql
    SHOW TABLES FROM hr;
```
    Confirmed tables: countries, departments, employees, job_history,
    jobs, locations, regions.

---

## Key Findings

### Managed vs. Self-Hosted Database
The most significant difference between Lab 01 (EC2) and Lab 02 (RDS) was
operational overhead. With RDS:
- No Windows Server to configure or maintain
- No MySQL installation required
- No OS-level patching or updates (Amazon manages this automatically)
- Amazon automatically maintains a replica for availability
- Connection is handled entirely through the endpoint address

This contrast illustrated why managed database services are preferred in
production environments where reliability and uptime are priorities.

### Endpoint-Based Connectivity
Unlike Lab 01 where the IP address of the EC2 instance was used,
RDS provides a persistent DNS endpoint address. This is significant
because IP addresses can change if an instance restarts, while the
endpoint remains stable — a critical distinction for production
application connectivity.

### VPC Security Group for Managed Services
Even managed RDS instances require explicit VPC security group configuration
to allow inbound connections. The new "RDS" security group served the same
function as the EC2 security group in Lab 01 — controlling which traffic
could reach the database on port 3306.

### Schema Verification
Executing `SHOW TABLES FROM hr` confirmed all 7 HR schema tables were
created successfully: countries, departments, employees, job_history,
jobs, locations, and regions.

---

## Skills Demonstrated

- AWS RDS instance provisioning and configuration
- VPC security group setup for managed database services
- Cloud endpoint addressing and DNS-based database connectivity
- MySQL Workbench remote connection to a managed cloud database
- Relational schema creation and SQL verification in a cloud environment
- Evaluation of managed vs. self-hosted cloud database tradeoffs

---

## Lessons Learned

- Managed database services dramatically reduce administrative overhead
  compared to self-hosted alternatives, but still require security
  group configuration and access management.
- Endpoint addresses are more reliable than IP addresses for persistent
  database connections in cloud environments.
- Disabling encryption and automatic backups is appropriate for short-lived
  development environments but would never be acceptable in production.
- Public accessibility must be explicitly enabled on RDS instances —
  the default is private access only, which is the more secure posture.

---

## Supporting Documentation

- Assignment completed November 22, 2024
- Course: ISM 4212 — Database Design & Administration, University of South Florida
- [Lab 02: AWS RDS — Managed Cloud Database Provisioning](https://github.com/user-attachments/files/26863027/ISM4212.Database.Design.and.Administration.-.AWS.RDS.-.Hunter.Vornheder.-.November.22nd.2024.pdf)
