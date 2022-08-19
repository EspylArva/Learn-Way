---
tags: [sensitive_data_protection]
---
# Sensitive Data Storage
## Password exposure
### Context
Sensitive data such as logins and passwords could be exposed to attackers
### Danger
Attacker can access a user profile and impersonate a user
### Example
An application contains sensitive information. If the attacker can retrieve the database containing the passwords, he will be able to access the users' profiles.
If the password are not salted or weakly encrypted, using a [[rainbow table]] will allow him to crack easily the passwords.
### Counter measures
- Use [[Salt & Pepper#Salt|salt]] and [[Salt & Pepper#Pepper|pepper]] to hash data
- Encrypt data with secure protocols such as TLS
- Store data only when necessary
- Use strong hashing or encryption where applicable
- For data that does not need to be hashed, use symmetric encryption
- Disable caching of sensitive data
## Sensitive data exposure
### Context
Paycheck, address, bank account... are all sensitive data that should not be displayed on database in clear-text
### Danger
If an attacker manages to attack and access such a database, all sensitive information could be used for [[Phishing|phishing attacks]], to impersonate someone, access restricted services, or be sold
### Counter measures
- Ensure data and personal details are encrypted with a string algorithm, accepted by the security community
- Only store necessary data