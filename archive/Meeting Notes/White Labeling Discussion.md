---
date: 2024-01-03
name: white labeling discussion
---



Date: [[2024-01-03]]
Attendees: [[Dhaval Prajapati]] [[Vaibhav Jain]] [[Ralstan Vaz]] [[Sadiq Ali Zaveri]]
---

# Agenda
1. 
# Discussion notes
- ![[Screenshot 2024-01-03 at 12.36.59 PM.png]]
- On the fly login, if a new user comes with a new mobile number the user will have to be created with member and ls id
- Thank you page would be from mumbai indians
- Power the purchase history
- 3 API's
	- On the Fly login
		- There is a security risk
	- Get booking details
	- Purchase History

- CF Rules should also be in place so that users cannot go to other page only
- App code and hostnames would be validated for the event code, this would act as a second layer
- Would work only for indian mobile numbers
- SMS changes won't happen, same flow would be used.

- Mobile number and email are required for transactions
	- This still needs to be checked, how this would be implemented

- Check if user manages to update the profile after a member is created from MI.
- 
# Questions
- How many times is the JWT token generated?
	- JWT token would be short lived and that would be the session duration also.
- Email And SMS?
	- SMS changes won't happen, same flow would be used.
# Action items
- [ ] 


