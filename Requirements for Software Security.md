# Part 1: Requirements for Software Security Engineering 

## 1) Use Case - Admin Manges users' permissions and access 

image: 

**Actors:**
* Authorized Administrator (User)
* Ex-employees, Privilige seeking external actor (misuer)

**Description of Use Case:**

The user (an organization administrator) manages team members permissions and access on Zulip. 
The admin user roles, adds, or removes users from groups, and deactivates or reactviattes accounts as needed. 
These features help the organization control who can access their team commmunications channels and what actions they can perform. 

**Description of Misuse Case:**
A hacker steals team members credentials to attempt unauthorized actions in Zulip, such as gaining admin priviliges, 
changing group membership, or deactivating and reactiviating accounts. A terninated or disgruntltes emplyees may also attempt to reuse existing sessions or credentials after they have ben deactivated.

**Security Requirements:**

**SR1:** Revoke sessions and reject authenticated requests when account is deactivated and or inactive.

**SR2:** Restrict account activation/deactivation to authorized admins.

**SR3:** Log and audit all acount activity for non-repudiation purposes.

**SR4:** Restrict role changes by accounts without administartor priviliges.

**SR5:** Enforce group member permissions.

## 2) Use Case - Authenicate User

image: 

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

image: ![Notifications Use/Misuse Case Diagram](images/use_case_diagram.pdf)

Actors:
* Zulip User (user), Zulip mobile app, Zulip server/mobile push notification service
* User with access to a compromised server (misuser)

**Description of Use Case:**
A user wants to be notified on their phone appropriately whenever they are tagged or miss a message in their Zulip server. The user expects this notification to be coming from a trusted source and with reliable intel.
If the user is receiving a private message, they expect that it is only sent to them and no one else can access the contents.

**Description of Misuse Case:**
A malicious user wants to send malicious or fake notifications to users to get a user to click on a malicious link or spam a legitimate user with unwanted notifications.
Doing this would cause unwanted resource usage for the user's mobile device or if enough messages are sent a Denial of Service attack. 
This could also allow access to the user's account or server depending on the link the malicious user is trying to get the legitimate user to click.


Security Requirements:

**SR11:** Zulip should enforce per-user and per-source rate limits to prevent spamming of notifications.

**SR12:** Zulip should send generic alerts so that the actual messages remain undisclosed and can only be seen in the app itself.

**SR13:** Zulip needs to authenticate the notification sender by requiring a server-to-push-service request to be signed/authenticated.

**SR14:** Users need to verify the senders and make sure they know what they are accessing when clicking on links.

**SR15:** Zulip does provide E2EE but there are limitations noted in their push notification services documentation.

Personal Reflection:


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


## 5) Account issues

## Overall Reflection of Team:
What did you learn from this assignment? What did you find most useful?
Compile individual team member reflections into a single reflection for the team. 

# Part 2: OSS Project Documentation Review

Improvements or missing features

**Documentation Review:**
One area that could be improved is Zulip’s security setup. The steps to needed to properly set up a Zulip server are spread across several separate pages rather than placed into a single checklist. One can 
find security recommendations or tips in the installation, reverse proxies, and monitoring pages (plus several more). This is a problem because some who wants to start their own Zulip server, could finish 
running the main install script, see the that the installation was complete, and assume they are done without realizing that there are still security recommendations that they still need to set up on other pages.
Another gap is that some warnings don't explain the risk behind them. For example, the docs note that using a self-signed certificate “isn't suitable for production use”, but don't say what actually goes wrong 
if you use one anyway, which makes the warning easy to underestimate.
















