# Failed Login Attack Simulation

## Objective
Simulate unauthorized access attempts by generating multiple failed login attempts and validating detection through CloudTrail and CloudWatch.

---

## Attack Description
An attacker attempts to gain access by repeatedly entering incorrect credentials through the AWS IAM login portal.

---

## Execution Steps

1. Logged out of AWS console
2. Navigated to IAM user login page
3. Attempted login using:
   - Valid username: `analyst-user`
   - Incorrect password
4. Repeated failed login attempts multiple times

---

## Expected Behavior

- Login attempts should fail
- Events should be logged in CloudTrail
- Detection rule should trigger CloudWatch alarm

---

## Observed Results

- CloudTrail recorded events:
  - `ConsoleLogin`
- Response field indicated:
  - `"ConsoleLogin": "Failure"`
- Logs were visible in CloudWatch log group
- Alarm triggered successfully

---

## Evidence

See:
![Failed Login](screenshots/Triggered-alert-failed-login.png)
![Failed Login](screenshots/Failed-login-attempts.png)


---

## Security Impact

Repeated failed login attempts may indicate:
- Brute force attack
- Credential stuffing attempt

Detection of these events is critical for early threat identification.
