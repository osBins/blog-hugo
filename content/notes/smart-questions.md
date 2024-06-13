---
title: "Asking questions the smart way - summarized"
date: 2024-01-09
description: "Summarizing the article 'How To Ask Questions The Smart Way' by Eric S. Raymond and Rick Moen"
---
**[How To Ask Questions The Smart Way](http://www.catb.org/~esr/faqs/smart-questions.html)** is one of my favourite pieces of text related to software development (although the learnings can be extrapolated to other fields too). I adopted it as my Bible back in first semester and have referred it to my friends and juniors in conversations around taking-help a LOT of times ever since.   
I've also gone back to the document to read it again, but would agree to it being lengthy (it is highly recommend as an investment in yourself though).  

I'll thus summarize the text for myself and in case I have to refer it to a friend in need again, this will be the link I'll share.  
(Read the original document if possible, it is a 100% worth the time and covers the nuances and explains different situations with examples for better understanding - [How To Ask Questions The Smart Way](http://www.catb.org/~esr/faqs/smart-questions.html))
### How to ask a good question?
#### Understanding a developer/hacker's persona
The developer community is super helpful to people who have done their homework ask clearly framed, well researched questions where the respondent has to put in minimal effort to help them out. This is due to the fact that everyone is busy with their own responsibilities and would appreciate being asked questions in a way which doesn't feel burdening for them.  
To effectively ask for help, understanding the following is important - 
* What to do before asking a question
* When and where to ask the question
* How to ask the question
* Interpreting the answer  
<br>

#### What to do before asking a question
A Google search or ChatGPT-ing the question beforehand is important. You don't want to offload the entire resolving process to the other person. This goes hand in hand with reading the documentation, `if(FAQ) { consult FAQ }`, Stack Overflow, GitHub issues/PRs. The list is not exhaustive.  
It is a time taking process but it is necessary.
#### When and where to ask the question

The question needs to be directed through the right communication channel. Avoid forums/discussions unrelated to the tools/language/project which pertains to the question. Avoid channels where it would be considered off-topic. Avoid hitting up random people to resolve your query (unless they are a stakeholder of some sort with what you're having a problem with). And do not spam channels with the issue. That is likely to get you ignored/told off/banned.  
Look up the question on the web before posing it to anyone, again.

#### How to ask the question

* Be specific.  
❌ "XYZ doesn't work!" - is a terrible way to get your query resolved. You need to minimize back and forth with the respondent so it is easier for them to answer your question with all the details already present to them.  
✅ "Doing ABC with XYZ version x.y.z gives this error on doing - \<error> on doing PQR. I have tried \<this> and \<that> but the error persists." - crisp, clear, concise.
Follow the "object-deviation" description while describing the problem.  

* Make it easier for the respondent to reply. Do not point them to another communication channel to hit you up to help you resolve your query.  

* Frame the issues in a grammatically correct, properly formatted language.  

* Do not include your guesses with the problem description unless you're sure you've researched well and know what exactly might be causing the issue.  

* Describe the goal, not the step.  

* Request exactly what you want from the respondent - to provide pointers, send code, check the patch or anything else.  

* Generate a small, minimal test case to pose code questions instead of dumping entire blocks of program code.  

* It is risky to flag your question 'urgent'. It might not be urgent for other developers and they'll consider it spam.

* Be courteous, share follow up on figuring out the solution, thank the people who put in efforts

#### Interpreting the answer

Consult the manual or search the web if asked to. Do research on the solution provided before bouncing back for a follow up.  

Interpret rudeness positively, react calmly. Get over it. Don't get into flame wars.

#### Good and bad questions (copied from source)
***Stupid**: Where can I find out stuff about the Foonly Flurbamatic?*  
This question just begs for "STFW" as a reply.  

***Smart**: I used Google to try to find “Foonly Flurbamatic 2600” on the Web, but I got no useful hits. Can I get a pointer to programming information on this device?* 
This one has already STFWed, and sounds like there might be a real problem.  

***Stupid**: I can't get the code from project foo to compile. Why is it broken?*
The querent assumes that somebody else screwed up. Arrogant git...  

***Smart**: The code from project foo doesn't compile under Nulix version 6.2. I've read the FAQ, but it doesn't have anything in it about Nulix-related problems. Here's a transcript of my compilation attempt; is it something I did?*  
The querent has specified the environment, read the FAQ, is showing the error, and is not assuming his problems are someone else's fault. This one might be worth some attention.  

***Stupid**: I'm having problems with my motherboard. Can anybody help?*  
J. Random Hacker's response to this is likely to be “Right. Do you need burping and diapering, too?” followed by a punch of the delete key.  

***Smart**: I tried X, Y, and Z on the S2464 motherboard. When that didn't work, I tried A, B, and C. Note the curious symptom when I tried C. Obviously the florbish is grommicking, but the results aren't what one might expect. What are the usual causes of grommicking on Athlon MP motherboards? Anybody got ideas for more tests I can run to pin down the problem?* 
This person, on the other hand, seems worthy of an answer. He/she has exhibited problem-solving intelligence rather than passively waiting for an answer to drop from on high.


#### Concluding
This summarises the text from [How To Ask Questions The Smart Way](http://www.catb.org/~esr/faqs/smart-questions.html). Again, I would highly recommend going through the original document. I have gone back to it a lot and it feels like a fresh read every time. It's inarguably one of the most important pieces covering nettiquetes for software engineers and I strongly feel that the developer community as a whole would become much warmer and helpful if hackers start following the advices stated here.