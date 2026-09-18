# Investigating and Resolving a SentinelOne EDR False-Positive Detection

## Summary
Investigated a SentinelOne EDR alert that quarantined a system due to an 
unsigned application binary, determined it was a false positive through 
hash verification, and resolved it while preventing recurrence across 
the environment.

## Detection
SentinelOne flagged and quarantined a device after detecting an unsigned 
Microsoft 365 ClickToRun binary (a beta release channel build). Unsigned 
binaries are commonly flagged by EDR tools as a heuristic risk indicator, 
since legitimate signed software is the norm and unsigned executables 
are statistically more likely to be malicious.

## Investigation
Rather than accepting the detection at face value or immediately clearing 
it, I investigated to confirm whether the flag was accurate:
- Reviewed the SentinelOne incident details to understand exactly what 
  triggered the quarantine
- Extracted the file's SHA256 hash and cross-referenced it against 
  VirusTotal to independently verify the file's reputation
- Confirmed the hash matched a known, legitimate (if unsigned) beta build 
  of M365 ClickToRun — not malicious code

## Scoping
Before closing the incident, I checked whether other machines in the 
environment were running the same hash/beta version, to determine whether 
this was an isolated event or a broader exposure. Confirmed only the one 
machine was affected.

## Remediation & Prevention
- Reconnected the affected device to the network once the file was 
  confirmed safe
- Created a targeted exclusion in SentinelOne for that specific beta 
  version, to prevent the same false positive from recurring — addressing 
  the root cause rather than just the single incident
- Notified the affected user both when the device was taken offline 
  pending investigation and again once it was resolved and reconnected, 
  keeping them informed throughout

## Skills Demonstrated
EDR alert triage, false-positive vs. true-positive discrimination, 
hash-based threat intelligence lookups (VirusTotal), environment-wide 
scoping, detection tuning/exclusion management, user communication during 
an active incident.
