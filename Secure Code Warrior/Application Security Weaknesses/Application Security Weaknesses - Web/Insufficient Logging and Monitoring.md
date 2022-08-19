---
tags: [insecure_development_practices]
---
# Insufficient Logging and Monitoring
## Context
Inside an application, events are bound to happen. Insufficient Logging is the lack of recording of said events
## Danger
Attacks can happen without administrator being warned.
Important and malicious transactions or operations can happen without the system notifying the administrator, or without being logged into the system
## Example
Attacker has gained access to a list of user names. They try to brute-force passwords, knowing the system does not log or notify an administrator on successive fail attempts.
In another case, the attacker knows successive fail attempts are logged, but only on one account: attempts on different accounts from one IP address are not logged
## Counter Measures
- Insufficient Logging is not a vulnerability in itself, but allow other weaknesses to be exploited
- Apply [[Logging]] security rules
- Ensure all failures are properly logged with sufficient user context: user id, IP address, etc.
- Log entries should be held for a sufficient time to allow analysis
- Ensure the logs are generated in a format that can be consumed by a centralised log management solution
- Ensure high-value transactions have an audit trail with integrity and non-repudiation controls to prevent tampering or deletion, such as append-only database tables
- Implement effective monitoring and alerting system to respond accordingly to threats and suspicious activities