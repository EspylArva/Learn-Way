---
tags: [authentification_and_access_control]
aliases: [SSRF]
---
# Server-Side Request Forgery
## Context
Application does not restrict the location and type of resources it can access
## Danger
The server can be made to perform a request from the hacker: attackers can scan for open ports, retrieve files or access internal services or data
## Counter measures
- Restrict requests made by the server to allow-listed locations if possible
- Check that the requested file type matches the expectation
- Use [[Robust Error Checking]] and [[Fail Securely|fail securely]], displaying generic errors
- [[Trust no Input]]: Restrict requests to approved URL schemas