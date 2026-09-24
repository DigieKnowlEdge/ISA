---
title: Case Study - Car Update Service - Sprint 1
---

In this document, the fictitious case study “Car Update Service” is described. The case study will be used throughout the ISA training during various lab exercises.

!!! note
    If you need to identify or choose additional cloud services, please use [AWS - Home](https://aws.amazon.com/products)


## Short Description

We want to use the "Car Update Service" (CUS) to provide all cars the necessary firmware via an AWS cloud environment. In order to achieve that, the car initially needs to reach out to the cloud environment and afterwards receives all necessary firmware packets. You can imagine CUS as the postal service: We are only responsible to deliver the packages from the firmware development side to the car. That's it :)

## Functional requirements

In order to receive an update, the car is configured in a way to regularly request for such an update. Therefore the CUS must provide an interface where such requests can be received. 

Before performing any next steps, the CUS must check if the initially received request comes from a legitimate resource.

If the request is legitimate, the CUS must determine if the car needs an update and if multiple updates are necessary in which order they need to be provided. In order to do so, the car needs to provide its latest metadata (e.g. car model and latest firmware version). Based on this information the CUS derives which firmware is necessary to be provided. 

Finally, the CUS retrieves the necessary firmware packages and provides these back to the car.

Additionally, the CUS needs to allow firmware developers to upload new firmware packages and manage the corresponding metadata (e.g. which car model needs a given firmware). This is achieved via a simple Update Form. The form is provided as a graphical user interface allowing firmware developers to select the firmware they want to upload and directly attach all necessary metadata. 

## Infrastructure & Staging

In order to provide the functions described above, the CUS uses a containerized environment. The control plane is [Amazon Elastic Container Service (ECS)](https://aws.amazon.com/ecs/) and in order to keep management overhead on a small feet [AWS Fargate](https://aws.amazon.com/fargate) is used (a serverless compute engine). 

Currently, there are two containers in use:

* CUS Business Logic (at least two instances)
* CUS Update Form (only one instance)

Both containers use the latest Ubuntu LTS as a base image.

In order to handle incoming load accordingly the CUS Business Logic is able to auto-scale (i.e. as many instances can be added as needed to cover the given load).

Besides of the productive "PROD" environment, there is a parallel "INT" environment for integration and testing. The INT environment does not use productive data but its own test data and test accounts.

### CUS Business Logic

Provides an API for the car, checks for necessary updates and delivers the update. The API and the logic behind is written in the python framework Flask.

### CUS Update Form

Provides a frontend for the firmware developer to upload new firmware. The solution runs on Flask as well and simply provides all necessary input fields to allow firmware developers to upload their software.

## Network

The environment runs on a single [Virtual Private Cloud (VPC)](https://aws.amazon.com/vpc/). However, the CUS Business Logic can be reached from the internet (via an internet gateway), whilst the CUS Update Form can only be reached from the MB Intranet (via the MB VPN gateway). 

In order to allow internet traffic to get on the ECS environment the public containers use an Application Load Balancer (ALB) which is able to handle auto-scaling ECS containers.

Besides of the productive VPC, there is a parallel INT VPC to run the integration tests.

## Database

The application stores all metadata (e.g. which car model need which firmware) in [Dynamo DB](https://aws.amazon.com/dynamodb/) aka "Metadata DB". Besides of the firmware's metadata, the database also stores the location of the stored firmware. 

## Storage

The containers use [Amazon EBS (Elastic Block Storage)](https://aws.amazon.com/ebs/) as their persistence layer.

The firmware is stored in an [Amazon S3 (Simple Storage Service)](https://aws.amazon.com/s3/) object storage in a dedicated bucket aka "Firmware Storage".

Any other relevant files (e.g. log files) are stored in a another S3 bucket (called "Internal Storage") which can only be accessed by the admin.

## Development, Test & Deployment

The code for the containers is developed by software developers and version controlled via the MB Github Enterprise. The main branch is protected and each update needs to be reviewed by another software developer. 

Tests are performed locally and on the INT environment. As soon as all tests have been passed successfully, the Admin builds a docker image and pushs it manually to the [Amazon ECR (Elastic Container Registry)](https://aws.amazon.com/ecr/). Finally, the containers are automatically deployed to ECS and provide their services.

## Administration

All changes on AWS are performed by the CUS administrator (admin). That means that the admin sets up all necessary services via the AWS Management Console (e.g. ECS, ECR, S3, etc.). However, in order to patch or debug a running ECS container, the admin uses [ECS exec](https://aws.amazon.com/de/blogs/containers/new-using-amazon-ecs-exec-access-your-containers-fargate-ec2/).

## Authentication

* The cars are authenticated via a build-in X.509 certificate (see External Dependencies)
* The software developers are authenticating using a Personal Access Token created via MB Github Enterprise
* The admin is authenticated via AWS IAM (which is SSO-connected to GAS as well incl. MFA). 
* The firmware developers are authenticated via AWS IAM too.

## Encryption & Signing

Regarding cryptography, there are two categories which need to be separated: 

### Platform Encryption

In order to protect the application and its users' data, secure communication using TLS (1.2 or higher) is enforced on all interfaces. All storages and the database uses state of the art encryption too. All relevant certificates, are provided by AWS. 

### Firmware Signing

The firmware itself is not encrypted, but digitally signed. That means the firmware developers are signing the firmware with a digital signature. The signature is part of the firmware package uploaded by the firmware developer and can be used by the car to check the authenticity and integrity of the firmware. 

## External Dependencies

In order to allow the CUS Business Logic to check incoming requests regarding their authenticity, the car digitally signs each message. Just like with all other digital signatures used by Mercedes-Benz, the CUS Business Logic contacts the MB Public Key Infrastructure (PKI) to check if the certificate is valid.

## Important Notes

* The car's certificate is installed and stored securely within the car. This certificate can be assumed to be very secure and used for various purposes (not only CUS) and is not under the control of the CUS team.
* The department responsible for firmware development made sure that each firmware is tested to be secure for the car. CUS on the other hand has no options to check, if any received firmware is dangerous for any car (see postal service explanation above)
* All relevant dependencies and systems have been checked for updates and freshly patched
* [AWS Cloudwatch](https://aws.amazon.com/cloudwatch/) is activated for AWS ECS as a monitoring service in order to collect, view, and analyze logs and metrics of the ECS environment (_Hint: You can add Cloudwatch (and other supplying cloud services) in your DFD. However, please focus on the main dataflow first!_) 

