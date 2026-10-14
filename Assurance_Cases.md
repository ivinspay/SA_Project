[gemini-code-1791940097609.txt](https://github.com/user-attachments/files/33411422/gemini-code-1791940097609.txt)# Part 1: Assurance Cases for Software Security Engineering
## 1) Security Claim: Account Issues

image: ![SecurityClaim1.png](images/SecurityClaim1.png)
**Claim:** 
* C1: Zulip protects user profile information against unauthorized modifications.
  
**Argument:**
* Zulip helps user profile information by verifying that its users have the permissions required to make profile changes, preventing users from modifying other users' profiles without proper authorization, this allows administrators to restrict certain profile settings through configuration, validating profile-update requests, and that maintains audit logs by significant profile account changes. All of these together help reduce the overall risk of authorized or improper modification controls. I wanted to add the security requirements SR21-SR25 to show the security requirements that are needed to guide the next phase of this case. It also helps build stronger claims for where evidence was drawn and why, while also supporting and recognizing weaknesses in next phase of these case and how they can be solved. 

**Sub-Claims:**
* C1(SR21): Profile Ownership - Zulip verifies that a user has authorized access to modify specific profile settings with requested change. 
* C2(SR22): Unauthorized Profile Changes - Zulip also prevents users from modifying another users' personal information without permission or authorization. 
* C3(SR23): Admin Profile Restrictions - Zulip allows organizations/server admins to restrict profile changes in regards to organizational and configuration settings. 
* C4(SR24): Profile Update Validation - Zulip validates profile-update requests and the rejects requests that are unauthorized, wrong or ones that do not meet conditions. 
* C5(SR25): Account Change Auditing - Zulip maintains its auditable records of significant profiles and account changes to support when needed for investigations regarding suspicious or unauthorized activity. 
  
**Evidence based on claims:**
* E1(SR21): The source-code inspection and tests demonstrate that the profile-update requests are being verified by the users' authorization to modify the specified profile they should be accessing. 
* E2(SR22): The permission-checking logic, access-control implementation, and tests elaborate on how unauthorized attempts are modified by another users' profile and is rejected at whole. 
* E3(SR23): Documentation, configuration settings, and tests prove that administrators can restrict profile changes, that can be as small or little from someones name or there avatar (according to policy). 
* E4(SR24): The profile-update validation code and rejection tests show miss information and unauthorized requests are not accepted. 
* E5(SR25): One of most important pieces, audit-log implementation, relevant documentation, and testing establish that profile or account changes are recorded properly in first place to be later used for investigative purposes. 

 **Context**
* CT1: This claims applies to Zulip user accounts and their profile information, focusing primarily on protection against unauthorized profile modifications; authorization checks, access controls, admin restrictions, requests validation, and auditing.

**Rebuttals**
* R1: If the profile-update authorization checks are not correctly verifying target profiles, a user could then modify a profile that they do not have access too. 
* R2: If permission checks fail or are incomplete more than once, unauthorized users could modify another users' personal information.
* R3: If administrator restrictions are misconfigured, unavailable, or not enforced,, users can make those profile changes that organizations policies prohibit. 
* R4: If request validation fails and all the relevant inputs, authorization conditions, missing or suspicious requests could then be accepted and in result improper profile modifications are put into place. 
* R5: If audit logging is missing or inaccurate, investigators may not be able to do their job properly and determine profile changes have occurred/who performed tasks. 

**AI Use**

**AI Prompt Response**
```
C0: Zulip protects user profile information against unauthorized modifications.
C1: Profile Ownership (SR21)
- E1: Verify authorization checks ensure users can only modify their own profiles.
- R1: Authorization checks may not prevent all unauthorized profile changes.
C2: Unauthorized Profile Changes (SR22)
- E2: Test that users cannot modify other users' profiles without permission.
- R2: Authorization weaknesses may allow unauthorized modifications.
C3: Admin Profile Restrictions (SR23)
- E3: Verify administrator settings restrict profile changes as intended.
- R3: Administrative restrictions may not be consistently enforced.
C4: Profile Update Validation (SR24)
- E4: Test that malformed and unauthorized profile-update requests are rejected.
- R4: Invalid requests may bypass validation.
C5: Account Change Auditing (SR25)
- E5: Verify audit logs record significant profile and account changes.
- R5: Incomplete audit logs may make investigations difficult.
```
**AI Usefulness for Account Issues**
This prompt was useful in the sense that it identified my cases weakness from the claims and evidence standpoints. It helped me brainstorm that users can modify their own profiles and by doing so, admin restrictions are enforced for this case and missing information is rejected. The other issues when it came to audit-logs, when missing and/or incomplete can make it harder for investigate unauthorized changes appropriately. These suggestions are very minor, but helped me identify areas where the evidence and rebuttals needed to be stronger for overall better security of my account issue case. 

**Gap**
* E1-E2 - Needed to verify that authorixation checks are put in place to prevent users from modyifing profile they do not own.
* E3: Need to confirm that admintrators restrictions work as intended.
* E4: Need evidence that invalid or unauthroized profile-updates requests could be rejected.
* E5: Need to verify that audit logs record only significant account changes completely and most accurate ways possible.
  
**Reflection**
This phase showed many gaps between how security requirements and evidence are very much needed to support security overall. E.g. listing authorization checks and audit logs are not enough, the verification that each work properly through Zulips source, documentation, and testing. The AI response also showed the weaknesses and strengthens n rebuttals, ultimately showing that this assurance case needs more evidence to address reasoning and claims that it could fail and what to do in that scenario. 

## 2) Security Claim: Software Issues
image: ![Assurance Diagram](images/AssuranceDiagramTW.drawio1.png)

**Analysis/Gaps:**
Looking at the diagram versus Zulip's documentation, the strongest (still weak but fixable) branch in our assurance case tree would be the tamper branch (Logs can't be altered or deleted without detection). In [Zulip's docs](https://zulip.readthedocs.io/en/latest/production/export-and-import.html#preventing-changes-during-the-export), we found that when exporting files you can actually shutdown the instance and lock everyone out of it before exporting, "so that nobody can send new messages (etc.) while you’re exporting data." This export of data includes an archive of all uploaded files by an organization, so this concept could be be applied to logging so that data can't be tampered with when pulling it, but this is not available today and would need to be built. Our weakest branch seems to be our completeness branch (Every download is recorded in the log). I couldn't find any documentation that showed that Zulip logs included any information like that, not even for messages. Zulip's logs are strictly error logs. 

I didn’t really use a prompt with AI during this assignment in the typical way that someone would probably use one. I fed the AI the key points found in the instructions and asked it to guide me through finding the answers. It gave me a step-by-step list of things to do and as we went through them the chatbot gave me feedback and tips to improve my answers as soon as I submitted them. I would say this was extremely useful in helping me understand the assignment and the material more.


**Reflection:**
During this assignment, I learned just how much work it takes to effectively backup a claim. Our top claim fell apart when I checked it, because Zulip doesn’t have download logs, so I rewrote it to be about how the organization deploys Zulip, and the missing feature turned into a gap for Part 2 instead of a hole in the argument. I think that writing the rebuttals helped the most. I took each word in the claim and asked how it could be wrong, and that’s how I came up with things like admins editing logs without anyone noticing, bulk exports that don’t get logged, and downloads that don’t need a login.


## 3) Security Claim: Authentication

image: <img width="1331" height="1042" alt="Assurance Case3 drawio-11 drawio" src="https://github.com/user-attachments/assets/d9f52a3a-8487-4776-9ee7-eb4107ebed6d" />

**Claim:**
* CT1: The system securely authenticates users to ensure that only legitimate users can access their accounts.

**Argument:**
* The system protects user accounts through secure authentication mechanisms, including secure password hashing, password-strength enforcement, brute-force monitoring, rate limiting, and secure password recovery. User identity can be verified through user IDs and security questions, while administrative configuration and single sign-on (SSO) policies provide additional authentication controls.

**Sub-Claims:**

* C2: User can contact an administrator or technical support for assistance.
* C3: User identity can be verified.
* C4: Technical support can be verified.
* C5: The system securely authenticates users.
* C6: The system recovers passwords safely.

**Evidence based on claims:**

* E1: User ID used as evidence to support user identification and verification.
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

* CT1: The user is an employee.
* CT2: An administrator is also a user of the system.

**Rebuttals and Undercutting Arguments:**

* R1: The user may be unable to access the account or log in.
* R2: The person requesting assistance may be an imposter.
* R3: The person claiming to provide support may be an imposter.
* R4: The user may forget their password.
* UC1: The authentication process may not be secure.

**AI USE:**
I asked Gemini to help review my drafts. My initial prompt included a rough draft assurance case, misuse case, and misuse case details. I edited my draft based on the responses and if I felt confused about the diagram (specifically, about how cluttered the right branch was or the lines which were getting messy). Gemini gave me options helping me brainstorm sub-claims and rebuttals to help declutter my right branch. Then I had Gemini review my finished draft for inconsistencies. 

**Prompt**
Image: <img width="1019" height="651" alt="Screenshot 2026-10-13 at 8 21 01 PM" src="https://github.com/user-attachments/assets/12f3fe01-b211-472a-b918-6213021119f8" />



**Alignment of Evidence and Identified Gaps**

**Evidence E1 & E2 & E3 (User Identification & Support Verification):**

**User ID and Security Questions for Identity Verification**
The authentication process uses user ID records (E1) along with security question procedures (E2, E3) to verify identity during account recovery and support inquiries. This evidence supports C2 (Contacting support for assistance), C3 (Identity verification), and C4 (Technical support verification) by establishing standard verification channels when users lose access.

**Gaps:** Security questions rely on fixed user knowledge, which can be vulnerable to social engineering or guessing. While these mechanisms verify user identity on paper, further verification is needed to determine if multi-factor authentication (MFA) or out-of-band verification is enforced during high-risk support interactions.

**Evidence E4 & E5 (Password Security & Enforcement):**

**Password Hashing and Strength Enforcement**
Zulip implements password hashing (E4) to protect stored user credentials and password-strength policies (E5) to ensure users create complex passwords during creation and reset. This directly supports sub-claim C5 (Secure system authentication) by mitigating offline dictionary attacks and weak password compromises.
**Gaps:** The presence of password-strength checks ensures complexity, but test execution is required to confirm whether custom dictionary checks or credential-stuffing protections are actively enforced at runtime.

**Evidence E6 & E7 (Administrative & SSO Governance):**

**Audit Logs and Single Sign-On (SSO) Policy Settings**

Administrative configuration logs (E6) capture changes to authentication settings, while SSO policy settings (E7) allow organizations to delegate authentication to external identity providers (OAuth/SAML). This supports C5 (Secure authentication) by enforcing centralized policy controls and auditing administrative overrides.
Gaps: While SSO policies reduce password sprawl, fallback local authentication options might leave secondary login vectors open if not explicitly disabled by administrators.

**Evidence E8 & E9 (Brute-Force Protection & Rate Limiting):**

**Brute-Force Monitoring and Rate Limiting Controls**
Brute-force monitoring logs (E8) and rate-limiting rules (E9) track and restrict excessive failed authentication attempts. This supports C5 (Secure authentication) and addresses rebuttal UC1 (Insecure authentication process) by throttling automated login attacks against user accounts.

**Gaps:** Rate limiting is enforced per endpoint/IP, but distributed brute-force attacks across varying IP blocks need empirical testing to verify if account lockout thresholds trigger cleanly.

**Evidence E10 & E11 (Password Recovery Controls):**

**Password-Reset Expiration and Account Recovery Procedures**
Password-reset token expiration limits (E10) alongside secure recovery workflows (E11) support C6 (Safe password recovery). This directly mitigates rebuttal R4 (User forgot password) and R1 (Inability to log in) by ensuring recovery links expire quickly and cannot be reused by malicious actors.

**Gaps:** Token expiration mechanisms exist in code, but end-to-end testing is needed to confirm that active sessions are terminated immediately upon a password reset completion.

**Reflection:**
I initially thought authentication would be a straightforward topic to cover, but working through this assurance case revealed far more nuances than I realized. While establishing that Zulip authenticates users is simple on the surface, mapping out how the system handles identity verification, rate limiting, password reset lifecycles, and SSO governance required looking at multiple interconnected layers of security controls. Writing the rebuttals and undercutting arguments was particularly helpful because it forced me to think about what could happen to decrease trust,such as rebuttals and undercutting,by asking how a password recovery link could be abused, how brute-force throttling could be bypassed, or how an imposter might exploit technical support workflows. Reorganizing the evidence tree to address these gaps made the overall argument much stronger and gave me a much deeper appreciation for how many moving parts are involved in securing user authentication.

## 4) Security Claim: Access Prevention for Deactivated Accounts

**Diagram:** ![Assurance Case](images/Sullivan_diagramV4.png)

**Argument:** 
* The assurance case argues that Zulip denies deactivated accounts access to protected organization resources after deactivation completes and while those accounts remain inactive. Security mechanisms such as invalidating existing sessions, rejecting retained session cookies, checking account status on API requests, blocking password and SAML logins, and removing cached user profiles collectively prevent these accounts from retaining or regaining access while inactive.

**Top Level Claim:** 
* Zulip denies deactivated accounts access to protected organization resources after deactivation completes and while those accounts remain inactive. 

**Ai Prompt:** 
* You are an expert software security engineer. Your job is to improve my assurance claims for Zulip and suggest more. Ensure that all claims focus on stopping deactivated accounts from retaining access.  The claims should describe how Zulip blocks deactivated accounts from accessing protected organization resources. Each claim must include an entity, a critical security property, and the expected result. Address things like existing sessions, API keys, login attempts, and anything else that may be relevant. Identify clear rebuttals and develop supporting subclaims that resolve them. End every argument branch with existing, verified evidence from Zulip’s source code, tests, or documentation. Use noun phrases for evidence labels, provide direct source links. Do not make up or infer things that cannot be proven with verified evidence.

* Revised Prompt: End every argument branch with concrete, measurable evidence that would support my claims. Identify which evidence that already exist and which evidence still needs to be verified. Use noun phrases to label the evidence, provide direct source links to existing code, tests, or documents. 

**Reflection on AI Usefulness:**
* I have mixed opinions about using AI for this assignment. It helped me with brainstorming and putting my thoughts on paper. I often have a difficult time with coming up with the right words. It also helped with reviewing and understanding the source code.However, it made things much harder than I thought it would. I started by having it check my original work for correctness and clarity. I then wanted it to help me come up with better claims and make sure those claims were correct, could be proven and made sense in this context. I spent majority of the time second guessing myself because the AI would provide feedback on my originals thoughts and suggest something stronger but then make statements that were either wrong or based on assumptions that could not be proven. Multiple times, I had to present source code or ask a series of logical verification questions to disapprove a claim. It would eventually say, "yes you're right" after giving me reason after reason on why it was right. This caused multiple necessary and unnecessary changes to my diagram. Overall, I think AI is great for brainstorming and checking work. However, it has a bad habit of contradicting itself, which could lead you down a long and stressful rabbit hole. 

### Alignment of Evidence and Identified Gaps

**Evidence E1**: 
* Session removal code and inactive session rejection test
Zulip’s source code includes the delete_user_sessions function and the test_clear_sessions, and test_send_deactivated_user tests. The function removes the user’s sessions, while the tests check that deactivation removes those sessions and that further attempts to access the resources are rejected. This evidence supports Sub claims C1, C2, and C3 by addressing session removal and rejection of access through retained sessions. 

* Gaps: The source code and tests were reviewed, but the test were not officially executed.  The tests need to be executed to confirm that sessions are removed and retained sessions are rejected. Source: [delete_user_sessions](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/lib/sessions.py#L50-L53), [test_clear_sessions](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_users.py#L2392-L2409), and [test_send_deactivated_user](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_decorators.py#L750-L794)

**Evidence E2**: 
* Account status validation code and inactive API checks
Zulip’s source code includes the validate_account_and_subdomain function and the test_send_deactivated_user test. The function rejects inactive accounts.  The test checks if a deactivated account can send a message using its API key. This evidence supports C4 and C5 through the shared inactive account check a test that expects HTTP 401 when an inactive account attempts to send a message using its API credentials.  

* Gaps: The reviewed code supports inactive account rejection through shared API authentication. However, this was not tested in this review.
 Source: [validate_account_and_subdomain](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/decorator.py#L280-L310), [test_send_deactivated_user](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_decorators.py#L750-L794), and [Shared Authentication Code](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/decorator.py#L784-L833)

**Evidence E3**: 
* Password and SAML inactive account login checks 
Zulip’s source code includes test_login_deactivated_user and test_external_auth_id_saml_deactivated_user. These tests check to see if password and SAML login attempts are rejected after account deactivation.  They support C6 and C7 by checking that a login request from a deactivated account does not restore access.

* Gaps: The existing code was reviewed, but it was not tested. The authentication setup needs to be verified through testing in the environment. 
Source: [test_login_deactivated_user](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_decorators.py#L813-L824), [test_external_auth_id_saml_deactivated_user](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_auth_backends.py#L4526-L4580)

**Evidence E4**: 
* Account status update and profile cache removal code
Zulip’s source code includes change_user_is_active, flush_user_profile, and delete_user_profile_caches. These functions save the account’s inactive status and clear the affected cache profiles. These functions support C9 and partially support C8 by showing how account deactivation triggers the removal of affected cached information.

* Gaps: The code shows that affected cached profiles are cleared.  However, verification is needed on whether request started after deactivation consistently use the correct account status when other request overlap deactivation. 
Source: [change_user_is_active](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/actions/users.py#L240-L253), [flush_user_profile](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/lib/cache.py#L689-L698), and  [delete_user_profile_caches](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/lib/cache.py#L612-L628).

**Reflection**:
* The assurance case I worked one was interesting. I thought it would be easy to think through, but it turned out be more challenging than I expected. Despite those challenges, the deep dive into Zulip's documentation was very informative. I learned a lot about how it handles account deactivation and the security checks needed to prevent. It is a complicated process because someone could attempt to access the system through retained sessions, saved API keys, or valid login credentials. Zulip has to coordinate several security checks to block these access methods while the account remains inactive. Its source code and documentation was extremely useful because I could follow the relevant functions and understand how connected to the claims I was trying to prove.
  
## 5) Push Notofications
![Notification Diagram](images/Notification_assurance_case_diagram_v2.png)

### AI Use  
I took pieces of the example prompts in the assignment and modified them with information from the slides. Included in the prompt were my original claims, rebuttals, evidence and one undermine. I was struggling coming up with more evidence and rebuttals and Claude helped flesh out the ones I had and suggested ones I missed.

```
You are an expert software security engineer. Your job is to inspect and suggest edits to a list of claims, evidence, rebuttals
and undermines, etc. in an assurance case review. A claim is always worded with a predicate. Avoid claims about the supporting
method/techniques. Claims should be a reasonable goal. Good arguments eliminate identified doubts or rebuttals. Claims are
used to eliminate the doubts. Example of a good claim: "The system minimizes information disclosure during communication"
Doubts can attack claims, evidence, or inferences. Here is an example claim with evidence, rebuttals, and an undermine.
Analyze based on mobile push notifications, and the threat actors to focus on are malicious users and compromised servers.

Claim: Zulip ensures that users receive notifications meant for them
Rebuttal 1: A malicious actor intercepts a message
Claim 1.1: Zulip ensures there is end to end encryption
Claim 1.2: Zulip uses notification certification and authentication
Rebuttal 1.1.1/1.2.1: Unless the message was sent from a compromised account
Rebuttal 2: A malicious user wants to perform a denial of service attack
Evidence 2: Zulip uses rate limiting

Use this as a potential claim for analysis, ask any clarifying questions
```  
The following list is part of what Claude generated in response:
```
C0: Zulip ensures users receive notifications meant for them

R1: A malicious actor intercepts a message
  C1.1: Notification content is unreadable in transit
    E1.1: End-to-end encryption of push payloads
    R1.1.1: Sent from a compromised account
      C1.1.1: Compromised accounts can be cut off
        E1.1.1: Account deactivation and API key/session revocation
  C1.2: Only authenticated servers and devices can send/receive notifications
    E1.2: Push bouncer registration with server authentication and
          user-bound device tokens
    R1.2.1: Sent from a compromised account
      C1.2.1: Compromised accounts can be cut off
        E1.2.1: Same as E1.1.1

R2: A malicious user performs a denial of service
  C2: One user cannot deny delivery to others
    E2: Rate limiting
```
### Notification alignment  
* End-to-end encryption is highlighted in the [security and privacy](https://zulip.readthedocs.io/en/stable/production/mobile-push-notifications.html#security-and-privacy) section and ensures that the content and metadata are not visible to Apple, Google, or Zulip's Mobile Push Notification Service. This covers the readability of notifications from an outside source or someone listening or intercepting notifications.
* Zulip does support account deletion/deactivation via their [Other useful manage.py commands](https://zulip.readthedocs.io/en/stable/production/management-commands.html#other-useful-manage-py-commands). This covers ordinary malicious users and malicious users with stolen credentials of a legitmate account.
* I had to do a little research on Claude's recommendation of the push bouncer registration. This is just the middle man between Zulip and Apple or Google's Push Notification Service. Zulip's documentation does talk about the [cryptography](https://zulip.readthedocs.io/en/stable/production/mobile-push-notifications.html#cryptography) used in devices' registration with the actual Push Notification Server to ensure that the token given to a device does not get learned by the Zulip server while it is in transit to the bouncer.
* [Rate limiting](https://zulip.readthedocs.io/en/stable/production/mobile-push-notifications.html#rate-limits) is talked about shortly after the cryptography piece and says that the default rate limit is 1000 requests per minute but can be configured through support if a server is big enough to warrant a higher rate limit. This prevents Denial of Service attacks.

### Gaps
* Compromised servers could still cause issues due to sending malicious notifications and messages from a legitimate looking server.

### Reflection
Throughout this sprint/segment of the assignment I learned how to draw an assurance case diagram and over time fine tune it to be concise yet still show where there is evidence and where claims can fall short. I also leaned into the prompt engineering on this assignment to further strengthen my claims, rebuttals, and evidence to cover areas that I missed to begin with. I found the template that was provided for the assurance case very useful. To see an example laid out and how each branch from the claim led to more and more evidence helped me visualize my own assurance case diagram as I worked through piecing it together.

# Part 2: Access Alignment of Evidence
  
**Team Reflection**

