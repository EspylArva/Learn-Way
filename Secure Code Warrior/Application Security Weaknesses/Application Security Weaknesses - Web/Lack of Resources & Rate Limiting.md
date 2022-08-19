---
tags: [data_handling]
---
# Lack of Resources & Rate Limiting
## Context
In an application exposing APIs, those APIs have limited resources and can be called by multiple clients simultaneously. The risk of Lack of Resources & Rate Limiting occurs when the API is unable to limit the number of requests or deliverables handled in a given time period
## Danger
Service can be overloaded and become unresponsive, resulting in a [[Denial of Service|DoS]]
## Counter Measures
- Set following properties:
	- Execution timeout
	- Maximum allocable memory
	- Number of processes permitted within a defined timeframe
	- Maximum number of file descriptors
	- Maximum number of requests allowed per client
	- Number of records per page, which can be returned per request
- Display a notification of when limits are met, including a timer to reset