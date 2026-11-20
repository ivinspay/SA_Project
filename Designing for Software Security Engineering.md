# Part 1: Threat Modeling
**1.1: Project Overview**

This security engineering view focuses on threat modeling through Zulip's user accounts and profile management features. The focus is to prioritize past assurance cases/security requirements to protect information from unauthorized modifications. 

The course of action to support these scenarios are broken down into structured parts. First we are creating DFDs for our previous claims and combining them into several diagrams that have related claims. Second we are then analyzing those DFDs in more depth by looking at their STRIDE analysis; Spoofing, Tampering, Repudiation, Information Disclosure, Denial of Service, Elevation of Privilege. Mainly looking at the per interaction basis, that shows the source and target element connected by a data flow. Third then we can gather up potential threats based on the complexity of our DFDs. Then lastly, we will address threat mitigation and how we can; redesign to eliminate any threats mentioned from previous section, how to apply standard mitigations, how to invent new mitigations even if they seem to be risky, and what are you willing to accept in terms of vulnerability based from designing aspect. 

Then for observations, we will simply look at Zulip's existing protections and any recommendations based on those security gaps. Then lastly we will collaborate on how we went about project and what we concluded from process and what results tell us about our design capabilities. 

**1.2: Data Flow Diagrams (DFDs)**

**1.3: STRIDE Threat Analysis**

**1.4: Threat Analysis Details**

**1.5: Mitigation Strategies**
 payten
**1.6: HTML Reports (link)**


# AI Usage
havent decided yet


# Part 2: Observations

**2.1: Existing Protections for Zulip**

Zulip has a few existing potential security mechanisms designed to protect user accounts and profile information in respect to what we have created based on our project.

* Authorization

* Profile validation

Authentication

* Zulip does support a wide variety of authentication methods; email and password, social   authentication, Microsoft Entra ID, LDAP (including Active Directory), SAML, OpenID Connect,  JSON Web Tokens (JWT), Apache-based SSO with REMOTE_USER. All these methods verify a user's identity before fully granting them access to an account. Authentication is one of the most important features as its prevents unwanted access for users to access other user's accounts and modify any profile information in that process. 

Source: https://github.com/zulip/zulip/blob/main/docs/production/authentication-methods.md
   
7. Audit Logging


**2.2: Security Gaps & Recommendations**

**2.3: Team Collaboration**

**2.4: Team Reflection**

**2.5: Conclusion**


