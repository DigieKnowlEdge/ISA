---
title: Conducting your 1st workshop
---

# Conducting your 1st workshop 

The assigned ISA conducted a kick-off workshop session with the CUS Project Lead and Lead Developer. What questions will you ask, if you are the ISA? Read the transcripts of the workshop for useful information to model the architecture of CUS in C4model.

## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (on session) | 10 min |
| Timing (self paced) | 60 min |


## Objectives

At the end of this exercise, attendee should be able to perform the following:
* Using input from project (documents or interview) be able to collect data required to create context and container views.
* Know when an entity is out of scope rather than a part of the system being analyzed.
* Be able to create a context view from information given.
* Describe the important questions to ask during a workshop.

## Additional Notes

What are the user stories of each interactor/entity identified previously?

## Tasks

### Prepare Questions (optional) & Read Transcript (10 min)

1. Discuss the important questions to ask
2. Discuss what questions to Ask the Lead Developer about the important design decisions he/she took, if you are the ISA. Main objective is to gather useful information from the workshop/interview for your C4model.
3. Create a list of the questions that you will ask
4. Compare your questions with the workshop transcript below:

#### Intro and Generic Topics 

ISA: How did you set up the CUS server infrastructure?

Lead Developer (LD): Well, CUS has no classical "servers". It runs on ECS via Fargate and Fargate means, that not we - but AWS - manage the underlying server infrastructure. However, CUS consists of the CUS Business Logic container and the CUS Update Form container. Both are managed via ECS.

I: Please share some insights regarding the networks the various actors are located.

> LD: Sure! The car is easy, it always comes from the internet. The Admin and the Software Developer typically come from the internet as well. Only the Firmware Developer must access the CUS Update Form via the MB Intranet.

I: Understood, and what about the storage solutions? 

> LD: So, the ECS containers use EBS block storages to run their system and store any ephemeral info. The firmware is stored in S3 bucket and the metadata is stored in a DynamoDB database. The most important "metadata" for us is the information for which car model the firmware must be delivered. Additionally, we store the S3 Bucket Object Identification (S3 OID) of the respective firmware. This allows to find the firmware on the S3 Firmware Storage easily.

I: What programming language, operating system and other services are you using?

> LD: We are using the latest Python 3.10 version as our main programming language. Our docker containers use Ubuntu as base image - also here we are using the latest Long-Term Support (LTS) solution. Any other "versions" are controlled by AWS.

I: How does the authentication of these services work?

> LD: All AWS services we are using, use AWS IAM to authenticate against each other. But not only authentication, we have also defined in AWS IAM which service is allowed to contact which other service.

I: Can you make an example?

> LD: Sure, we have defined that the CUS Business Logic container is allowed to access the S3 Firmware Storage, so that it is able to retrieve the firmware requested by the car.

#### Car Requests Firmware Use Case

I: Now, let's talk about the main dataflow coming from the car. How does the car connect to the CUS?

> LD: The car has a build-in routine. This routine regularly connects to the CUS and requests for updates. The connection is established via HTTPS.

I: And the car authenticates via certificates?

> LD: Exactly! During production the car gets injected with secure X.509 certificates and we use these to authenticate the requesting car. Additionally, we check against the PKI, if any car's certificate is on the certificate revocation list.

I: And what if the certificate is hacked?

> LD: Hey, this is not an architecture, but a security question, but ok...first of all these certificates are stored in a Hardware Security Module, so it is not trivial to hack them and even if that would be the case, the corresponding team needs to handle it, which means we are definitely out of scope here. Please do not forget about this!

I: Sure - this comes with the territory :) So, the car's certificate and the PKI are used, but out of scope regarding our assessment. I would suggest to perform another deep-dive session on the CUS Business Logic, as this seems to be the core element for our target of evaluation.

> LD: This is totally right, let's do so.

#### Firmware Developer Uploads Firmware Use Case

I: Let's talk about the Firmware Developer (FD). How does an FD connect to the CUS?

> LD: The FD connects to our service via their browser over https. For that purpose we use the CUS Update Form container on ECS. It can only be reached from an internal MB network via VPN. 

I: Are you using any framework to deliver these services?

> LD: Sure - we are using the python framework Flask to provide the CUS Update Form services. 

I: How does authentication and authorization happen?

> LD: We connected AWS IAM in front of our CUS Update Form. That means an FD is authenticated via AWS IAM which is SSO connected to the MB SSO Global Authentication Service (GAS). We received a list of all relevant FDs and added these users to our "FD AWS IAM" authorization role. If a user has that role it is allowed to access the Update Form and therefore upload firmware. 

I: How is the firmware binary and metadata pushed to the respective datastore?

> LD: First, the CUS Update Form checks if all necessary info is given (i.e. firmware package and corresponding metadata). Then the CUS Update Form will first upload the binary to the S3 Firmware Storage and get the S3 OID. After that, it will push the metadata (including S3 OID) to the Metadata DB.

I: I was informed about a firmware signature - how is that used?

> LD: That is correct. The FDs sign each firmware and attach the signature to the firmware package. So, for us the signature can be handled transparent. However, the car has an option to check if the delivered firmware is valid or if anything was changed between the firmware creation and its delivery. Any further details regarding firmware signing must be requested at the FD-team, we are out of scope here.

I: Understood - based on that information, we will put our main focus initially on the CUS Business Logic and come back to the CUS Update Form later on.

> LD: Fine by me. 

#### Administration

I: Let's talk about the Administrator. What the admin's tasks and how does the authentication work?

> LD: The main task of the admin is to set up the complete AWS cloud environment. The admin is responsible to configure all services (like setting up the S3 bucket, configure the DB and all compute services like ECS, Fargate, etc.) All of these tasks are performed via the AWS management console. The authentication is done via AWS IAM which is connected to the MB SSO global authentication service aka GAS. By default, multi factor authentication is activated.

I: Is the admin also involved when a container needs to be updated or debugged.

> LD: Yes, of course. However, this is not done via the management console but the AWS CLI. 

I: Oh, I would suggest to cover this in another deep dive session.

> LD: Fine!

### Create C2 - Container Diagram (50 min)

Update C1 and create C2 with your group:
1. Update C1 - Context diagram from workshop notes (if needed - e.g. if you did not yet add Github)
2. Duplicate the C1 - Context diagram in the Overview section
3. Add all identified containers as entities and add all needed paths 

!!! note
    You can ignore boundaries for the moment. You can also skip "Protocol" & "Authentication" for path descriptions.

