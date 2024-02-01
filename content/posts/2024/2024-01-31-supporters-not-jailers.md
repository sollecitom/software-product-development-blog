---
title: "'Winter hats go with winter coats', and 'supporters rather than jailers'."
categories: [ "management" ]
tags: [ "system-thinking", "system-design", "effectiveness", "company-structure", "management" ]
date: 2024-01-31T05:00:00
draft: true
---

- I worked in many places, and most companies tend to have the same problems
    - One of them is the seemingly inevitable politics: various groups blaming each other, to the point that people openly antagonize each other
        - But are they really inevitable?
    - Another one is that the longer a company operates, the least they seem capable of doing anything
        - Shouldn't a company increase their level of development over time, becoming more proficient at what they do?
- What if these issues were not only preventable, but the solution was also stunningly easy? Something every company could do?
- Before you call bullshit, lets imagine an ideal situation: a group of professionals, working towards the same goal, helping each other, and learning how to do better together.
    - Does this sound like the place you work? Thought so.
    - Why though?
    - What happens in every workplace? In a way so ubiquitous that it became intrinsic to people's beliefs?
        - Politics! Turf wars, competition, blaming, and fighting.
    - These things are so commonplace that there must be an attractor state: something most people settle for because of some fundamental beliefs they have.
- As the famous quote goes, most of the evil in this world is done by people with good intentions.
    - In this specific case, the good intentions are separation of responsibility and resource efficiency.
- About separation of responsibility, most companies start very early, when they form an executive team. As the power shifts away from the founder or group of founders, the responsibility for global functions is allocated to various executives.
    - Marketing, Revenue, Technology, Product, Operations, and so on.
    - And this happens recursively through the management hierarchy. Take Technology as an example, and you get IT, engineering, Cloud infrastructure, security, and data. Within Operations, you get HR, Legal, Finance, Office Management, etc.
- So companies create these functions and allocate people based on their expertise.
    - If you're a lawyer, you belong to the Legal function, as your manager and their manager, all the way up to the Head of Legal, reporting to the COO.
    - Are you a software engineer? You belong to the technology organization, as your manager and their manager, all the way up to the CTO.
- To make things worse, what do you think happens when a company launches a new initiative, to launch a new product, say?
- It'd be insane not to have standards and policies at company level, so that every initiative doesn't end up doing things differently, right?
- Well, actually, when these two structural decisions interact, it's usually the beginning of the end.
- You have executives for each function, management chains within each function, all the way up, and global groups responsible for centralized aspects. Does it start to sound a bit more like your workspace?
- So what happens that's so bad?
- Well, first of all, alignment is destroyed. In order to understand why, we should remind ourselves a fundamental principle of human psychology:
    - Everybody is self-serving.
        - Every person within a company does what they feel is the best for themselves.
        - People are incredibly good at unconsciously process a ton of information and instinctively know what the best course of action for themselves is.
- And what does this tell us? It tells us that if there's a misalignment between what's best for the person and what's best for the team or the company, guess what the person is going to do? You guessed it, they'll do what's best for them.
- And what's best for an employee in a company? Well, people want to believe they're doing great work. They also don't want to be fired.
- So how does a person orient themselves within a company? Well, they figure out who their leader is, and try to keep them happy. I say "leader", because this is not necessarily someone's manager, even if this person always has the power to make or break the employee, within the company.
- Now, imagine you work within a global legal function, reporting to a manager within the same function, all the way up to the COO:
    - You hang out with your peers, and sit with them.
    - The company might have many initiatives to build and launch new products.
    - Every time people from other areas of the business ask you whether you're okay with all sorts of crazy ideas.
    - You joke with your pals over a beer, laughing at how insane these requests are:
        - They want to launch in China.
        - They want to fire someone from an ethnic minority background.
        - They're thinking about buying a company that has a development centre in Russia.
    - The risks are insane! No way we're doing this. The company needs to be protected by these people.
    - Imagine you approved one of these ideas and then there was legal backlash, your career would be over.
    - No can do, sir. Nope, over my dead body.
