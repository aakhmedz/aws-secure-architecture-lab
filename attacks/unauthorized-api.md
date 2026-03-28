# Unauthorized API Call Simulation

## Objective
Simulate an attempt to access restricted AWS resources and verify enforcement of IAM least privilege.

---

## Attack Description
An EC2 instance attempts to execute an AWS CLI command without sufficient permissions.

---

## Execution Steps

1. SSH into public EC2 instance

2. Executed command:

aws iam list-users

## Evidence:
![Unauthorized API](../screenshots/SSH-restrict-command.png)
