---
title: Identify Trust Boundaries
---

# Identify Trust Boundaries

## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (on session) | 25 - 30 min |
| Timing (self paced) | n/a |

## Objectives:
At the end of this exercise, attendees should be able to perform the following:
* add trusted boundaries to C4model
* verification of solutions by the groups and comparison of solutions, to learn from each other.
  * what went well
  * things that you could have done differently (not so well)

## Additional Notes:
* Authentication usually required between trusted boundaries.
* User authenticates over a Web Browser?
* User is authenticated over user DB?
* User submits Report to Report DB?
* BUT what happens then? – Is there something missing ?

## Tasks

###  Read Transcript (5 min)

1. Read the transcript below:

#### Transcript: Trust Boundaries

I: Let’s start with the car. I assume it is connected to the internet?

> LD: Absolutely!

I: But this does not apply to the various admins and developers, correct?

> LD: That’s also correct. The admin accesses the AWS environment from the internet. The software developer also accesses GitHub from the internet. Only the firmware developer must be inside the corporate intranet to access the upload form.

I: So a VPN is used for that?

> LD: Exactly. Access is only possible via VPN.

I: Are there additional trust boundaries within the AWS environment?

> LD: What exactly do you mean by trust boundaries in this context?

I: A trust boundary exists whenever one component does not inherently trust another component, or when trust must first be established explicitly. This is often reflected in how networks are structured or how IAM roles and permissions are configured.

> LD: Okay. For one thing, we isolate our environment using a so-called VPC. Our ECS cluster runs inside this VPC. By default, the VPC is isolated. However, we configured permissions via AWS IAM so that the containers (e.g., the business logic) can access the respective AWS services (e.g., DynamoDB) without issues.

I: And within the cluster? For example, could the business logic directly access the update form?

> LD: No! Both are located in dedicated subnets. We configured this using the VPC’s security groups. The business logic container runs in the public subnet, where an Internet Gateway is attached, making it accessible from the internet via the Application Load Balancer.

I: And the update form?

> LD: The update form container runs in the so-called private subnet. A VPN gateway is attached there. Accordingly, it is only accessible from the intranet. This means the business logic cannot directly access the update form; the network configuration prevents this.

I: What about the new SageMaker endpoint for firmware verification? Is it also in a private subnet?

> LD: Yes, absolutely. The SageMaker endpoint is deployed in a private subnet and is not accessible from the public internet. The CUS Update Form container communicates with it through a VPC endpoint for SageMaker. This ensures that the firmware verification process is completely internal.

I: That makes sense. But what about other AWS services like S3 and DynamoDB? Are you also using VPC endpoints for them?

> LD: That's a great question. We discussed this topic at length. While VPC endpoints for S3 and DynamoDB would further enhance security by keeping all traffic within the AWS network, we decided against it for now, for a couple of reasons. First, all communication with these services is already encrypted using TLS, so the data is protected in transit. Second, and more importantly, we have seen no data exfiltration attempts from our containers. The containers are purpose-built and have a very limited set of permissions. We are following the principle of least privilege very strictly. Therefore, we decided that the cost and complexity of setting up and managing VPC endpoints for all services is not justified by the minimal additional security benefit in our current setup. 

I: Understood. Are there additional trust boundaries within the business logic itself, i.e., at the component level?

> LD: No. At that level, all components trust each other and can invoke one another without additional authentication.

I: And none of the components run with root privileges?

> LD: Oh, you are right. Even though none of the components we developed require root privileges, the SSM agent (needed for ECS exec) needs root permissions to work as intended.

### Add Trust Boundaries (20 min)

* Go to your groups container diagram. Go to the "Boundaries" section. Create all needed boundaries outside (i.e. MB Intranet) and inside (i.e. any subnets) the target of evaluation. Afterwards review your components as well!
* Assign parent relations as needed

!!! note
    Try to be as complete as possible adding network layers as trust boundaries (e.g. Intranet, Edge DCs, etc.). However, sometimes it may support visualization if you are not adding a "default" boundary (e.g. in many situations it is clear that certain systems are hosted in the internet so you can skip adding it as a trust boundary).


* Validate the Model:

> Can we explain the application based on the DFD without further explanations?
>
> Does the diagram reflect the current or planned reality of the software?
>
> Can we see where all the data goes and who uses it?
>
> Do we see the processes that move data from one data store to another?