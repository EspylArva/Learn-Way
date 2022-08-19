# Fail Securely
## Context
Error badly handled when user uses service
## Danger
Can lead to loss of data, shut down of service
## Counter measures
- Service should only be granted on [[Least privilege|explicit permission]]
- Display generic error messages
- Roll back when displaying error to have a "safe" error environment
- Make sure [[Robust Error Checking]] is implemented