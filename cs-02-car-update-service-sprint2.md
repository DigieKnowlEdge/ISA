---
title: Case Study - Car Update Service - Sprint 2
---

In this document, the fictitious case study “Car Update Service” is updated. That means that the given architecture is adjusted in some areas and these updates are addressed in this document.

!!! note
    If you need to identify or choose additional cloud services, please use [AWS - Home](https://aws.amazon.com/products)


## Functional Introduction

After an internal audit, the CUS team was tasked to increase the security of the firmware update process. The team decided to introduce an AI-based firmware verification step. Before a new firmware is available for the cars, it must be checked and simulated by an AI model. Only if the AI model approves the firmware, it will be added to the Firmware Storage.

## Technical Implementation

To implement the AI-based firmware verification, the team decided to use [Amazon SageMaker](https://aws.amazon.com/sagemaker/). SageMaker is a fully managed service that provides every developer and data scientist with the ability to build, train, and deploy machine learning (ML) models quickly.

The firmware development team is responsible for training the AI model. The trained model is then made available to the CUS team. The CUS team uses this model to check and simulate the firmware.

The team runs the following tasks to integrate the new AI feature:
1. The CUS Update Form is adjusted. Instead of directly uploading the firmware to the Firmware Storage, it now first sends the firmware to a SageMaker endpoint for verification.
2. A new SageMaker endpoint is created to serve the pre-trained AI model.
3. The CUS Update Form is adjusted to handle the response from the SageMaker endpoint. If the firmware is approved, the CUS Update Form uploads the firmware to the Firmware Storage S3 bucket.
4. If the firmware is rejected, the CUS Update Form will inform the firmware developer about the rejection.

After these updates the team can ensure that only verified firmware is provided to the cars.
