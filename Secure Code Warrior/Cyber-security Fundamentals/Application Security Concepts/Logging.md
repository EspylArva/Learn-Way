# Logging
## Context
Application not logging enough, or logging too much
## Danger
When logging too much, confidential information could be leaked. When not logging enough, attacks could not be detected
## Counter measures
- Use framework to log
- Log errors and warnings
- Always log following information:
	- Login attempts (successful and failed)
	- Modification of data
	- Retrieval of data
- Do not log confidential information 
- Use 5W method: What happened, When, Where (host, network, interface), Who, Where did it come from
- Restrict access to logs