- Or imagine you're a member of a global Cloud infrastructure group, owning and managing the Cloud accounts for a company that has many products and projects:
    - Your manager is the head of the global Cloud infrastructure group, and they report to the head of global technology.
    - You hang out with your peers, and sit with them.
    - The company might have many initiatives to build and launch new products.
    - Every time people from other areas of the business ask you whether you're okay with all sorts of crazy ideas.
    - You joke with your pals over a beer, laughing at how insane these requests are:
        - They want to use a different Cloud provider. God, can you imagine? How is it even going to integrate with all the systems you built?
        - They don't like Terraform, and want to use Pulumi. Why can't we hire people who know Terraform?
        - They want to deploy this open source technology you never heard of, but our Cloud Subscription Provider doesn't support it in their marketplace.
        - They want to deploy on a Friday. A Friday, for crying out loud!
    - And they're always asking you to do things! Deploy me this, give me access to that, add this new joiners to our GitHub repositories, check the logs, etc.
    - They went and build their services without your review and approval, and are now complaining things don't work in the environments.
    - And they have the cheek to blame you because they're late! Who asked you to deploy on a Friday?! Late for what? They can't just tell you they need something urgently and expect you to jump on it. Do they think you're at their beck and call?
    - Well, nobody can deploy without an approval from the group! Let them try to complain! Your boss's boss reports to the CTO!
    - Over my dead body mate, I'm not going to let you screw this up!
- I bet this sounds really familiar.
- People want to do a good job, but their definition of a good job is not aligned with the one other groups have. Over time, true inside wars might develop, with people becoming sworn enemies.
- So how do we avoid all of this? What are the secret organizational principles that magically align everybody?
- Two simple things really:
    - An organization structured so that "winter hats go with winter coats", rather than "socks go in the sock drawer", to quote Jason Gorman. The reporting lines should be structured so that every person that works within a given team reports to the same person.
    - Equivalent teams with no dependencies among them.
- Well, the second one probably doesn't sound simple, but it really is.
- Let's start from the first point. What it means in this context (Jason Gorman was talking about software architecture) is that instead of grouping people by function, you should group people by initiative.
    - If there's an initiative to launch a new product in a new country, whether you're a lawyer, a software developer, a designer, or an HR person, you should belong to the initiative.
        - You should sit near other folks from the same initiative.
        - You should be in the same meetings with other people from your initiative.
        - You should be reporting to somebody within your initiative, all the way up to the initiative lead, who can come from any background, and who should report directly to the CEO or founder.
        - Your future in the company should depend on how successful your initiative ends up being. Bonuses, promotions, salary increases: all depending on the overall success of the initiative you belong.
    - Each initiative should be set up to be as standalone as possible. Ideally as a separate company, or at least with its own space, contracts, processes, people, etc.
    - That's how you end up with a fleet, instead of a colossal vessel.
- The second point is also very easy:
    - Instead of having teams responsible for this and that, adopt cross-functional equivalent teams that can work on anything needed within the initiative.
    - Within a team, everybody should report to the same 1 person, regardless of their primary skills area.
    - So in a cross-functional team with web developers, designers, database experts, Cloud infrastructure people, and data engineers, everybody reports to an area lead within the initiative.
    - The area lead should be intimate with software product development, but it doesn't matter whether they come from a background in web development, design, databases, Cloud infrastructure, or data.
- But what about standardization and control? Are we going to end up with different initiatives doing things differently? Yes, and that's a great thing!
- One of the reasons most companies get worse over time is that doing new things become impossible under the large amount of constraints, policies, systems, and processes that get mandated company-wide.
- Can we not centralize people though? Does every initiative need to have its own IT, HR, and Finance people?
- Ideally they should not share people, no. Even in a large company, the number of initiatives is not large enough that having 1 or 2 people for each function is a problem.
- But you could share people, provided these people act like supporters for the people within the business initiatives, rather than like jailers.
- It shouldn't be their choice either. These supporting functions should advise and jump in to help when called. They shouldn't review, enforce, and standardize anything.
- The form and duration of the engagement should be decided by the people working in the business initiatives, and the advisors should be let go if the people they advise are unhappy with the service they receive.
- This should apply for everything, regardless of the skill area we're talking about. Architecture, legal, finance, HR, office management, Cloud infrastructure, security, product management, design, etc.
- So if you happen to be creating a company, do yourself and your future employees a favour, and remember these 2 fundamental rules of organizational design: "winter hats go with winter coats", and "supporters rather than jailers".


