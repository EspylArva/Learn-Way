---
tags: [authentification_and_access_control]
aliases: [XSS]
---
# Cross Site Scripting
## Stored XSS
### Context
An attacker submits a blog post containing a malicious script on a vulnerable site. The script redirects users reading the blog post to a malicious site. The blog post is saved as-is on the web server: this is a Stored XSS attack
### Danger
Users could be redirected to malicious sites for [[Phishing]] attacks
### Counter Measures
- [[Trust no Input]]
- Validate all data that should be rendered on the application
- Encode user inputs
## Reflected XSS
### Context
An email with a malicious URL is sent to a user. The URL is built using a trusted domain and a parameter redirecting the user to the malicious website, making use of [[Unvalidated Redirects and Forwards]]. The user is caught in the Phishing attack and clicks on the link: this is a Reflected XSS attack
### Danger
Users could be redirected to malicious sites for [[Phishing]] attacks
### Counter Measures
- [[Trust no Input]]
- Validate all data that should be rendered on the application
- Encode user inputs
## DOM-based XSS
### Context
DOM-based XSS attack occur when an attacker submitting malicious code into the website to redirect users to a malicious website. The script usually is executed by the browser without user knowledge, as the script is executed in background when the page is loaded
### Danger
Users could be redirected to malicious sites for [[Phishing]] attacks
### Counter Measures
- Identify where and how data is appended to the DOM
- Identify the context in which the data is placed
- Sanitise the data