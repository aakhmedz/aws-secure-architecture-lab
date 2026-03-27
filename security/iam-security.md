# IAM Security

## Objective
Implement least privilege access and role-based authentication to control access to AWS resources.

---

## IAM User Configuration

### User: `analyst-user`

A restricted IAM user was created to simulate a standard user account.

### Permissions
- `AmazonS3ReadOnlyAccess`

---

## Least Privilege Enforcement

The user was intentionally limited to:

- Viewing S3 resources
- No ability to modify infrastructure
- No access to IAM management
- No access to EC2 configuration

---

## Validation

Testing confirmed:

- Allowed actions succeeded
- Unauthorized actions failed with access denied errors

---

## IAM Role for EC2

### Role: `ec2-s3-readonly-role`

An IAM role was created and attached to the EC2 instance.

### Permissions
- `AmazonS3ReadOnlyAccess`

---

## Benefits of IAM Roles

- No hardcoded credentials required
- Secure, temporary access via AWS identity system
- Reduced risk of credential exposure

---

## Privilege Escalation Risk

A simulation demonstrated that attaching excessive permissions (e.g., `AdministratorAccess`) significantly increases risk.

### Observations
- Privilege changes were logged
- Elevated access allowed broader system control

---

## Security Impact

- Least privilege reduces attack surface
- Role-based access eliminates need for static keys
- Monitoring IAM changes is critical for detecting escalation

---

## Key Takeaways

- Over-permissioning is a major security risk
- IAM roles are safer than access keys
- Access should always be minimized and validated
- IAM changes must be monitored continuously
