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

### Security Claim #4: Access Prevention for Deactivated Accounts
**Overview:**

**Top Level Claim:** Zulip denies deactivated accounts access to protected organization resources after deactivation completes and while those accounts remain inactive. 

**Diagram:** ![Assurance Case](images/Sullivan_diagramV4.png)

**Ai Prompt:** You are an expert software security engineer. Your job is to improve my assurance claims for Zulip and suggest more. Ensure that all claims focus on stopping deactivated accounts from retaining access.  The claims should describe how Zulip blocks deactivated accounts from accessing protected organization resources. Each claim must include an entity, a critical security property, and the expected result. Address things like existing sessions, API keys, login attempts, and anything else that may be relevant. Identify clear rebuttals and develop supporting subclaims that resolve them. End every argument branch with existing, verified evidence from Zulip’s source code, tests, or documentation. Use noun phrases for evidence labels, provide direct source links. Do not make up or infer things that cannot be proven with verified evidence.

Revised Prompt: End every argument branch with concrete, measurable evidence that would support my claims. Identify which evidence that already exist and which evidence still needs to be verified. Use noun phrases to label the evidence, provide direct source links to existing code, tests, or documents. 

**Reflection on AI Usefulness:**
I have mixed opinions about using AI for this assignment. It helped me with brainstorming and putting my thoughts on paper. I often have a difficult time with coming up with the right words. It also helped with reviewing and understanding the source code.However, it made things much harder than I thought it would. I started by having it check my original work for correctness and clarity. I then wanted it to help me come up with better claims and make sure those claims were correct, could be proven and made sense in this context. I spent majority of the time second guessing myself because the AI would provide feedback on my originals thoughts and suggest something stronger but then make statements that were either wrong or based on assumptions that could not be proven. Multiple times, I had to present source code or ask a series of logical verification questions to disapprove a claim. It would eventually say, "yes you're right" after giving me reason after reason on why it was right. This caused multiple necessary and unnecessary changes to my diagram. Overall, I think AI is great for brainstorming and checking work. However, it has a bad habit of contradicting itself, which could lead you down a long and stressful rabbit hole. 

### Alignment of Evidence and Identified Gaps

**Evidence E1**: Session removal code and inactive session rejection test
Zulip’s source code includes the delete_user_sessions function and the test_clear_sessions, and test_send_deactivated_user tests. The function removes the user’s sessions, while the tests check that deactivation removes those sessions and that further attempts to access the resources are rejected. This evidence supports Sub claims C1, C2, and C3 by addressing session removal and rejection of access through retained sessions. 

**Gaps**: The source code and tests were reviewed, but the test were not officially executed.  The tests need to be executed to confirm that sessions are removed and retained sessions are rejected. 
Source: [delete_user_sessions](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/lib/sessions.py#L50-L53), [test_clear_sessions](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_users.py#L2392-L2409), and [test_send_deactivated_user](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_decorators.py#L750-L794)

**Evidence E2**: Account status validation code and inactive API checks
Zulip’s source code includes the validate_account_and_subdomain function and the test_send_deactivated_user test. The function rejects inactive accounts.  The test checks if a deactivated account can send a message using its API key. This evidence supports C4 and C5 through the shared inactive account check a test that expects HTTP 401 when an inactive account attempts to send a message using its API credentials.  

**Gaps**: The reviewed code supports inactive account rejection through shared API authentication. However, this was not tested in this review.
 Source: [validate_account_and_subdomain](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/decorator.py#L280-L310), [test_send_deactivated_user](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_decorators.py#L750-L794), and [Shared Authentication Code](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/decorator.py#L784-L833)

**Evidence E3**: Password and SAML inactive account login checks 
Zulip’s source code includes test_login_deactivated_user and test_external_auth_id_saml_deactivated_user. These tests check to see if password and SAML login attempts are rejected after account deactivation.  They support C6 and C7 by checking that a login request from a deactivated account does not restore access. 
**Gaps**: The existing code was reviewed, but it was not tested. The authentication setup needs to be verified through testing in the environment. 
Source: [test_login_deactivated_user](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_decorators.py#L813-L824), [test_external_auth_id_saml_deactivated_user](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/tests/test_auth_backends.py#L4526-L4580)

**Evidence E4**: Account status update and profile cache removal code
Zulip’s source code includes change_user_is_active, flush_user_profile, and delete_user_profile_caches. These functions save the account’s inactive status and clear the affected cache profiles. These functions support C9 and partially support C8 by showing how account deactivation triggers the removal of affected cached information.

**Gaps**: The code shows that affected cached profiles are cleared.  However, verification is needed on whether request started deactivation use the correct account status when other request overlap deactivation. 
Source: [change_user_is_active](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/actions/users.py#L240-L253), [flush_user_profile](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/lib/cache.py#L689-L698), and  [delete_user_profile_caches](https://github.com/zulip/zulip/blob/ef6e64bd3cb4e2fe7ed993e68e3b05ff576ee816/zerver/lib/cache.py#L612-L628).

**Reflection**:
The assurance case I worked one was interesting. I thought it would be easy to think through, but it turned out be more challenging than I expected. Despite those challenges, the deep dive into Zulip's documentation was very informative. I learned a lot about how it handles account deactivation and the security checks needed to prevent. It is a complicated process because someone could attempt to access the system through retained sessions, saved API keys, or valid login credentials. Zulip has to coordinate several security checks to block these access methods while the account remains inactive. Its source code and documentation was extremely useful because I could follow the relevant functions and understand how connected to the claims I was trying to prove. 


Security Claim #5: Push Notifications

**Part 2**
-Highlight gaps
-Record AI Use
-Team Reflection

