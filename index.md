---
title: Prework
---

!!! note
    Attendee are strongly recommended to complete the following Prework before beginning the ISA Training, to ensure you are prepared to complete all the modules.



## Metadata

| Property | Details |
|-|-|
| Setup | Group Exercise |
| Timing (self paced) | 240 min |

## Objectives:
Upon completion, attendee should be able to perform the following:

* Prepared to join classroom and ensure learning tools are available
* Understand how to use the C4 Model for Software Architecture
* Understand C4 Modeling Basics
* Create a simple C4-model using ThreatCat

## Tasks

### Get it started

1. Read and complete the instructions in the Welcome Email (~5 min)
2. Download & Install MS Teams client (if not already done)

!!! warning
    You need a CD account (not a supplier- or dealer- account!) to be prepared for Mercedes-Benz SSO login, and you need the PingID mobile- or desktop app for multifactor authentication .


!!! note
    If you are External and do not already have an MB Account, we will create an account for you (please check your inbox). You need to activate the account (aka set a password) in order to proceed with the authentication. You will be prompted for MFA, just follow the MFA setup instructions to Register your new External Account’s PingID, which include downloading pingID app to your IOS or Android phone: [More Details](https://login.mercedes-benz.com/password/mfa/guide/).


### Mattermost

1. Reach out to [Mattermost](https://matter.i.mercedes-benz.com/mercedes-benz/channels/town-square) and log in via SSO. 
2. Send a **Direct Message** to the ISA Training private Channel Administrators (@vicente.yueh and/or @jtschoe).

!!! warning
    If you get error for mattermost access, please open a new issue to get support: [Mattermost Github Space](https://mercedes-benz.ghe.com/mb-home/MBRDI-Mattermost_Mattermost-Support/issues/new/choose). If you do not have access to Github, send a mail to [mattermostsupport@mercedes-benz.com](mailto:mattermostsupport@mercedes-benz.com). In case of any SSO issue, please contact [isa@mercedes-benz.com](mailto:isa@mercedes-benz.com)


![How to send a direct message in Mattermost](./assets/isa_training_mattermost_direct_message_cheatsheet.png){ width="80%" }

!!! note
    Instructor(s) may not be able to respond to your request immediately, so please proceed with the rest of the exercises and it should be ready by then :)  


### C4 Modeling Exercise

!!! note
    The prework consists of two parts: One is the theoretical lesson which covers the basics around C4 Modeling at Mercedes Benz and the second part is the actual exercise around a fictional software solution. If you are well aware about C4 Modeling you can skip the first part and directly start with the exercise.


#### ThreatCat

1. Go to the Training Environment of [ThreatCat](https://threatcat-training.i.mercedes-benz.com/) and sign in for the first time. 
2. After successful login, there should already wait a project for you called "Race Track Pro - Newsletter (Prework)". 
3. If not already done, please rename the project to contain your firstname (e.g. "Race Track Pro - Newsletter (Prework) - John")

!!! note
    The ThreatCat Training environment uses the so-called INT SSO. If you never used it before it may be necessary to register an MFA device (you can use the same as you use normally). Further Details can be discovered here: [Login-Int](https://login-int.mercedes-benz.com/password/mfa). If you are totally stuck, please contact the Support:  	cuhd_support_MFA-PingID@mercedes-benz.com or +49 (711) 17-25005


#### Video Series

1. Checkout the [MB video series about C4 modeling](c4-modeling-intro.md)
2. If you prefer reading the slides (not suggested!), go here: [Lesson0-1_video.pdf](assets/Lesson0-1_video.pdf).

#### Practical example

1. Read the Architecture Description of the C4 Modeling exercise about the RaceTrackPro - Newsletter application, by reaching out to [RTP-Newsletter-Architecture.pdf](./assets/RTP-Newsletter-Architecture.pdf).
2. Go back to the Training Environment of [ThreatCat](https://threatcat-training.i.mercedes-benz.com/) and open the project ```Race Track Pro - Newsletter (Prework) - Exercise```. Next, simply start by filling in all "??" fields in ALL three provided diagrams (Context, Container, Components). However - be aware - some dataflows, and probably even actors, **MAY** not even appear on the cheat sheet and **MUST** be added by you, based on the Architecture Description!!

!!! warning
    If the project does not yet exist, inform the instructors via mattermost (read the instruction in the meantime).


!!! note
    In most cases you only need to provide a label when the label field is marked with ```??```. However, in some cases (i.e. technical solution, e.g. on container level) you are also required to provide a technical description. The technical description should explain what technical solution a container or component is running on (e.g. ```S3``` or ```AWS ECS``` ).


#### Final steps

1. Inform the instructor via Mattermost about the completion of your DFD.
2. Create a Mattermost entry covering your learning objectives, by copying the template below (you are welcome to add your own objectives) and share them on the private [ISA Training Channel](https://matter.i.mercedes-benz.com/mercedes-benz/channels/isa-training).


```
My learning objectives are to:

* learn more about Threat Modeling
* learn more about Cloud Security
* create Security Profile in ThreatCat
* pass ISA exam
* ...
```
Now you are done with all preparations - well done! :)

