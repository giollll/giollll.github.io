---
layout: default
title: "Web Security Academy Notes"
---

# 🌐 Web Security Academy Notes

This page contains an outline of my notes on various topics from the Web Security Academy.
The actual notes/content I keep in remnote.com.

# Server-side Vulnerabilities

## Path Traversal
- What is path traversal?  
- Reading arbitrary files via path traversal

## Access Control
- What is access control?
- Vertical privilege escalation
- Unprotected functionality - Continued
- Parameter-based access control methods
- Horizontal privilege escalation
- Horizontal to vertical privilege escalation
- User ID controlled by request parameter with password disclosure

## Authentication Vulnerabilities
- What is the difference between authentication and authorization?
- Brute-force attacks
- Brute-forcing passwords
- Bypassing two-factor authentication

## SSRF (Server-Side Request Forgery)
- What is SSRF?
- SSRF attacks against the server
- SSRF attacks against the server - Continued
- SSRF attacks against other back-end systems

## File Upload Vulnerabilities
- What are file upload vulnerabilities?
- How do file upload vulnerabilities arise?
- Exploiting unrestricted file uploads to deploy a web shell
- Exploiting flawed validation of file uploads
- Flawed file type validation
- Flawed file type validation - Continued
- Flawed file type validation - Continued

## OS Command Injection
- What is OS command injection?
- Useful commands
- Injecting OS commands
- Injecting OS commands - Continued

## SQL Injection (SQLi)
- What is SQL injection (SQLi)?
- How to detect SQL injection vulnerabilities
- Retrieving hidden data
- Retrieving hidden data - Continued
- Subverting application logic

### SQL Injection Union Attacks
- SQL injection UNION attacks
- SQL injection UNION attacks - Continued
- Determining the number of columns required
- Determining the number of columns required - Continued
- Database-specific syntax
- Finding columns with a useful data type

---

# AWS (Amazon Web Services)

## Why AWS?
- Cloud Trends
- Core Principles

## Core Principles
### 6 Pillars of a Well-Architected Framework
- Operational excellence (corporate propaganda)
- Security
- Reliability
- Performance efficiency
- Cost optimization
- Sustainability

## Architecture
- Availability Zones/Regions
- AWS Organizations
- Virtual Private Cloud configuration
    - Network segmentation/routing, NACLs, security groups

## ARN (Amazon Resource Name)
- What is ARN?
- arn:partition:service:region:account-id:resource-id
- arn:partition:service:region:account-id:resource-type/resource-id
- arn:partition:service:region:account-id:resource-type:resource-id
    - Example: `arn:aws:iam:123456789012:user/johndoe`
    - Example: `arn:sns:us-east-1:123456789012:example-sns-topic-name`
    - Example: `arn:ec2:us-east-1:123456789012:vpc/vpc-0e9801d129....`

## Core Services
- Elastic Cloud Computer (EC2)
- Simple Storage Service (S3)
- Virtual Private Cloud (VPC)
- Lambda
- Key Management Service (KMS)

## Core Security Services
- GuardDuty
- Cloudwatch
- Cloudtrail

### Details
- Things to be Mindful of

---

# Cloud Service Models
- **Infrastructure as a Service (IaaS)**
- **Platform as a Service (PaaS)**
- **Software as a Service (SaaS)**
    - Physical infrastructure, virtualized environments, and underlying software managed by AWS
        - Example: SES
