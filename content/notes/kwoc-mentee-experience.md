---
title: "KWoC'21 Project Mentee Experience"
date: 2021-01-07T16:52:35+05:30
description: "Kharagpur Winter of Code is an initiative by IIT Kharagpur’s Open Source Society (KOSS) for students with little to no experience (such as myself) in open source software development."
---
[Kharagpur Winter of Code (KWoC)](https://kwoc.kossiitkgp.org/) is an initiative by IIT Kharagpur’s Open Source Society (KOSS) for students with little to no experience (such as myself) in open source software development.

It aims to introduce students to the working of one of the most popular version control systems - Git. KWoC helps flatten the learning curve and allows students to prepare further for prestigious open source programs like Google Summer of Code (GSoC), Outreachy, Season of KDE, GNOME Internship program and others.

<br>

---

<br>

### How did I hear about KWoC?
I learnt about Open Source for the first time during my college’s orientation. The idea of contributing to development of code which is publicly available and for everyone to use appealed to me. So I, a curious (yet clueless) first-year joined the Open Source Developers Community (OSDC) of my college. Initially, the level of discussions which used to take place within the hub was overwhelming since I had no prior experience in either open source or coding whatsoever. However, we have extremely helpful seniors, who are there to help bridge the gap for us. On November 27, 2020, they told us about the beginner-friendly open source program, KWoC, and encouraged us to register as it would be a great learning experience for us.


### How did I choose my first ever open source project?
Initially, I had decided to choose a project, and then contribute to its documentation because I believed that was the only thing I was capable of at that time. However, after going through ~20 projects, their READMEs and list of open issues, I realized I can do more than just documentation changes if I push myself.

I ended up choosing this cute project MarvellOS by (mentor) akshgpt7, who also happens to be my senior in college. (But I swear I found this out after choosing the project). There was a code-formatting issue which piqued my interest. I believed that formatting code would be a great start for me.

### What’s MarvellOS?
MarvellOS is a basic operating system mock-up made from the Python GUI module Tkinter. It has a few interactive applications to navigate through.  
<br>
{{<figure src="https://user-images.githubusercontent.com/70942982/167294179-e6b1c881-2253-4389-b90a-93e9f3badeaa.png" class="center-image">}}
{{<figure src="https://user-images.githubusercontent.com/70942982/167294196-e325ad73-9e58-445e-b696-b19a036b6267.png" class="center-image">}}

<br>

### What was my contribution?
When we launch MarvellOS, we are greeted by a lock-screen. The documentation mentioned that the password for first-time use was ‘0000’. I typed in the password and hit Enter, but nothing happened.

As it turns out, in order to successfully enter the password, we had to click the ‘Confirm’ button, since the ‘Enter’ key was not bound to submit an input.

Naturally, the first thing I did was to tell my mentor about this. I was asked to open an issue for this on GitHub for this ‘Enter’ key problem.

Thus, my first successful contribution to the project was finding and creating an issue.
<br><br>
{{<figure class="center-image" src="https://user-images.githubusercontent.com/70942982/167294369-bf95ae8e-246e-4cfb-93cb-130e9fb2ec51.png">}}

Next, I went to the issue I had decided to work on, and commented “Hi, I would like to work on this issue.”

The first thing I did here was to run flake8 on the main code file for MarvellOS. Flake8 is a linting tool which checks for PEP8 violations in code style.

{{<figure class="center-image" src="https://user-images.githubusercontent.com/70942982/167294490-abaac741-3bdf-4b87-8103-63dbe1f11e5e.png">}}

<br>
As of then, the code did not conform to PEP8 Style Guide for Python Code. There were missing whitespaces around operators, exceeding line lengths, modules not being imported the right way and a few other violations. All violations added up to more than 250 in number. This was slightly demotivating for the previously motivated me. However, my mentor was helpful and he told me about ‘black’, which is a code-formatting tool for python, that enforces code conforming to PEP8.

So I ran ‘black’ on the code as well, and it fixed the minor errors like whitespaces, line lengths, and a few others. But flake8 still showed a lot of violations in the code.

However, as I was short on time and needed at least one commit to clear the mid-evaluations, I requested my mentor to pull the changes I made to the code, and then I took a break.

After about a week of studying and taking my end semester exams, I got back to rectifying the issue I was working on. I copy-pasted every remaining violation individually on Google, tried to understand the causes of the violations, and then looked up their fixes. I kept regular communication with my mentor so I could clarify things I did not understand. After a week or so of rigorous communication and code formatting, I was finally done with the issue. I created a pull request, and my mentor requested a few changes which I had previously overlooked. I committed the required changes within a span of two days, and the code was almost ready to merge. However, that is when I realized that my code-formatting broke the clock feature in MarvellOS.

The clock which was previously automatically updating on all screens to sync with the machine’s time, stopped updating on the home screen. My mentor and I racked our brains looking at the code, trying to figure out what went wrong, but nothing came to our mind. After about three days, when I was comparing my code with the upstream repository’s code, I noticed an extra indentation, which I undid, and the clock started working again!  
<br>
{{<figure class="center-image" src="https://user-images.githubusercontent.com/70942982/167294548-1d08b2ea-a152-4aca-99f9-778df30db9e5.png">}}

<br>
There is still one violation which shows up when I run flake8 on the code, but even after hours and days of trying to understand what this is and how I can fix it, nothing about it makes sense to me. After discussing this violation with my mentor we decided to let it be for the time being and to resolve it after the coding period for KWoC ends.

### Final words
My experience with Kharagpur Winter of Code has been great. It is beginner friendly and the mentors are really helpful. I am thankful to my mentor for being the friend and the teacher I needed to help me get familiar with Open Source.

I look forward to becoming a frequent Open Source contributor, and expanding the horizons of my knowledge through working on real issues.

---

This article was originally posted on Medium [here](https://arpitjain-23306.medium.com/osbins-kharagpur-winter-of-code-report-2e65959811b5)

