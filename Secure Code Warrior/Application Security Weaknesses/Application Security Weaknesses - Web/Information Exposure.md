# Information Exposure
## Security Misconfiguration
### Context
Applications usually use configuration files to change settings such as IP addresses, ports, etc.
Security Misconfiguration vulnerability occurs when attackers are able to retrieve the configuration files
### Danger
Sensitive data could be retrieved by the attacker. These data mostly are application scoped, but they could grant access to the server or database, and therefore lead to more data leakage
### Counter Measures
- Place configuration files outside the web root directory
- Apply [[Least privilege]]: configure system read and write restriction
- Disable directory listing
- [[Fail Securely|Display generic error message]]
- Hide sensitive information from [[Logging|log files]]
## Error Details
### Context
When navigating an application, errors could be risen. Error details vulnerability occurs to when too much information is displayed to the user when the error occurs.
### Danger
Attackers could intentionally trigger errors to gain knowledge of the application's [[Business Logic]] or weaknesses
### Counter Measures
- Implement good [[Logging]] practices
- [[Fail Securely|Display generic error message]]
## Debug Information
### Context
When navigating an application, errors could could be risen. Debug information vulnerability occurs to when too much information is logged in log files when the error occurs.
### Danger
If the attacker gains access to log files, they could get access to sensitive data that has been logged abusively 
### Counter Measures
- Implement good [[Logging]] practices
- [[Fail Securely|Display generic error message]]
- Place configuration files outside the web root directory
- Apply [[Least privilege]]: configure system read and write restriction
- Disable directory listing
## Sensitive Data Exposure
### Context
Sensitive Data Exposure happens when attackers get access to sensitive data. This can range from identity information (date of birth, name, health insurance, etc.) to consumer profile (buying habits, credit card information, bank information, etc.)

The following data types are considered sensitive:
- Personal Identifiable Information (PII)
- Payment Card Industry data (PCI data)
- Any data subject to privacy law, such as [[GDPR]]
### Danger
Sensitive data could be leaked, sold, or used to impersonate someone else
### Counter Measures
- Identify where and how data is used and combined
- Prevent [[Least privilege|sending unnecessary data]] to users
- Avoid [[Data Protection|collecting unnecessary data]] from users
- Secure data through encryption