# Lab 01: AWS EC2 — Cloud Virtual Server Provisioning & MySQL Installation

## Overview

This lab focused on provisioning a cloud-based virtual server using AWS EC2
and configuring it to host a publicly accessible MySQL database instance.

The objective was to understand how cloud infrastructure is provisioned from
scratch, how security is configured to allow controlled external access, and
how a relational database is installed and administered on a remote cloud server.

This exercise reinforced the distinction between self-hosted cloud databases
and managed database services, and demonstrated the real operational overhead
involved in maintaining a self-hosted approach.

---

## Environment

- AWS Management Console (AWS Academy Sandbox)
- AWS EC2 — t2.medium instance, Windows Server 2022 Base (AMI)
- VPC Security Groups
- Key Pair Authentication (PEM file)
- Remote Desktop Protocol (RDP)
- MySQL Server (installed on cloud instance)
- MySQL Workbench (local client)
- Public IPv4 Address: `54.221.52.178`

---

## Methodology

1. Logged into AWS Academy and launched the Sandbox environment via the
   AWS Management Console.

2. Navigated to EC2 and clicked **Launch Instance** to begin server configuration:
   - Instance name: `ISM4212`
   - AMI selected: Windows Server 2022 Base
   - Instance type: `t2.medium` (2 vCPU, 4GB RAM)
   - Generated a new key pair named `ISM4212` (downloaded as `.pem` file)

3. Configured network settings and launched the instance. Monitored status
   checks until the instance passed **2/2 checks**, confirming it was ready.

4. Configured inbound security group rules to allow MySQL connections:
   - Navigated to the Security tab → Security Group → Inbound Rules
   - Added rule: Type = MySQL/Aurora, Source = Anywhere-IPv4 (port 3306)

5. Connected to the running Windows Server instance via RDP:
   - Downloaded the Remote Desktop file from the Connect panel
   - Decrypted the administrator password using the saved PEM key pair
   - Authenticated into the cloud server via Remote Desktop

6. Installed MySQL Server on the Windows Server instance.

7. Configured MySQL to accept remote connections from outside the instance.

8. From a local machine, opened MySQL Workbench and created a new connection:
   - Hostname: `54.221.52.178` (public IPv4 of the EC2 instance)
   - Successfully connected to the cloud-hosted MySQL database

9. Loaded and executed the HR schema script to create and populate
   relational tables within the cloud database.

---

## Key Concepts Demonstrated

### Cloud Virtual Machine Provisioning
Launching an EC2 instance involves selecting compute resources (instance type),
an operating system image (AMI), and configuring storage and network settings.
The t2.medium instance type provided sufficient resources for a development
MySQL server.

### VPC Security Groups and Firewall Rules
By default, AWS blocks all inbound traffic to instances. Inbound rules must
be explicitly configured to allow specific protocols and ports. Opening
MySQL/Aurora on port 3306 to Anywhere-IPv4 allowed external client connections
but represented a security tradeoff — in a production environment this would
be restricted to specific IP ranges.

### Key Pair Authentication
AWS uses asymmetric key pairs to secure instance access. The public key is
stored by AWS; the private key (PEM file) is held by the user. The private
key was required to decrypt the auto-generated administrator password before
RDP access was possible.

### Remote Server Administration via RDP
Once connected, the cloud server was administered exactly like a local Windows
Server — no difference from the user's perspective. This demonstrated how
cloud infrastructure abstracts physical hardware while maintaining familiar
operating system interfaces.

### Self-Hosted vs. Managed Database Tradeoffs
This lab illustrated the operational overhead of self-hosting a database
in the cloud: OS updates, MySQL installation, security configuration, and
firewall management all require manual attention. Lab 02 (AWS RDS) contrasts
this with a fully managed alternative.

---

## Skills Demonstrated

- AWS EC2 instance provisioning and configuration
- VPC security group and inbound firewall rule management
- Key pair generation and administrator password decryption
- Remote Desktop Protocol (RDP) server administration
- MySQL Server installation and remote access configuration
- MySQL Workbench remote connection setup
- Relational schema loading and SQL execution in a cloud environment

---

## Lessons Learned

- Cloud servers require explicit security group configuration before any
  external connections are possible — security is off by default.
- Key pair management is critical; losing the PEM file means losing
  administrator access to the instance.
- Self-hosted cloud databases carry the same maintenance burden as
  on-premises servers — OS patching, software updates, and security
  hardening remain the administrator's responsibility.
- Opening database ports to Anywhere-IPv4 is convenient for development
  but represents a significant attack surface in production environments.

---

## Supporting Documentation

- Assignment completed November 21, 2024
- Course: ISM 4212 — Database Design & Administration, University of South Florida
- [Lab 01: AWS EC2 — Cloud Virtual Server Provisioning & MySQL Installation](https://github.com/user-attachments/files/26863013/ISM4212.Database.Design.and.Administration.-.AWS1.-.Hunter.Vornheder.-.November.21st.2024.pdf)
