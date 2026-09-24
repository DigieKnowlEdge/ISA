---
title: Identify Interactors and Other Systems using CUS Case Study
---

# Identify Interactors and Other Systems using CUS Case Study 

Using the Car Update Service case study, participants should list what actors they identify the external entities such as actors, interactors, 3rd-party-system, and any other relevant out-of-scope-systems to create C4 model level 1 context view.

## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (on session) | 20 - 25 min |
| Timing (self paced) | n/a |

## Objectives

At the end of this exercise, attendee should be able to perform the following:
* Know how to identify actors and interactors from their description.
* Know when an entity is out of scope rather than a part of the system being analyzed.
* Be able to create a C4 level 1 context view from information given.

## Additional Notes

* Which software system is in scope?
* List the users and the other systems that it interacts with the software system.
* Which Systems are out-of-scope?

## Tasks (On Session)

### Identify External Interactors

1. Understand **Sprint 1** of the case study: [Car Update Service - Case Study](cs-01-car-update-service-sprint1.md). 
2. Identify and list the Interactors and External Entities (e.g. ```Car```). 

!!! note
    <details><summary><b> > Click here, to see the solution < </b></summary>
    <ol>
      <li>Car</li>
      <li>Firmware Developer</li>
      <li>Software Developer</li>
      <li>Administrator</li>
      <li>Public Key Infrastructure (PKI)</li>
      <li>MB Git</li>
    </ol>
    </details>


### Create a New ThreatCat Project 

1. Nominate a group member to _open_ [ThreatCat](https://threatcat-training.i.mercedes-benz.com/)
2. Share `screen`/`application` with the group
3. "Create project"
4. Select "without LeanIX / don't sync" (Note: We will address that later in the training)
5. Give the project a name e.g. "Car Update Service - Group A"
6. The rest (contacts & classification) can be kept empty or default
7. Save the project
8. Go to access control and "Add Project User" to add your team colleagues as "admins"

### Create C4 Level 1, Context view, with your group

1. Go back to "Overview"
2. Click on "Create diagram"
3. Give the diagram a name e.g. "Context Diagram"
4. Create C4 Level 1, context view, to show how the list of interactors/entities ***from previous task*** that interact with CUS

!!! note
    You can ignore boundaries for the moment. You can also skip "Protocol" & "Authentication" for path descriptions.

