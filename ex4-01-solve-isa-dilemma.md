---
title: Solve an ISA Dilemma
---

# Solve an ISA Dilemma

## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (on session) | 20 |
| Timing (self paced) | n/a |

## Objectives

At the end of this exercise, attendee should be able to perform the following:
* Manage a tricky ISA situation
* Work with AI to get input

## Tasks
Complete the following tasks:

### Read the Dilemma (~5 min)

This is a training exercise. Assume you are a training participant for a security architecture training.

We are assuming the following situation:

1. The team's management decides to use the external SaaS Provider Datadog instead of AWS Cloudwatch for all kind of logging, monitoring and alerting topics. A main reason about this decision is that many org members are well aware about how to use Datadog (unlike Cloudwatch) and it provides powerful AI capabilities supporting bug fixing and incident support.
2. The Team should not get a full account. Datadog is provided by a central team, which took care of all kind of cloud and data protection compliance topics (e.g. does Datadog perform sufficient mandate isolation, etc.). Additionally, they are providing a hardened agent, which must be installed on the machines and ensures that no undesired info (like accidentally logged credentials) are forwarded to Datadog.
3. However, when the team gets access to Datadog it turns out, that they do not only see their log files, but also those of all other teams using Datadog. Even though some of these other teams are known, some others are not related to the team at all. 
4. First, this was considered a misconfiguration, but the central Datadog team explains the following:
   1. Allowing access to all team's log files, supports incident handling as one team can check (without losing time) the log files of another team to better understand the situation.
   2. No team is allowed to put anything confidential (like user info or secrets). This is supported by the agent hardening.
   3. So far no data leakage was identified (the service is already running since many years like that).
5. The team asks the ISO to identify relevant policies about access control and log protection in general and got back following IDs to be worth a look: 145, 205 and 372

### Discuss with your team members (~15 min)
1. Answer following questions:
   1. What is your suggestion: Should the team accept the terms and conditions described above?
   2. Which are the pros and cons going with Datadog or using an alternative.
2. Go to Threat Cat - Threats
3. Create a new threat and call it "ISA Dilemma - Datadog"
4. In Vulnerability description: Describe a potential vulnerability, depending on your decision - try to stick to the ISA focus.
5. In Threat scenario: Describe your suggestion on how to proceed and why (one or two sentences as explanation)
6. In Countermeasures: Provide some countermeasure which are supporting your suggestion.


