Requirements for Software Security Engineering 

1) Use Case - Admin Manges users' permissions and access 

image: 

Actors: 
*Authorized Administrator (User)
*Ex-employees, Privilige seeking external actor (misuer)

Description of Use Case:
*The user (an organization administrator) manages team members permissions and access on Zulip. 
The admin user roles, adds, or removes users from groups, and deactivates or reactviattes accounts as needed. 
These features help the organization control who can access their team commmunications channels and what actions they can perform. 

Description of Misuse Case:
*A hacker steals team members credentials to attempt unauthorized actions in Zulip, such as gaining admin priviliges, 
changing group membership, or deactivating and reactiviating accounts. A terninated or disgruntltes emplyees may also attempt to reuse existing sessions or credentials after they have ben deactivated.

Security Requirements:
*SR1: Revoke sessions and reject authenticated requests when account is deactivated and or inactive.
*SR2: Restrict account activation/deactivation to authorized admins.
*SR3: Log and audit all acount activity for non-repudiation purposes.
*SR4: Restrict role changes by accounts without administartor priviliges.
*SR5: Enforce group member permissions.

2) Use Case - Authenicate User

image: 

Actors:
*Zulip User (user)
*Credential theft (misuser)
*Organization/Admin

Description of Use Case:
*The authenticated user allows the actual Zulip user to prove their identity before accessing Zulip organization information. 
The user has to submit authentication information that has to be monitored and approved; Zulip has to be validated and successful authenication results in a completed authentication session in the system. 

Description of Mis Use Case:
*Here the crdential theft obtains authentication through whatver gained, and then can use crdentials that have been compromised to gain access to insider information.

Security Requirements:
*SR6: Zulip needs to limit repeated failed authenticated requests to reduce password guessing type of attacks.
*SR7: Zulip needs to enforce password strength contraints when a user creates or chnages their passwords.
*SR8: Zulip should now store passwords appropriately secure password hashibg ratger than plaintext encryption. 
*SR9: Zulip now limits password reset to not abuse the password recovery mechanism intended for its actual use.
*SR10: Zulip has to allow authorized adminsitrators to configure certain authentication methods for its users. 

3) Phishing
4) Software issues 
5) Account issues

Overall Reflection of Team: 
What did you learn from this assignment? What did you find most useful?
Compile individual team member reflections into a single reflection for the team. 














