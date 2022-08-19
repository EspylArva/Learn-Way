# Robust Error Checking
## Context
Error badly handled in the code
## Danger
Attackers can see what framework, language is used and where the code is broken
## Counter measures
- Display generic error messages
- Close application securely
- Do not display private information: internal IP, stack traces, library information...
- Test app and services to make sure it [[Fail Securely|fails securely]]