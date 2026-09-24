---
title: Finalize Team Security Profile
---

# Finalize Team Security Profile

This exercise will validate findings are properly documented with ThreatCat and all relevant details are added.

## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (on session) | n/a |
| Timing (self paced) | 25 min |

## Objectives

At the end of this exercise, attendee should be able to perform the following:
* Validate ThreatCat findings of CUS
* Finalize a project in ThreatCat

## Tasks

### Discuss Validation with your group (15 min)

1. _Discuss_ and take notes of our findings – Did we do a good job in the previous steps?
> The Objective: Validate the findings

### Edit properties (10 min)

1. Discuss as a group and use `ThreatCat` go to "Overview" and click "Edit properties"
2. Make sure you completed `Project - Edit` with the data from the following transcript:

#### Transcript: CUS Service Info

ISA: Before finalizing the security profile, I need to request all needed service info details. 

Lead Developer: Sure, what exactly do you need?

I: First, I need to know the App-ID in LeanIX

> LD: We do not have an entry in LeanIX yet, please keep it empty for the moment

I: Understood! Which Project name should be used?

> LD: Car Update Service

I: And the Department of Solution as in LeanIX?

> LD: PT/TAS via Global Cyber Security

I: Are you able to share a short description of the system, we can use in out tool?

> LD: Sure; The Car Update Service or CUS is an AWS hosted , web-based service which provides our cars with over the air updates.

I: What is your responsible ISO as in LeanIX

> LD: Oh, this is my dear colleague Casper Knut

I: And who is the technical owner, or its contact person and the primary point of contact?

> LD: The technical owner is Alex Merev and the primary point of contact is Taylor Fizz

I: OK, this is all key info. Just to confirm, the CIA is internal, critical, standard; and the system is internet facing?

> LD: Correct!

I: Fine. So we are done here and I can finalize the Security Profile.

## ThreatCat Submission

!!! warning
    This task may only be executed if you already requested the needed Alice INT entitlements (see [Exercise 2-10](ex2-10-apply-countermeasures.md))


1. Review if all elements are done: 
   1. DFDs (Context, Container, Components)
   1. Threats (all threats have a score and a countermeasure description, at least one threat is mitigated)
   1. Overview - Properties are aligned with the actual project info (Info-Classification, ISO, etc.)
2. Go to "Project Version" and select "Submit"
