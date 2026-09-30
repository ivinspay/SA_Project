# Part 1: Requirements for Software Security Engineering 

## 1) Use Case - Admin Manges Users' Permissions and Access 

image: ![Admin manges permissions and access Use/Misuse Case Diagram](images/sullivan_usecase.png)

**Actors:**
* Authorized Administrator (User)
* Ex-employees, Privilige seeking external actor (misuer)

**Description of Use Case:**

The user (an organization administrator) manages team members permissions and access on Zulip. 
The admin user roles, adds, or removes users from groups, and deactivates or reactivates accounts as needed. 
These features help the organization control who can access their teams commmunication channels and what actions they can perform. 

**Description of Misuse Case:**
A hacker steals team members credentials to attempt unauthorized actions in Zulip, such as gaining admin priviliges, 
changing group membership, or deactivating and reactiviating accounts. A terminated or disgruntled employees may also attempt to reuse existing sessions or credentials after they have been deactivated.

**Security Requirements:**

**SR1:** Revoke sessions and reject authenticated requests when account is deactivated and or inactive.

**SR2:** Restrict account activation/deactivation to authorized admins.

**SR3:** Log and audit all acount activity for non-repudiation purposes.

**SR4:** Restrict role changes by accounts without administartor priviliges.

**SR5:** Enforce group member permissions.

**Assessment:**

Zulip’s advertised security features support the security requirements. However, the strength of the alignment varies. It implements a user-update API which enforces RBAC to restrict changes to admins and owners addressing the privilege escalation scenario. Zulip let organizations control who can add, remove, join, or leave groups supporting the group membership permission requirement. One issue with this is that this permission can be given too broadly, allowing unwanted membership changes. Zulips deactivation features meet the requirement to restrict account management to admins and block access after account has been deactivated.  A reactivated account keeps its previous permissions and API key making usable if stolen under the right conditions. Zulip advertises permanent long-term audit logs for important actions satisfying the requirement of log and audit account activity, but the documentation does not show if these logs can be altered themselves. Overall these features provide decent protection, but it will be difficult to prevent someone who already has elevated permissions from misusing the system.

**Personal Reflection:**

I learned more about identifying threats, understanding how vulnerabilities can be exploited, and finding ways to mitigate them. This assignment helped me think through possible attack pathways and how developers can address security issues before they become problems. I also took a deeper dive into how Zulip works and how its specific features address different security risk. At first, I found it difficult to think through how certain features may be exploited but it became clearer over the many iterations of my diagram. 

## 2) Use Case - Authenicate User

image: ![](images/UseDiagramPayten.png)

**Actors:**

* Zulip User (user)
* Credential theft (misuser)
* Organization/Admin

**Description of Use Case:**
The authenticated user allows the actual Zulip user to prove their identity before accessing Zulip organization information. 
The user has to submit authentication information that has to be monitored and approved; Zulip has to be validated and successful authenication results in a completed authentication session in the system. 

**Description of Mis Use Case:**
*Here the crdential theft obtains authentication through whatver gained, and then can use crdentials that have been compromised to gain access to insider information.

**Security Requirements:**

**SR6:** Zulip needs to limit repeated failed authenticated requests to reduce password guessing type of attacks.

**SR7:** Zulip needs to enforce password strength contraints when a user creates or chnages their passwords.

**SR8:** Zulip should now store passwords appropriately secure password hashibg ratger than plaintext encryption. 

**SR9:** Zulip now limits password reset to not abuse the password recovery mechanism intended for its actual use.

**SR10:** Zulip has to allow authorized adminsitrators to configure certain authentication methods for its users. 

## 3) Use Case - Mobile Push Notifications from a Malicious or Compromised Server

image: ![Notifications Use/Misuse Case Diagram](images/NotificationUseCase.png)

**Actors:**

* Zulip User (user), Zulip mobile app, Zulip server/mobile push notification service
* User with access to a compromised server (misuser)

**Description of Use Case:**
A user wants to be notified on their phone appropriately whenever they are tagged or miss a message in their Zulip server. The user expects this notification to be coming from a trusted source and with reliable intel.
If the user is receiving a private message, they expect that it is only sent to them and no one else can access the contents.

**Description of Misuse Case:**
A malicious user wants to send malicious or fake notifications to users to get a user to click on a malicious link or spam a legitimate user with unwanted notifications.
Doing this would cause unwanted resource usage for the user's mobile device or if enough messages are sent a Denial of Service attack. 
This could also allow access to the user's account or server depending on the link the malicious user is trying to get the legitimate user to click.


**Security Requirements:**

**SR11:** Zulip should enforce per-user and per-source rate limits to prevent spamming of notifications.

**SR12:** Zulip should send generic alerts so that the actual messages remain undisclosed and can only be seen in the app itself.

**SR13:** Zulip needs to authenticate the notification sender by requiring a server-to-push-service request to be signed/authenticated.

**SR14:** Users need to verify the senders and make sure they know what they are accessing when clicking on links.

**SR15:** Zulip does provide E2EE but there are limitations noted in their push notification services documentation.

**Personal Reflection:**


## 4) Software issues

![Use-Misuse Diagram](images/UseCaseDiagramTamir.drawio.png)

**Security Requirements:**

**SR16:** Zulip should enforce file permissions so that only the original owner of the file can control who can access the uploaded file; to limit exfiltrating data via attachments.

