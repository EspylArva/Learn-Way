---
tags: [data_handling]
---
# Unvalidated Redirects and Forwards
## Context
This vulnerability refer to when trusted websites are tricked into redirecting users to malicious websites or into using forward values to access unauthorised pages.
This vulnerability can be exploited when user input is not validated and is used to construct URL destinations using [[Injection Flaws#HTTP Injection CRLF Injection|HTTP injection]]
## Danger
Exploiting unvalidated redirects and forwards vulnerabilities can lead to [[Phishing|phishing]] attacks, or allow attackers to access sensitive data
## Example
A victim receives an email from a trusted domain, but the website does not validate the appended parameterised URL. This parameter redirects the victim to a [[Phishing|phishing]] site
## Counter Measures
- Avoid redirects and forwards unless necessary
- Do not let user determine the destination of a redirection or forward: [[Trust no Input|do not trust user input]]
- If parameters must be used, validate the value and ensure it is authorised
- Use mapping values rather than actual URLs