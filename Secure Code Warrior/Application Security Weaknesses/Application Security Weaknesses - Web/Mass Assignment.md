---
tags: [authentification_and_access_control]
---
# Mass Assignment
## Context
In an application where API are exposed, Mass Assignment vulnerability occurs when API endpoints do not restrict which properties can be modified
## Danger
Attackers could edit their properties or provide fake input for a transaction
## Example
An attacker notices an application API uses a single endpoint to retrieve and update user data, and that this endpoint does not restrict all properties. For example, one of the properties sets the user privileges.
Changing the attacker's account privilege in a request, they are able to gain elevated privileges
## Counter Measures
- Parse request values rather than binding them directly to an object: [[Trust no Input|do not trust user input]]
- Use a reduced [[Data Transfer Object|Data Transfer Object (DTO)]] rather than binding directly to an object
- Ensure sensitive properties are deny-listed or only safe properties are allow-listed for direct object binding