**SR17:** Zulip should allow administrators to restrict which users can create and post in public streams; to limit sensitive messages from being exposed across the organization.

**SR18:** Zulip should allow administrators to restrict which users can create and receive direct messages; to limit sensitive info being sent to users outside the organization.

**SR19:** Zulip should implement log file downloads so administrators can investigate data exfiltration after the fact.

**SR20:** Zulip should allow authorized administrators to audit messages sent (for example: by sender, recipient, keyword, and time) to investigate data exfiltration through messages.

**Reflection:**
The misuse case analysis produced 5 security requirements targeting a malicious insider exfiltrating data through sending messages and attachments on Zulip. After reviewing Zulip’s documentation, we found 
that Zulip’s advertised features are strongest in access controls. For example, file access is checked per request against who actually received it and admins can restrict who creates or posts 
in channels and who can send direct messages. Zulip does have room for improvement on the auditing side of things, we couldn’t find anything in the documentation about logging file downloads 
that would let organizations investigate a suspected leak after the fact, and audit tools like message export exist but require special authorization rather than being fully self-service. Overall, 
Zulip's security features are sufficient against outsider threats but could improve on their action against insider threats, where prevention alone can't stop someone from misusing access 
they're already entitled to have, and better logging/audit capability would be the most impactful improvement.

**Personal Reflection:**

I thought writing security requirements would be pretty simple, but it turned out to be a lot harder to make them specific enough to actually be useful against real documentation. My original drafts sounded fine on the surface but honestly were too vague, and I had to keep revising until they actually said something worthwhile. The most useful part was going back and forth between use cases and misuse cases until we found a real gap in coverage it showed me that security isn't really a clean "yes" or "no" answer.

## 5) Account issues

image: ![<img width="1196" height="662" alt="diagram5 drawio" src="https://github.com/user-attachments/assets/aab71f63-9b0b-46aa-aa2c-f6d007c4cc52" />

**Actors:**

* Zulip User (user)
* Malicious Zulip User with Standard Account Access (misuser)

**Description of Use Case:**

A Zulip user manages their personal profile information, such as their display name, profile picture, and other available profile fields. Zulip also allows organizations to configure restrictions on certain profile changes and can synchronize profile information through external identity systems such as LDAP/Active Directory.

**Description of Misuse Case:**

A malicious Zulip user with a legitimate standard account attempts to modify another user's profile information without authorization. The misuser's goal is to impersonate or misrepresent another organization member by changing information such as the user's display name, profile picture, or other profile fields. The attacker has normal authenticated Zulip access but is not authorized to modify the targeted user's profile.


**Security Requirements:**

**SR21:** Zulip should verify that a user is authorized to modify the specific profile associated with the account being changed.

**SR22:** Zulip should prevent a user from modifying another user's personal profile information without appropriate authorization.

**SR23:**  Zulip should allow organization/server administrators to restrict user changes to profile information when required by organizational policy. Zulip already provides configuration controls for disabling name and avatar changes.

**SR24:** Zulip should validate profile-update requests so that unauthorized or malformed changes to personal profile information are rejected.

**SR25:**: Zulip should maintain an auditable record of significant profile/account changes so that unauthorized modifications can be investigated after an incident.

**Reflection:**

The misuse case analysis produced five security requirements focused on preventing unauthorized changes to user profile information. After reviewing Zulip's documentation, we found that Zulip provides several controls that address these requirements. Organizations can restrict whether users are allowed to change certain profile information, including names and avatars, which can help prevent unauthorized or unwanted changes to user identities. Zulip can also synchronize profile information from external identity systems such as LDAP/Active Directory, allowing organizations to manage certain profile information through an existing identity system.
However, there are still limitations to consider. Restricting profile changes helps prevent unauthorized modifications, but it does not necessarily prevent a user who already has legitimate access from intentionally providing misleading information when changes are allowed. External identity synchronization can also help maintain consistent profile information, but its effectiveness depends on how the organization configures and manages its identity provider. Overall, Zulip provides useful controls for restricting profile changes, but stronger auditing of profile changes would provide additional support for investigating unauthorized modifications after they occur.

## Overall Reflection of Team:
What did you learn from this assignment? What did you find most useful?
Compile individual team member reflections into a single reflection for the team. 

# Part 2: OSS Project Documentation Review

Improvements or missing features

**Documentation Review:**
One area that could be improved is Zulip’s security setup. The steps to needed to properly set up a Zulip server are spread across several separate pages rather than placed into a single checklist. One can 
find security recommendations or tips in the [installation](https://zulip.readthedocs.io/en/stable/production/install.html), [reverse proxies](https://zulip.readthedocs.io/en/stable/production/reverse-proxies.html), and [monitoring](https://zulip.readthedocs.io/en/stable/production/troubleshooting.html) pages (plus several more). This is a problem because some who wants to start their own Zulip server, could finish 
running the main install script, see the that the installation was complete, and assume they are done without realizing that there are still security recommendations that they still need to set up on other pages.
Another gap is that some warnings don't explain the risk behind them. For example, the docs note that using a self-signed certificate [“isn't suitable for production use”](https://zulip.readthedocs.io/en/latest/production/install.html), but don't say what actually goes wrong 
if you use one anyway, which makes the warning easy to underestimate.
















