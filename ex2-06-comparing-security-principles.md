---
title: Comparing Security Principles
---

# Comparing Security Principles

Discuss as a group to consolidate the Security Principles, taking turns to present, and challenge other group answers.

## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (on session) | 20 min |
| Timing (self paced) | 10 min |

## Objectives

At the end of this exercise, attendee should be able to perform the following:
* Describle, explain, and give example of the security principles

## Tasks

### Compare and consolidate the security principles (~20 min)
1. _Discuss_ and _create_ the `Security Principles list` with your group

!!! note
    The Objective: create a consolidated list of security principles, for own reference.


#### [Security Principles by Salzer & Schroeder 1975](https://shostack.org/blog/the-security-principles-of-saltzer-and-schroeder)			
1. **Economy of mechanism:** Keep the design as simple and small as possible.			
2. **Fail-safe defaults:** Base access decisions on permission rather than exclusion.			
3. **Complete mediation:** Every access to every object must be checked for authority.			
4. **Open design:** The design should not be secret. The mechanisms should not depend on the ignorance of potential attackers, but rather on the possession of specific, and more easily protected, keys or passwords.			
5. **Separation of privilege:** Where feasible, a protection mechanism that requires two keys to unlock it is more robust and flexible than one that allows access to the presenter of only a single key.
6. **Least privilege:** Every program and every user of the system should operate using the least set of privileges necessary to complete the job.			
7. **Least common mechanism:** Minimize the amount of mechanism common to more than one user and depended on by all users.			
8. **Psychological acceptability:** It is essential that the human interface be designed for ease of use, so that users routinely and automatically apply the protection mechanisms correctly.			

#### [Top 10 Secure Design Principles](https://cybersecurity.ieee.org/blog/2015/11/13/avoiding-the-top-10-security-flaws/)			
1. Earn or give, but never assume, trust.  
2. Use an authentication mechanism that cannot be tampered with.			
3. Authorize after you authenticate.			
4. Strictly separate data and control instructions, and never process control instructions received from untrusted sources			
5. Define an approach that ensures all data are explictily validated			
6. Use cryptography correctly			
7. Identify sensitive data and how they should be handled			
8. Always consider the users.			
9. Understand how integrating external components changes your attack surface			
10. Be flexible when considering future changes to objects and actors.