# Detecting and Responding to an Adversary-in-the-Middle (AITM) Phishing Attack

## Summary
While monitoring security alerts, I identified and remediated an active 
Adversary-in-the-Middle (AITM) phishing attack against a user account, 
using log correlation across Microsoft Defender and Exchange to confirm 
compromise and contain it before further damage occurred.

## Detection
Microsoft Defender flagged a sign-in as a suspected AITM attack at 
approximately 8:14 AM. Rather than treating the alert at face value, I 
cross-referenced the detection timestamp against Exchange sign-in logs to 
independently verify the activity.

## Investigation
The sign-in logs showed a login attempt originating from a geographic 
location inconsistent with the user's normal pattern, occurring at the 
same time as the Defender alert — strong corroborating evidence the 
account had been compromised. I also observed recurring login activity 
after the initial event, suggesting the attacker retained access rather 
than a one-off attempt.

To scope the potential impact, I extended the investigation beyond the 
initial alert:
- Reviewed mailbox rules and forwarding settings to determine whether any 
  data had been redirected outside the organization
- Checked the account for unauthorized MFA method additions and OAuth 
  application grants, to rule out persistence mechanisms attackers 
  commonly use after an AITM compromise

## Remediation
Once compromise was confirmed, I revoked the user's active sign-in tokens 
and forced a password reset, cutting off the attacker's session-based 
access immediately.

## Follow-Up & Validation
Rather than closing the case at remediation, I monitored the account for 
roughly 72 hours following the incident and performed a final check the 
following week to confirm no further unauthorized access occurred — 
validating that containment was fully effective, not just assumed.

## Skills Demonstrated
Log correlation across multiple security tools, AITM/phishing attack 
patterns, incident scoping, token/credential remediation, persistence-
mechanism awareness (OAuth/MFA abuse), structured follow-up validation.
