---
title: Conducting follow up workshops
---

# Conducting follow up workshops

The assigned ISA conducted follow-up workshop session with the CUS Project Lead and Developers.
Read the transcripts of the workshop for useful information to model the architecture of CUS in C4model.
Use the C4Model method to visualize the Level 3, Components view of a chosen container.

## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (on session) | n/a |
| Timing (self paced) | 60 min |

## Objectives

At the end of this exercise, attendee should be able to perform the following:
* Using input from project (documents or interviews) be able to collect data required to create components view.
* Know the relationship between entity, process, & datastore, and how they communicate.
* Be able to create a components view from information given.

## Additional Notes

Which container should you decompose? What are the components inside? What about the data flows? How is data being processed? How is data being stored? How is data being used?

## Tasks

### Prepare Questions (optional) & Read Transcript (10 min)

1. Discuss the important questions to ask
2. Discuss what questions to Ask the Lead Developer about the important design decisions he/she took, if you are the ISA. Main objective is to gather useful information from the workshop/interview for your C4model.
3. Create a list of the questions that you will ask
4. Compare your questions with the workshop transcript below:

#### CUS Business Logic

ISA: Let's come back to the CUS Business Logic. Could you repeat, how the car connects to the CUS Business Logic to request a firmware update?

Lead Developer: Upon online, the car connects to the CUS. In order to cater these requests, we set up a simple web API which serves as an entry point for the CUS Business Logic.

I: I assume you are again using Flask as a framework and HTTPS as protocol?

> LD: Correct, the CUS Business Logic uses Flask via HTTPS.

I: We already addressed the authentication in our last workshop. Could you please carry on from there - what happens after the car is authenticated?

> LD: After the CUS Business Logic knows that a valid car requests for an update, it connects with the Metadata DB. This is the place, where the CUS Business Logic can identify if there is any delta between the given vs. the desired firmware status.

I: Ok - so, I assume there are two options now?

> LD: Exactly! Either there is no delta and the dataflow ends here. However, if there is any update the CUS Business Logic would identify it in this step.

I: What happens, if the CUS Business Logic identified that the requesting car needs a firmware update?

> LD: The Metadata DB does not only store the info which car needs which firmware, but also the location of the firmware in our Firmware Storage aka the S3 OID. And with this ID, the CUS Business Logic knows where to fetch the necessary firmware from the Firmware Storage.

I: Easy - and the last step is to deliver the firmware package.

> LD: You got it! The final step is to answer the initial request with the needed firmware package. After that the second dataflow is done as well. The complete process restarts as soon as the car routine triggers another update request.

I: All clear now. I think we covered the most important questions. Just to get a better understanding and to avoid any relevant dataflows are missed, I would like to address a couple of additional questions.

> LD: Go ahead.

I: First, what sort of data is provided by the car?

> LD: Besides of the authentication related certificates, the car only shares the least necessary information. In our case it is the model (e.g. C-Class), - if relevant - some further details (e.g. "has feature XYZ") and of course its latest firmware version (which is a non-human readable unique string). With this information the CUS Business Logic can calculate any "firmware delta" and provide relevant packages when needed.

I: Second, what happens if the download is not completed, or fails?

> LD: The car will restart the initially mentioned routine aka try again a little later.

#### Administrator tasks

I: Let's come back to the Administrator. We already talked about the management console. Now let's have a closer look on the debugging use case. I understood the admin is able to log into the containers via SSH - is that correct?

> LD: No! There is no open SSH port on the containers. However, if we have to perform any update or debugging on the ECS containers, the admin uses ECS exec. 

I: I am not familiar with that function - could you please explain, how it works incl. authentication?

> LD: First, the admin needs to use the AWS CLI, instead of the management console. However, just like via the console, the admin needs to authenticate via the AWS IAM account. Afterwards it is possible to run a so-called "aws ecs execute-command", e.g. "apt-get update" in order to receive all available updates for the operation system - just like with SSH, but without opening any SSH ports.

I: Understood - but there must be something "waiting for" or receiving these command within the containers, right?

> LD: Yes, we need to install the so-called AWS Systems Manager (SSM) Agent on our containers. The necessary packages are provided by Amazon, we just need to ensure they are running on our containers. If that is the case, the admin can run all necessary commands on them.

I: Are those administrative tasks all tracked?

> LD: We use AWS Cloudtrail with default settings - I hope that answers your question.

I: I will try to find out and will keep you posted - thank you for the moment.

### Create C3 - Component Diagram (50 min)

Update C2 and create C3 with your group:
1. Update C2 - Container diagram from workshop notes (if needed - e.g. if you did not yet add AWS ECR)
2. Create a new diagram and name it "Component Diagram"
3. Copy all needed containers as entities and **add** all needed components (as entities) and their interfaces (as paths)
4. Discuss if anything is missing or still unclear and take notes of **questions to ask the project** in the next meeting/workshop to help complete C2 & C3

!!! note
    As the component diagram is a "zoom-in" on the Business Logic container - it would be too much noise copying the whole container diagram. Thus we need to copy all needed entities first; i.e. all entities which have a path into or from the business logic server on the container view - must be manually copied first.


!!! note
    You can ignore boundaries for the moment. You can also skip "Protocol" & "Authentication" for path descriptions.

