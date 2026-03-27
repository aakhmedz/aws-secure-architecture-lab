# CloudTrail Setup

## Objective
Enable centralized logging of all AWS account activity, including API calls, authentication attempts, IAM changes, and resource modifications.

---

## Configuration Steps

1. Navigated to:
   - AWS Console → CloudTrail → Trails → Create trail

2. Created trail:
   - Name: `secure-lab-trail`

3. Storage configuration:
   - Created new S3 bucket for log storage

4. Event settings:
   - Management events:
     - Read events: Enabled
     - Write events: Enabled
   - Data events: Not configured (not required for this lab)

5. Multi-region trail:
   - Enabled to capture activity across all AWS regions

---

## CloudWatch Integration

- Enabled CloudWatch Logs integration
- Created log group:
  - `secure-lab-log-group`

This allows real-time monitoring and alerting based on CloudTrail logs.

---

## Validation

To confirm CloudTrail was functioning:

- Logged out and logged back into AWS
- Performed IAM and EC2 actions
- Verified events appeared in:
  - CloudTrail → Event History
  - CloudWatch → Log groups → `secure-lab-log-group`

---

## Key Events Captured

- ConsoleLogin
- StartInstances
- StopInstances
- AttachRolePolicy
- DetachRolePolicy
- API access attempts

---

## Security Impact

CloudTrail provides:
- Full audit visibility into AWS account activity
- Ability to trace actions back to specific users or roles
- Critical foundation for detection and incident response
