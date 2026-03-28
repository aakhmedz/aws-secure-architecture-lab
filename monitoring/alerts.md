# Detection Rules

## Objective
Define and validate detection logic for suspicious or high-risk AWS activity using CloudTrail and CloudWatch.

---

## Detection Rule 1: Failed Console Login

### Description
Detects repeated failed login attempts, which may indicate brute force or unauthorized access attempts.

### Filter Pattern

" ($.eventName = "ConsoleLogin") && ($.responseElements.ConsoleLogin = "Failure") "

### Metric
- Namespace: SecurityMetrics
- Metric Name: FailedConsoleLogins

### Alarm Condition
- Trigger if value > 0 within 5 minutes

---

## Detection Rule 2: Root Account Usage

### Description
Detects usage of the root account, which is considered high-risk and should be avoided.

### Detection Method
CloudWatch built-in metric:
- RootAccountUsage

---

## Detection Rule 3: IAM Policy Changes

### Description
Detects changes to IAM roles and policies, which could indicate privilege escalation.

### Events Monitored
- AttachRolePolicy
- DetachRolePolicy
- PutRolePolicy

---

## Detection Rule 4: Unauthorized API Calls

### Description
Detects API calls that are denied due to insufficient permissions.

### Example
- aws iam list-users (denied)

### Detection Method
- CloudTrail logs showing access denied events

---

## Detection Rule 5: Resource Manipulation

### Description
Detects changes to AWS infrastructure, such as stopping or modifying instances.

### Events Monitored
- StopInstances
- StartInstances
- TerminateInstances

---

## Validation Summary

Each detection rule was validated by performing controlled test scenarios:

- Failed login attempts triggered detection
- IAM changes were logged and visible
- Unauthorized API calls were captured
- Resource manipulation events were logged

---

## Security Value

These detection rules demonstrate:

- Ability to identify suspicious behavior
- Visibility into account activity
- Detection of privilege escalation attempts
- Monitoring of infrastructure changes

This reflects real-world cloud detection engineering practices.
