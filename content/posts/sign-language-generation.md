---
title: "Generating Sign Language"
date: 2023-10-16
description: "I've been working on creating a more accessible space online for the specially abled using AI/ML technologies under my university's Centre of Excellence."
---

I've been working on creating a more accessible space online for the specially abled using AI/ML technologies under my university's Centre of Excellence.

### The What, Why, Who, When and Where
About 5% of our country's population suffers from auditory and speech impairment. Most of the educational content available on the internet caters to the "mainstream" population and **lacks accessibility features** for those with special needs.

![](https://uploads.iasscore.in/image/Persons-with-Disabilities-(Divyangjan)-in-India.jpg#small)

In order to create a friendlier online space for them, we are working on modules which will essentially **translate the content** on internet into a more comprehensible form.  

It is currently WIP and I hope to make more developments, have it deployed on the web by the time I graduate in a few months.

### How?
One of the main modules I'm developing for this project translates English videos to sign language through a series of conversions.  
The translated sign language gestures are acted out by a generated avatar provided by *Virtual Humans Group at UEA, Norwich.*
Say hi to Luna - 
![](https://github-production-user-asset-6210df.s3.amazonaws.com/70942982/275352250-41dea6dc-b87c-4717-96f6-33946727e9eb.png#small "Say hi to Luna")

#### The Technical Details

I'll explain by reverse engineering.

1.  Our avatar, in order to act out the sign language gestures, takes input in the form of SiGML _(Signing Gesture Markup Language)_ which is nothing but an XML describing the location and movements to be performed by the hands and fingers.
2.  SiGML is formed through an interesting character encoding, HamNoSys _(Hamburg Notation System)_, which is a set of unicode characters transcribing our signing gestures.
3.  Currently in our (limited) database, every English word has it's corresponding HamNoSys notation (yes, hash maps🤠).
4.  The next task was to extract text from videos using Automatic Speech Recognition. Another team from my university developed a model to transcribe text from spoken English videos, which we are currently using for our project. However, other tools and libraries (thanking OpenAI for a super accurate Whisper ASR) are viable alternatives.

![](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExMjdoYzhwZ2Frc2lrNGc2eHNlMW9qMm90aDVsNHRmYnQyNmtlb3V1bCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/faBMq582pan7Z2gpY2/giphy.gif#small "Luna signing 'I take a mug'")

## Challenges
Throughout the development process, I have faced several challenges - 

#### Lack of research and development on Indian Sign Language
No HamNoSys notations were found for ISL glosses. The module currently translates to British Sign Language (BSL).

### Limited sign language grammar and vocabulary
* Unlike spoken and written English, sign language does not account for words like 'a', 'an', 'the', 'is', 'am', 'are' et cetera. 
* There's a complex set of grammatical rules to translate English to sign language which needs to be followed for correct translations.
* Words like 'breakfast' and 'daughter' are considered complicated by sign language. No signs exist for these words. They are broken down into 'morning food' and 'girl child' to sign.

#### Avatar is expressionless and cold
No emotions are expressed by the avatar while signing. Honestly, it makes them unpleasant to look at.

#### No way to verify the integrity and accuracy of signs
There's a lack of a process to test and verify how correct the generated signs are.

### Future Scope
Being a research-cum-development project, advancements in sign language and closely working with the concerned authorities will mutually benefit the researchers and developers. For this reason, we are in touch with ISLRTC, GoI to further research and development on Indian Sign Language, with the help of which, we can work on creating a platform to uplift those with special needs and increase accessibility online.