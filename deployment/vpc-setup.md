# VPC Setup

## Objective
Create a secure network architecture using a custom VPC with segmented public and private subnets.

---

## VPC Configuration

- VPC Name: `secure-vpc`
- CIDR Block: `10.0.0.0/16`

This provides a private address space for all resources in the environment.

---

## Subnet Configuration

### Public Subnet
- Name: `public-subnet`
- CIDR: `10.0.1.0/24`
- Purpose: Host internet-facing EC2 instance

### Private Subnet
- Name: `private-subnet`
- CIDR: `10.0.2.0/24`
- Purpose: Host internal EC2 instance

---

## Internet Gateway

- Created and attached Internet Gateway to VPC
- Enables inbound and outbound internet access for public subnet

---

## NAT Gateway

- Created NAT Gateway in public subnet
- Associated Elastic IP
- Allows private subnet to access internet without being exposed

---

## Route Tables

### Public Route Table
- `10.0.0.0/16 → local`
- `0.0.0.0/0 → Internet Gateway`
- Associated with public subnet

### Private Route Table
- `10.0.0.0/16 → local`
- `0.0.0.0/0 → NAT Gateway`
- Associated with private subnet

---

## Validation

- Public subnet resources had internet access
- Private subnet resources had outbound access only
- Private resources were not directly accessible from internet

---

## Security Impact

- Segmented network reduces attack surface
- Private subnet protects internal resources
- NAT Gateway prevents inbound exposure while allowing updates
