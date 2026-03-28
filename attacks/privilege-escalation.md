# Privilege Escalation Simulation

## Objective
Simulate an attacker gaining elevated permissions and verify that IAM changes are logged and detectable.

---

## Attack Description
An IAM role is modified to temporarily gain administrative privileges.

---

## Execution Steps

1. Navigated to:
   - AWS Console → IAM → Roles

2. Selected role:
   - `ec2-s3-readonly-role`

3. Attached policy:
   - `AdministratorAccess`

4. After validation, removed the policy

---

## Expected Behavior

- IAM modification events should be logged
- Events should be visible in CloudTrail
- Security team should be able to detect privilege escalation

---

## Observed Results

- CloudTrail logged:
  - `AttachRolePolicy`
  - `DetachRolePolicy`
- Events included:
  - User identity
  - Timestamp
  - Modified role

---

## Evidence

See:
![Privilege Escalation](screenshots/Adminaccess-IAM.png)
![Privilege Escalation](screenshots/Adminaccess-logs.png)


---

## Security Impact

Privilege escalation is one of the most critical attack vectors.

Improperly controlled IAM roles can allow attackers to:
- Gain full administrative access
- Modify infrastructure
- Access sensitive data

Monitoring IAM changes is essential for detecting this behavior.
