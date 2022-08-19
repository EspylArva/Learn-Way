---
tags: [insecure_development_practices]
---
# Vulnerable Components
## Using Known Vulnerable Components
### Context
Developing an app, a framework and libraries are used. Some may be out of date and contain published and known vulnerabilities.
### Danger
Attackers can try analyse and determine the versions of libraries. Depending on the vulnerability, attackers may access or tamper with the service.
### Counter measures
- Check libraries against known vulnerabilities lists regularly
- Subscribe to cyber-security mailing list
- Implement security policies to define, evaluate, and ensure safety of components
- Be [[Secure by default]] and remove unused, insecure, or unsafe component functionalities
## Using Components From Untrusted Source
### Context
Open source components are easy to use, but may introduce weaknesses if the component has vulnerabilities, or even carry backdoors into the application
### Danger
Using modified open source component, attackers can access applications using their modified components.
### Example
An attacker uploads an open source customised text field on the internet. An application developer needs a text field, and uses the attacker's open source component to allow users to enter their login and password.
Using a backdoor they introduced in the component, the attacker may retrieve the users' sensitive information
### Counter measures
- Only use trusted sources
- Set up a patch management process to monitor components throughout the software lifecycle
- Use tools such as NVD or CVE to check for security alerts
- Make an inventory of client-side and server-side components
- Remove unused or unnecessary dependencies and features
- Check resources to verify that they are delivered without manipulation or tampering