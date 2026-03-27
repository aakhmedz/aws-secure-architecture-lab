# IAM Setup

## Objective
Implement secure identity and access management using least privilege principles and role-based access.

---

## IAM User Creation

### User: `analyst-user`

- Created IAM user with console access
- Assigned limited permissions:
  - `AmazonS3ReadOnlyAccess`

---

## User Validation

Tested user access and confirmed:

- Can view allowed resources
- Cannot modify infrastructure
- Cannot access IAM controls
- Cannot perform administrative actions

---

## IAM Role Creation

### Role: `ec2-s3-readonly-role`

- Created role for EC2 service
- Attached policy:
  - `AmazonS3ReadOnlyAccess`

---

## Role Attachment

- Attached role to public EC2 instance
- Enabled EC2 to access AWS resources securely without storing credentials

---

## Validation

From EC2 instance:

- Allowed actions (S3 access) succeeded
- Unauthorized actions were denied

---

## Security Impact

- Eliminates need for static credentials
- Enforces least privilege access
- Reduces risk of credential compromise
- Enables secure service-to-service communication