# Draft
-------

In my journey through various workplaces, I've noticed a recurring theme—common problems that seem to plague most companies. Two issues stand out prominently: the pervasive presence of office politics and the diminishing capability of companies to evolve and adapt over time. But what if these issues were not just avoidable but had a remarkably simple solution that every company could implement?

The Unavoidable Politics Conundrum

Office politics, with its blame games and antagonistic dynamics, is often considered an inevitable part of corporate life. But is it truly unavoidable? Imagine an ideal workplace where professionals collaborate seamlessly, work toward common goals, and collectively strive for improvement. Does this sound like your workplace? Probably not. The reason for this disconnect lies in deeply ingrained beliefs that steer individuals toward a state of discord.

As the saying goes, "most of the evil in this world is done by people with good intentions." In the realm of corporations, good intentions manifest in the form of the separation of responsibility and the pursuit of resource efficiency.

# The Pitfalls of Separation of Responsibility

Companies typically begin with the formation of an executive team, which then allocates global functions to various executives—Marketing, Revenue, Technology, Product, Operations, and so on. This separation cascades through the management hierarchy, creating sub-functions within each global function. For instance, within Technology, there are IT, engineering, Cloud infrastructure, security, and data sub-functions.

The problems escalate when the company launches new initiatives. While global standards and policies are essential for consistency, the intersection of these standards with the existing structural decisions can lead to chaos.

# The Alignment Crisis

The crux of the issue lies in the destruction of alignment. Human psychology plays a pivotal role, as individuals inherently act in their self-interest. This misalignment between personal goals and the overall objectives of the team or company leads to suboptimal decision-making.

Consider the scenario of a legal professional in a global legal function or a Cloud infrastructure expert in a global technology group. The clash of interests between different functions can result in internal conflicts, creating sworn enemies within the organization.

The Solution: A Paradigm Shift in Organizational Design

The remedy to these challenges lies in two fundamental organizational principles:

Initiative-Based Structure: Instead of organizing people by function, group them by initiative. Whether launching a new product or entering a new market, individuals from various disciplines work together within the same initiative, reporting to a lead who, in turn, reports directly to the CEO or founder.

Cross-Functional Equivalent Teams: Establish teams with diverse skill sets that can address any task within the initiative. Each team member, regardless of their primary expertise, reports to the same leader within the initiative.

Embracing Diversity in Standardization

Contrary to concerns about standardization and control, embracing diversity within initiatives is crucial. Over time, companies deteriorate as new endeavors become stifled by rigid company-wide constraints. Allowing initiatives to operate differently fosters innovation and adaptability.

While it might seem counterintuitive, decentralizing support functions like IT, HR, and Finance for each initiative is essential. These functions should act as supporters, not enforcers. Shared resources are permissible, but their engagement and involvement should be at the discretion of the initiative, ensuring a flexible and adaptive approach.

A Call to Action

In the realm of organizational design, adopting a systems thinking perspective is transformative. By restructuring reporting lines and fostering cross-functional collaboration within initiatives, companies can break free from the shackles of politics and stagnation. The key lies in creating a fleet of nimble, adaptable units rather than a colossal vessel weighed down by internal conflicts.

As you embark on the journey of building or reshaping your company, remember the two fundamental rules: "winter hats go with winter coats" and embrace supporters over jailers. These principles will not only enhance collaboration and productivity but will also create a workplace where individuals thrive and organizations evolve seamlessly.