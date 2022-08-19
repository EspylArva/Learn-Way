---
tags: [data_handling]
aliases: [XXE Injection]
---
# XML eXternal Entity Injection
## Context
External input is parsed by a weakly secured XML parser. Attackers can intercept the XML request 
## Danger
- Internal port scanning can be executed by attackers
- Confidential files could be extracted
- [[Denial of Service|DoS]] can hit the application
## Counter measures
- Application-wide filter or sanitization of user input: apply [[Trust no Input]] principle
- Use GET and POST parameters
- Use cookies and HTTP headers
- Whitelist input validation
- XML parsers should disable support for external entities or DTDs