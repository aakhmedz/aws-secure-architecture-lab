# Logging and Monitoring Security

## Objective
Ensure full visibility into AWS activity and enable detection of suspicious or unauthorized behavior.

---

## CloudTrail Logging

CloudTrail was enabled to capture:

- Console logins
- API activity
- IAM changes
- Resource modifications

---

## Log Storage

Logs are stored in:

- S3 bucket (long-term storage)
- CloudWatch log group (`secure-lab-log-group`)

---

## Monitoring with CloudWatch

CloudWatch was used to:

- Analyze logs in near real-time
- Create metric filters
- Generate alarms for critical events

---

## Detection Capabilities

The following behaviors were monitored:

- Failed login attempts
- Root account usage
- IAM policy changes
- Unauthorized API calls
- Resource manipulation events

---

## Alerting

CloudWatch alarms were configured to trigger when:

- Failed login attempts occur
- Suspicious activity is detected

---

## Validation

Monitoring was validated by:

- Simulating failed login attempts
- Modifying IAM roles
- Executing unauthorized API calls
- Stopping EC2 instances

All events were successfully captured and logged.

---

## Security Impact

- Provides visibility into all account activity
- Enables detection of suspicious behavior
- Supports auditing and incident investigation
- Helps identify misconfigurations and abuse

---

## Key Takeaways

- Logging is essential for detection and response
- CloudTrail provides full audit visibility
- CloudWatch enables actionable monitoring
- Detection must be validated through testing
