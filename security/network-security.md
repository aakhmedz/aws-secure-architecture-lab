# Network Security

## Objective
Design and enforce secure network boundaries to protect internal resources and limit exposure to external threats.

---

## Architecture Overview

The environment uses a segmented network design within a custom VPC:

- Public subnet for internet-facing resources
- Private subnet for internal systems
- Internet Gateway for controlled inbound access
- NAT Gateway for controlled outbound traffic

---

## Public Subnet Security

The public subnet hosts the public EC2 instance, which acts as a controlled access point.

### Controls Implemented
- Assigned public IP only to required instance
- Restricted SSH access to a specific IP address
- Limited exposed ports (no unnecessary services)

---

## Private Subnet Security

The private subnet hosts the backend EC2 instance.

### Controls Implemented
- No public IP assigned
- No direct internet access
- Outbound traffic only through NAT Gateway
- SSH access restricted via security group reference

---

## Security Groups

### Public Security Group (`public-sg`)
- SSH (port 22) allowed only from user IP
- HTTP (port 80) allowed as required

### Private Security Group (`private-sg`)
- SSH (port 22) allowed only from `public-sg`

---

## Routing Controls

### Public Route Table
- Routes traffic to Internet Gateway

### Private Route Table
- Routes outbound traffic to NAT Gateway
- Prevents direct inbound connections

---

## Security Impact

This design ensures:

- Internal systems are not exposed to the internet
- Administrative access is controlled and restricted
- Lateral movement is limited through segmentation
- External attack surface is minimized

---

## Key Takeaways

- Network segmentation is a foundational security control
- Private resources should never be directly exposed
- Security groups provide fine-grained access control
- NAT Gateway enables safe outbound communication without exposing internal systems
