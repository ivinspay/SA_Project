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
## 4) Admin Manges Users' Permission and Access
## 5) Push Notifications
![Notification Diagram](images/Notification_assurance_case_diagram_v2.png)
**Claim:** Zulip ensures users receive notifications meant for them  
  
**Sub-Claims:**  
Notifications content is unreadable in transit  
Only authenticated servers and devices can send/receive notifications  
Compromised accounts can be cut off  
One user cannot deny delivery to others  

**Evidence based on claims:**  
End-to-end encryptions  
Account deactivation and API key/session revocation  
Authenticated device/push registration  
Rate limiting  

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

# Part 2: Assess Alignment of Evidence
## Notification alignment  
* End-to-end encryption is highlighted in the [security and privacy](https://zulip.readthedocs.io/en/stable/production/mobile-push-notifications.html#security-and-privacy) section and ensures that the content and metadata are not visible to Apple, Google, or Zulip's Mobile Push Notification Service. This covers the readability of notifications from an outside source or someone listening or intercepting notifications.
* Zulip does support account deletion/deactivation via their [Other useful manage.py commands](https://zulip.readthedocs.io/en/stable/production/management-commands.html#other-useful-manage-py-commands). This covers ordinary malicious users and malicious users with stolen credentials of a legitmate account.
* I had to do a little research on Claude's recommendation of the push bouncer registration. This is just the middle man between Zulip and Apple or Google's Push Notification Service. Zulip's documentation does talk about the [cryptography](https://zulip.readthedocs.io/en/stable/production/mobile-push-notifications.html#cryptography) used in devices' registration with the actual Push Notification Server to ensure that the token given to a device does not get learned by the Zulip server while it is in transit to the bouncer.
* [Rate limiting](https://zulip.readthedocs.io/en/stable/production/mobile-push-notifications.html#rate-limits) is talked about shortly after the cryptography piece and says that the default rate limit is 1000 requests per minute but can be configured through support if a server is big enough to warrant a higher rate limit. This prevents Denial of Service attacks.

### Gaps
* Compromised servers could still cause issues due to sending malicious notifications and messages from a legitimate looking server.


**Highlight gaps:**
* Making sure changes are recorded in audit logs, while audit logs are implemented within source code. (Claim 1)

  
**Record AI Use:**
* Used AI for rewording of security rewuiremnets from last project to simplfy what they were saying for my claims. (Claim 1)
  
**Team Reflection**
Throughout this sprint/segment of the assignment I learned how to draw an assurance case diagram and over time fine tune it to be concise yet still show where there is evidence and where claims can fall short. I also leaned into the prompt engineering on this assignment to further strengthen my claims, rebuttals, and evidence to cover areas that I missed to begin with. I found the template that was provided for the assurance case very useful. To see an example laid out and how each branch from the claim led to more and more evidence helped me visualize my own assurance case diagram as I worked through piecing it together. 
