# Part 1: Assurance Cases for Software Security Engineering
## 1) Security Claim: Account Issues

image: ![Security_Claim1Diagram](images/Security_Claim1Diagram.drawio.png)
**Claim:** 
* Zulip protects user profile information against unauthorizes modifications.
  
**Argument:**
* Zulip helps user profile information by verifying authorization for profile changes, preventing unauthorized modifications. 

**Sub-Claims:**
* SR21: Profile Ownership 
* SR22: Unauthorized Profile Changes
* SR23: Admin Profile Restrictions
* SR24: Profile Update Validation
* SR25: Account Chnage Auditing
  
**Evidence based on claims:**
* SR21: Profile-update authorization checks in source code and tests
* SR22: Authorization checks and tests for authorized profile changes
* SR23: Document and tests for admin controlled profile-editing restrictions
* SR24: Profiles-update input validation code and rejection tests
* SR25: Audit-log implement and test for profile/account

## 2) Security Claim: Software Issues
## 3) Security Claim: Authentication

image: <img width="1331" height="1042" alt="Assurance Case3 drawio-2-10 drawio" src="https://github.com/user-attachments/assets/b57f14bb-583f-4b02-ae32-eafa9f33bb9e" />


**Claim:**
* C1: The system securely authenticates users to ensure that only legitimate users can access their accounts.

**Argument:**
* The system protects user accounts through secure authentication mechanisms, including secure password hashing, password-strength enforcement, brute-force monitoring, rate limiting, and secure password recovery. User identity can be verified through user IDs and security questions, while administrative configuration and single sign-on (SSO) policies provide additional authentication controls.

**Sub-Claims:**

* C2: User can contact an administrator or technical support for assistance.
* C3: User identity can be verified.
* C4: Technical support can be verified.
* C5: The system securely authenticates users.
* C6: The system recovers passwords safely.

**Evidence based on claims:**

*E1: User ID used as evidence to support user identification and verification.
* E2: Security questions used to help verify user identity.
* E3: Security questions used as evidence to support verification procedures.
* E4: Secure password hashing to protect stored passwords.
* E5: Password-strength enforcement to ensure users create stronger passwords.
* E6: Administrative configuration logs to support monitoring of authentication-related settings.
* E7: Single sign-on (SSO) policy settings to support secure authentication.
* E8: Brute-force monitoring logs to help detect repeated or suspicious login attempts.
* E9: Rate limiting to restrict excessive authentication attempts.
* E10: Password-reset expiration to limit the validity of password-recovery links or tokens.
* E11: Recovery controls to support secure account recovery.

**Context:**

*CT1: The user is an employee.
* CT2: An administrator is also a user of the system.

**Rebuttals and Undercutting Arguments:**

* R1: The user may be unable to access the account or log in.
* R2: The person requesting assistance may be an imposter.
* R3: The person claiming to provide support may be an imposter.
* R4: The user may forget their password.
* UC1: The authentication process may not be secure.


## 4) Admin Manges Users' Permission and Access
## 5) Push Notofications

# Part 2: Access Alignment of Evidence

**Highlight gaps:**
* Making sure changes are recorded in audit logs, while audit logs are implemented within source code. (Claim 1)
  
**Record AI Use:**
* Used AI for rewording of security rewuiremnets from last project to simplfy what they were saying for my claims. (Claim 1)
  
**Team Reflection**

