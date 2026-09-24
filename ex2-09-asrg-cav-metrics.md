---
title: Use ASRG to find CAV & provide all Metrics to Prioritize
---

# Use ASRG to find CAV & provide all Metrics to Prioritize

Using security controls such as ASRG to find security flaws in the system and input parameters to calculate the technical vulnerability rating.

## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (on session) | 20 min |
| Timing (self paced) | 30 min |

## Objectives

At the end of this exercise, attendee should be able to perform the following:
* Find CAV(s) using ASRG
* Calculate CAV Rating and Prioritize

## Additional Notes

What are the rating of your finding? If it is low, try look for medium or high finding.

## Tasks

### Add Base Metrics (20 min)

1. _Discuss_ as a group and use `ThreatCat` to _update_ all relevant Base Metrics.
2. _Compare_ the rating of your Mattermost entry with the ThreatCat calculated rating. If they are completely different, investigate further what may be the reason (e.g. your initial assumption was wrong or you picked the wrong metrics in ThreatCat).

!!! note
    Refer to the info icon on each metric for more information. If any entity outside the CUS (e.g. Any other Github repo or any other PKI user) is affected by a threat, you also have to evaluate the "Subsequent System Impact Metrics" otherwise simply leave it as "None". As the car is in the scope, it would not be considered a subsequent system.



### Solve ASRG Exercise (30 min)

1. _Read_ the workshop transcript below

#### Transcripts for potential input validation issue:

ISA: I understand that we might have issue related to the most common web application security
weakness, from OWASP top 10, could someone tell me more about it?

> Lead Developer: I suspect we might have Injection flaws, have failure to properly validate input coming from developer during the firmware upload, if an attacker inject malicious commands into the databases during the upload.   

> Developer 1 (the experienced one): in my opinion, SQL injection is not possible. unlike relational databases, DynamoDB is NoSQL databases don't use a common query language.

> Developer 2: Any MB employee could have access to the form upload server via VPN VPC. But only authenticated user with AWS IAM role is able to upload firmware binary and related
metadata

> LD: yes, we would appreciate any support on implementing input validation controls

ISA: We could check related security control with our new ASRG project on GIT. The ASRG fork from OWASP Application Security Requirements Standard (ASVS) defines three
security assurance levels, with each level increasing in depth. For example by achieving ASRG Level 1 (Basic) could adequately defends against application security
vulnerabilities that are easy to discover, and included in the OWASP Top 10.

> ALL: Awesome, could you show us how?

ISA: Sure, let me show you.

2. Read further info about [Using the ASRG](https://pages.i.mercedes-benz.com/isa/ASRG/docs/0x03-Using-ASRG/)
3. Use the GIT Search Function (or other alternatives) to search for "input validation" or "validate input" 
4. _Discuss_ if the CAV is applicable to CUS. If not, repeat from step 1 with other words
5. Update Base Metrics in ThreatCat



