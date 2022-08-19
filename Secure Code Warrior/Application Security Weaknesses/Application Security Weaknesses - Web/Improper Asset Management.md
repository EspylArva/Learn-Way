---
tags: [insecure_development_practices]
---
# Improper Asset Management
## Context
Improper Asset Management refer to vulnerability where an attacker exploit outdated, incomplete or undocumented API behaviour
## Danger
Attacker can bypass the API routes and access services not designed to be public
## Example
A code compilation service provides an rate-limited API to ensure each user can access the service, accordingly to their access tier.
An attacker has access to the address used for testing new features, and uses it to run their task freely, without using the production server and without subscribing to an adequate access tier
## Counter Measures
- Ensure production and development or staging environments are made separate
- Implement [[Defense in depth|security controls such as firewalls]] and [[Open Design|change default ports]], to prevent unintended access to weaken environments
- Document endpoints and error states that exist within the API
- Be [[Secure by default]]: disable unused API endpoints, or validate them using safety checks