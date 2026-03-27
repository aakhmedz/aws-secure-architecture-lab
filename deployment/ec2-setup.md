# EC2 Setup

## Objective
Deploy and configure EC2 instances to demonstrate secure access patterns between public and private environments.

---

## Public EC2 Instance

### Configuration
- Name: `public-ec2`
- Subnet: `public-subnet`
- Public IP: Enabled
- OS: Amazon Linux

### Security Group (`public-sg`)
- SSH (22): Allowed from user IP only
- HTTP (80): Allowed from internet (if used)

---

## Private EC2 Instance

### Configuration
- Name: `private-ec2`
- Subnet: `private-subnet`
- Public IP: Disabled
- OS: Amazon Linux

### Security Group (`private-sg`)
- SSH (22): Allowed only from `public-sg`

---

## Access Design

- Public EC2 acts as controlled access point (bastion-style host)
- Private EC2 is only accessible from within the VPC
- No direct internet access to private instance

---

## Validation

- Successfully connected to public EC2 via SSH
- Confirmed private EC2 has no public IP
- Verified private instance cannot be accessed directly from internet

---

## Security Impact

- Restricts administrative access paths
- Prevents exposure of internal systems
- Enforces controlled entry point into environment
