---
tags: [insecure_development_practices]
---
# Business Logic
## Flawed logic
### Context
Coding bugs or Business flaws exist in the app
### Danger
Order is cancelled and attacker gets reimbursed, but still gets the product or service.
### Example
- User can enter coupon when finalising their purchase. If the user can click multiple times on "redeem coupon", it could be applied multiple times.
- User can cancel a purchase. If the article is granted before money is taken, then cancelling the order after the article is sent will give back the money while still sending the product
### Counter measures
- Application specific as it targets the business logic*
- Impact varies, but is usually high
- Test regularly
- Use [[Threat Modelling]]
- Design assumption should be stated
- Use flow diagrams

## Insufficient Validation
### Context
Any application where user is expected to enter input
### Danger
User may voluntarily or involuntarily break application or trigger unexpected events or behaviour
### Example
- User are expected to enter integer input to send money to another user. Entering negative value might take money from the other user instead
### Counter measures
- Check all input points and assume inputs will be malicious: in short, [[Trust no Input]]
- Implement an allow-list with valid input parameters
- Ensure checks made on client side are also made on server side
- Convert data to expected data type