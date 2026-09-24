---
title: Sprint 2, DFD Validation, Path Authentication
---

# Sprint 2, DFD Validation, Path Authentication

In Sprint 2, more functions and features are being added to improve the security and quality of the products.

An AI-based firmware verification step is integrated to ensure that only approved firmware is uploaded to the firmware storage.

Update and Validate the Dataflow Diagram for our case study "Car Update Service” Sprint 2, that represents the system architecture.

## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (on session) | 15 min |
| Timing (self paced) | 50 min |

## Objectives:
At the end of this exercise, attendee should be able to perform the following:
* update and validate the C4/DFD.

## Additional Notes:
What are the changes to Sprint 2? Does the new security control in place create new problems?

## Tasks

### Prepare follow-up workshop with project team (~15 min)

1. Understand **Sprint 2** of the case study: [CUS - Case Study - Sprint 2](cs-02-car-update-service-sprint2.md). 
2. Discuss and take notes of **questions to ask the project** in the next meeting/workshop to help complete C1, C2 & C3 (e.g. "what is the information classification?")
3. Each group will (as ISA) ask questions to the `Developers` (role played by Instructor) regarding the new architecture (Sprint 2)
4. For further details consider the transcript below:

#### Transcript: AI-based Firmware Verification

ISA: Thank you for providing the documentation for Sprint 2. However, can you walk us through how the new AI-based firmware verification works?

Lead Developer: Sure. When a firmware developer uploads a new firmware via the CUS Update Form, we don't store it directly in the Firmware Storage anymore. Instead, we first send it to an AI model for verification.

I: Interesting. Can you tell me more about this AI model?

> LD: The model itself is developed and trained by a dedicated team of data scientists. We just use it. We deployed the model using Amazon SageMaker, which provides us with a simple REST endpoint to interact with the model.

I: So the CUS Update Form calls this SageMaker endpoint?

> LD: Exactly. The CUS Update Form sends the firmware to the SageMaker endpoint. The model then runs a series of checks and simulations. This can take a while, so the call is asynchronous. Once the verification is complete, SageMaker sends a notification to our CUS Update Form with the result.

I: And what happens then?

> LD: If the firmware is approved by the AI model, the CUS Update Form proceeds to upload the firmware to the S3 Firmware Storage. The rest of the process is the same as before. If the firmware is rejected, the firmware developer is notified and the firmware is discarded.

I: How does the authentication between the CUS Update Form and the SageMaker endpoint work?

> LD: We use AWS IAM roles for that. The CUS Update Form container has an IAM role that grants it permission to invoke the SageMaker endpoint.

I: What about the security of the model itself?

> LD: The model is managed by the SageMaker service, which includes security features to protect the model from unauthorized access. We have also configured the endpoint to be in a private VPC, so it's not exposed to the public internet.

I: So the new data flow is: Firmware Developer -> CUS Update Form -> SageMaker Endpoint -> CUS Update Form -> Firmware Storage.

> LD: Correct. This new step ensures that only verified and safe firmware is stored and eventually delivered to the cars.

I: All clear now. Thank you for the explanation.


## Update C4/DFD according to Sprint 2 with your group (~30 min)

1. _Update_ `C1`, `C2`, and `C3` from workshop notes
2. Validate your `C4`/`DFD`

## Add Path Authentication & Description (~20 min)

1. Go to your group's container diagram (hint: for context there is no need to add authentication, if all interfaces are shown on container too)
2.  Go to the "Paths" section of your C2 container diagram (C3 components is optional for training purposes)
3. Review each path and add an authentication mean (i.e. certificate)
4. As a "Description" add the authentication mean's storage or location if relevant (i.e. HSM, Local Storage, etc.)
