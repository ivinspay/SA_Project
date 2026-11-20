# Part 1: Threat Modeling
**1.1: Project Overview**

This security engineering view focuses on threat modeling through Zulip's user accounts and profile management features. The focus is to prioritize past assurance cases/security requirements to protect information from unauthorized modifications. 

The course of action to support these scenarios are broken down into structured parts. First we are creating DFDs for our previous claims and combining them into several diagrams that have related claims. Second we are then analyzing those DFDs in more depth by looking at their STRIDE analysis; Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege. Mainly looking at the per interaction basis, that shows the source and target element connected by a data flow. Third then we can gather up potential threats based on the complexity of our DFDs. Then lastly, we will address threat mitigation and how we can; redesign to eliminate any threats mentioned from previous section, how to apply standard mitigations, how to invent new mitigations even if they seem to be risky, and what are you willing to accept in terms of vulnerability based from designing aspect. 

Then for observations, we will simply look at Zulip's existing protections and any recommendations based on those security gaps. Then lastly we will collaborate on how we went about project and what we concluded from process and what results tell us about our design capabilities. 

**1.2: Data Flow Diagrams (DFDs)**  
For our notifications DFD, we came up with this diagram:  
![Notifications DFD](images/Notification_DFD.png)  
**1.3: STRIDE Threat Analysis**

**1.4: Threat Analysis Details**

**1.5: Mitigation Strategies**
 payten
 
**1.6: HTML Reports (link)**
 - [Threat Modeling Report for Zulip Sign-in, Messaging and Attachments](https://htmlpreview.github.io/?https://github.com/SA_Project/blob/main/images/Zulip%20Sign-in%2C%20Messaging%20and%20Attachments.htm)  
 - [Threat Modeling Report for Zulip Notifications](https://htmlpreview.github.io/?https://github.com/ivinspay/SA_Project/blob/main/reports/Notificaiton_report 2.htm)   

# Part 2: Observations

**2.1: Existing Protections for Zulip**

Zulip has a few existing potential security mechanisms designed to protect user accounts and profile information in respect to what we have created based on our project.

Authorization

* Zulip also offers permission checks that can control which users perform certain tasks within environment. These checks make sure that when a user changes information they have authroization and are authorized to modify. This part showed code of how that implemented within system and how each each key feature mentioned comes from authorization and each department e.g. Endpoint all can play a part in this process.

Source: https://github.com/zulip/zulip/blob/main/zerver/views/user_settings.py

Profile validation

* Zulip shows process update requests through the view of server-side application. This helps validate and ensure that the submitted information follows the applications set in place security requirements and inherently prevents invalid and unauthorized changes when flagged in system. This is also represented as code to do so, while providing different type of errors and how that is validated in system. 

Source: https://github.com/zulip/zulip/blob/main/zerver/views/user_settings.py

Authentication

* Zulip does support a wide variety of authentication methods; email and password, social   authentication, Microsoft Entra ID, LDAP (including Active Directory), SAML, OpenID Connect,  JSON Web Tokens (JWT), Apache-based SSO with REMOTE_USER. All these methods verify a user's identity before fully granting them access to an account. Authentication is one of the most important features as its prevents unwanted access for users to access other user's accounts and modify any profile information in that process. 

Source: https://github.com/zulip/zulip/blob/main/docs/production/authentication-methods.md
   
Audit Logging

* This is least emphasized but key importance in existing system and our teams project. The functionality records show how administration supports account related actions. These records in the files investigate changes and identify potenially unauthorized activity to show up. This is also code on how to do go about doing that within system. Interestingly here made are just extracting data from current models from authentication methods and using data to see for analytical purposes.

Source: https://github.com/zulip/zulip/blob/main/zerver/models/realm_audit_logs.py?utm_source=chatgpt.com

**2.2: Security Gaps & Recommendations**

**2.3: Team Collaboration**

**2.4: Team Reflection**

**2.5: Conclusion**


