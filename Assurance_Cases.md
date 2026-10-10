**Part 1: Assurance Cases for Software Security Engineering**

**Security Claim #1: Account Issues**
**Diagram:** <img width="962" height="985" alt="image" src="https://github.com/user-attachments/assets/fd5c3398-eb01-4a96-80cc-39175c9da5ce" />
**Claim:** Zulip protects user profile information against unauthorizes modifications.
Argument: Zulip helps user profile information by verifying authorization for profile changes, preventing unauthorized modifications. 
**Sub-Claims:**
SR21: Profile Ownership 
SR22: Unauthorized Profile Changes
SR23: Admin Profile Restrictions
SR24: Profile Update Validation
SR25: Account Chnage Auditing
**Evidence based on claims:**
SR21: Profile-update authorization checks in source code and tests
SR22: Authorization checks and tests for authorized profile changes
SR23: Document and tests for admin controlled profile-editing restrictions
SR24: Profiles-update input validation code and rejection tests
SR25: Audit-log implement and test for profile/account

Security Claim #2: Software Issues
Security Claim #3: Authentication

**Security Claim #4: Admin Manages Users' Permission and Access**

**Diagram:** ![Assurance Case](images/Sullivan_assurancecase2.png)

**Claim:** Deactivated Zulip accounts cannot retain access to protected organization resources

**Ai Prompt:** You are an expert software security engineer. Your job is to improve my assurance claims for Zulip and suggest more. Ensure that all claims focus on stopping deactivated accounts from retaining access.  The claims should describe how Zulip blocks deactivated accounts from accessing protected organization resources. Each claim must include an entity, a critical security property, and the expected result. Address things like existing sessions, API keys, login attempts, and anything else that may be relevant. Identify clear rebuttals and develop supporting subclaims that resolve them. End every argument branch with existing, verified evidence from Zulip’s source code, tests, or documentation. Use noun phrases for evidence labels, provide direct source links. Do not make up or infer things that cannot be proven with verified evidence.

Security Claim #5: Push Notifications

**Part 2**
-Highlight gaps
-Record AI Use
-Team Reflection

