# CloudWatch Monitoring Setup

## Objective
Enable monitoring and alerting based on CloudTrail logs to detect suspicious or high-risk activity.

---

## Log Group

CloudTrail logs were configured to stream into:

- Log group: `secure-lab-log-group`

This enables real-time log analysis and metric creation.

---

## Viewing Logs

Logs can be accessed via:

AWS Console → CloudWatch → Logs → Log groups → `secure-lab-log-group`

Each log stream contains JSON-formatted events such as:
- Console logins
- API calls
- IAM changes

---

## Live Monitoring

CloudWatch allows near real-time visibility using:
- Log stream refresh
- Live tail (when available)

---

## Metric Filters

Metric filters were created to detect specific events from CloudTrail logs.

Example use cases:
- Failed authentication attempts
- IAM changes
- Root account usage

---

## Alarm Configuration

Alarms were created using custom metrics derived from log filters.

### Example Alarm

- Name: `failed-login-alarm`
- Metric: FailedConsoleLogins
- Condition: Greater than 0 within 5 minutes

---

## Validation

To validate monitoring:

- Generated failed login attempts
- Confirmed logs appeared in CloudWatch
- Verified metric filter captured events
- Confirmed alarm triggered correctly

---

## Security Impact

CloudWatch enables:
- Real-time monitoring of AWS activity
- Detection of suspicious behavior
- Alerting on critical events

This provides a detection layer on top of CloudTrail logging.
