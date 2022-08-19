# Trust no input
## Context
User or hackers will input malformed data
## Danger
Application can crash, or there might be a risk of injection (command, SQL...)
## Counter measures
- Implement input validation: character blacklist (&, /, \...), type validation...
- Validate fields, files, other services and databases
- Provide dropdown instead of text field
- Implement server side validation, such as: exact match (x == CONST), allow-listing or deny-listing
- Clean and/or escape inputs