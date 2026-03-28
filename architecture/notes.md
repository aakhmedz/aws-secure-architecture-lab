# Architecture Notes

## Objective
Design a secure AWS environment that separates public-facing and internal resources, limits access through least privilege principles, and supports centralized logging and detection.

---

## High-Level Architecture

The environment was built inside a custom VPC and split into two security zones:

- Public subnet
- Private subnet

The public subnet contains a public EC2 instance used as a controlled access point.  
The private subnet contains an internal EC2 instance that is not directly exposed to the internet.

An Internet Gateway provides public connectivity where required, while a NAT Gateway allows the private subnet to initiate outbound traffic without accepting direct inbound connections.

---

## Core Components

### 1. Virtual Private Cloud (VPC)
- Name: `secure-vpc`
- CIDR Block: `10.0.0.0/16`

The VPC provides isolated networking for all resources in the lab and allows full control over routing, segmentation, and security boundaries.

---

### 2. Public Subnet
- Name: `public-subnet`
- CIDR Block: `10.0.1.0/24`

Purpose:
- Hosts the public EC2 instance
- Provides controlled external access into the environment

Security rationale:
- Only resources that require internet-facing access should be placed in a public subnet
- SSH access is restricted to a specific source IP rather than being open broadly

---

### 3. Private Subnet
- Name: `private-subnet`
- CIDR Block: `10.0.2.0/24`

Purpose:
- Hosts the private EC2 instance
- Keeps internal systems isolated from direct internet exposure

Security rationale:
- Sensitive or backend systems should remain private whenever possible
- The private EC2 instance has no public IP assigned

---

### 4. Internet Gateway
Purpose:
- Provides internet connectivity to resources in the public subnet

Security rationale:
- Required for the public EC2 instance to be reachable externally
- Public exposure is limited to only the systems that require it

---

### 5. NAT Gateway
Purpose:
- Allows the private subnet to make outbound connections to the internet

Security rationale:
- Lets internal systems retrieve updates or access AWS services without exposing them to inbound internet traffic
- Preserves isolation while maintaining limited operational functionality

---

### 6. Public EC2 Instance
Purpose:
- Serves as a bastion-style administrative entry point
- Used to demonstrate secure access design and controlled connectivity

Security rationale:
- Centralizes administrative access
- Reduces the need to directly expose internal systems

---

### 7. Private EC2 Instance
Purpose:
- Represents an internal backend system

Security rationale:
- Deployed without a public IP
- Protected by subnet placement, routing controls, and security groups

---

### 8. IAM User and Role Design
Purpose:
- Enforce least privilege for both human and system access

Components:
- `analyst-user` with restricted permissions
- `ec2-s3-readonly-role` for role-based AWS access from EC2

Security rationale:
- Prevents unnecessary privilege
- Avoids hardcoded credentials
- Reflects real-world identity and access management design

---

### 9. Logging and Monitoring Components
Purpose:
- Provide visibility into user activity, API calls, IAM changes, and infrastructure actions

Components:
- AWS CloudTrail
- AWS CloudWatch
- S3 for log storage

Security rationale:
- Logging is required for accountability, detection, and incident response
- Security controls should be observable and testable

---

## Traffic Flow

### Inbound Administrative Access
- User connects from trusted IP to public EC2 over SSH
- Public EC2 acts as the controlled access point into the environment

### Internal System Isolation
- Private EC2 does not accept direct internet traffic
- Access to the private subnet is restricted by design

### Outbound Private Subnet Traffic
- Private EC2 reaches external services through NAT Gateway
- No direct inbound path from the internet exists

### Logging Flow
- AWS account and infrastructure events are captured by CloudTrail
- Logs are stored in S3 and streamed into CloudWatch for monitoring and detection

---

## Security Design Principles Applied

### Network Segmentation
Public-facing and internal systems were separated into different subnets to reduce exposure and limit attack paths.

### Least Privilege
IAM users and roles were configured with only the permissions required for their intended purpose.

### Controlled Administrative Access
Administrative access was limited to a known source IP and restricted through security groups.

### Defense in Depth
The design uses multiple layers of protection:
- Subnet isolation
- Route table controls
- Security groups
- IAM restrictions
- Logging and detection

### Visibility and Auditability
CloudTrail and CloudWatch were used to ensure that important actions could be monitored and investigated.

---

## Why This Architecture Matters

This architecture reflects practical cloud security engineering concepts rather than basic infrastructure deployment. It was designed to answer key security questions:

- How can public and private resources be separated safely?
- How can internal systems retain outbound access without becoming publicly reachable?
- How can access be controlled through identity and security groups?
- How can suspicious or high-risk actions be logged and detected?

The final design demonstrates a secure baseline AWS environment that supports both protection and observability.

---

## Diagram Reference

See:
![Architecture Diagram](../screenshots/architecture.png)

This diagram visually represents the relationship between the VPC, subnets, EC2 instances and gateways.
