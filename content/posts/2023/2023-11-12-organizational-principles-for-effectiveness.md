---
title: "Organizational principles for effective software product development"
categories: [ "management" ]
tags: [ "system-thinking", "management", "effectiveness", "startups", "organization-design" ]
date: 2023-11-12T05:00:00
draft: true
---

I often discuss what's wrong with an approach, practice, or system. Today, for a change, I want to clarify some principles that an effective software product development company should adopt.

Why principles? Wouldn't a detailed description of how things should work be more useful?

It'd be almost impossible to write, as it's a colossal task. Perhaps it'd be good for a book, but definitely not for a blog post.

Also, reality is multifaceted and nuanced. Everything depends on everything. Prescriptive approaches cope poorly with dynamic situations. Principles, on the other hand, allow you to deal with uncertainty, and guide your decision-making by cutting out the noise.

# How to use these principles

You can use these principles to design how a whole company operates. When choosing tradeoffs, approaches, and practices, check whether the element you're designing violates one of the principles. If it does, design an alternative approach that doesn't.

The principles work in synergy, so the value they bring when implemented together is more than the sum of the parts, but they're individually useful. That means you can apply them to designing not only whole organizations, but also departments, areas, and teams.

At the very least, they provide a framework to evaluate how effective a company or a team is.

# Applicability

Like any model, these principles have specific applicability boundaries. They're only useful when:

1. There's a willingness to strive for excellence. If a company is content with doing okay, some of these will sound extreme or dangerous.
2. The results are placed before what's better for some people. The non-goals include keeping people in their comfort zone, supporting control structures, and feeding people's ego.

# Principles

## Outside-in organization

Employees work across different levels. Activities range from being closest to the customers, to the innermost level. The time horizons tend to widen as the levels get further from the customers.

The inner levels support the outer levels. It's about coordination, not command and control. The outer levels can pull help from the inner levels, but the decision-making stays with the people working as close as possible with the customers.

The people that work in the inner levels tend to manage how the work works, and shepherd long-term goals, initiatives, and changes.

The opposite of this is the traditional top-down organization, where each level controls and manages the level below.

## The unit of work allocation is a team

Work is carried over by teams, rather than by individuals. This means that nothing is allocated to a specific one person.

A team is a group of people working together towards the same goal. Sharing a goal is not enough, people need to collaborate synchronously towards achieving it. Ensemble programming is a great example of a practice that embodies this principle.

## Small equivalent teams

Teams should be as small as possible, while still qualifying as a team. A team must abstract who's doing what, be capable of doing any work, and be resilient to absences. To do so, teams should be cross-functional and staff people with different backgrounds and strengths.

About backgrounds, you want a mix of old and young, senior and more junior, academic and self-taught, genders, etc. In terms of archetypes, you need shapers, fixers, and explorers. You also want both starters and finishers. When it comes to skills, you should at least cover web development, user experience, distributed systems, codebase structure, Cloud infrastructure, databases, product discovery, scripting, observability, and code maintainability.

I believe teams of five people can achieve the requirements above, without internally splitting into more than one team. People are not interchangeable, and the same person will complement a team and not fit in others. Hire for the specific skills, strengths, archetype, personality, and background you need in a given team.

The design goal is to eliminate any dependencies across teams.

## Work-in-progress limits

Each team should be working on only one initiative at a time. So the number of teams you have is the degree of parallelism you get. Not everything counts as an item though, only high-level product goals or technical initiatives do. So a team is always improving various things, but only working on a significant piece of work at a time.

## Pull-based just-in-time work

The teams should pull work when they become available. As a team finishes working on an initiative, they should pull the next initiative and start working on it. This means that teams cannot get overwhelmed by work pushed on them. Information about upcoming work shouldn't reach a team until that team has finished the current initiative.

## Pull-based information

Information should also be pull-based, made available when and if a team or a person needs it. Documentation, expertise, advice, support, etc. should all be accessible when needed by anybody.

## Leaderless teams

A team should be a group of equals who are great at different things. Nobody should be the designated leader of the team. Seniority shouldn't formally matter. The team can self-organize in terms of representation when dealing with stakeholders, but nobody should be allowed to represent indefinitely.

## Company-wide initiative queues

A company should organize and prioritize goals and work initiatives using company-wide queues. This means that prioritization should happen across areas, rather than within each area.

This works well with equivalent teams capable of working on anything needed, so that the company can focus on whatever is needed.

This is in opposition to deciding what's next for each team or area, leading to inflexibility in work allocation.

## Direct Responsible Individuals for initiatives

Each initiative should have a Direct Responsible Individual (DRI), who's in charge of coordinating the work, escalating risks and issues, and outline dependencies. The DRI is not responsible for the outcomes, and it's not the ultimate decision-maker.

When decisions are of medium importance, the DRI might make a call, but anybody can decide to escalate to senior management.

Being a DRI is not a job, and it's always a temporary engagement. The rule is that if you just finished an initiative you were DRI for, you're not going to be DRI in the next initiative you work on. A DRI is nominated autonomously by the team that commits to an initiative.

## Tribes as smaller companies

A company should behave as a whole until it reaches the critical number of 50 developers (roughly 10 teams). At that moment, the company should adopt Tribes to coordinate the work better.

Tribes are purposed mini-companies within the larger company. Everything works the same, except for the fact that everything stays within a tribe (teams, initiative queues, prioritization, etc.). Tribes should focus on end-to-end vertical slices of the business, not on a given function.

When a tribe becomes too big, and has ten or more teams, it can create nested tribes within itself. Each nested tribe relates to the parent tribe in the same way the parent tribe relates to the company. 

The design goal is to eliminate any dependencies across Tribes.

## People who work together sit close to each other

People in a team should sit together. Teams belonging to the same tribe should also be near each other. Experts should move around to the team that needs their expertise.

## Evolutionary approach to development

Important decisions and initiatives should be de-risked by leveraging a set-based approach. Different teams should work in parallel on the same decision or initiative, without any contact between them, except for checking they're not converging towards the same solution.

The importance of the work determines the number of teams working towards the same goal in parallel. At the end, the different solutions produced can be compared across multiple dimension, and a higher-quality decision or solution is adopted.

This is a commonplace practice in collaborative knowledge work (policymaking, city planning, vaccine development, science research, etc.), and in opposition to the standardization and efficiency factories obsess about.

## Vertically-aligned people

People should be associated with vertical product organizations (tribes), as opposed to horizontal function-specific ones. So, as an example, a Java back-end engineer in the "Everyday Spending" tribe would be a product developer within the "Everyday Spending" tribe, rather than a Java developer, or a back-end engineer.

Horizontal structures can exist, but none can be across the vertical structures, only contained within them. So, if the "Savings" tribe decides to adopt a "back-end" chapter to try and coordinate the continuous learning in that area, they're free to do so, but that organization only lives within that tribe, never across tribes.

This means that anybody in a tribe reports to the tribe lead, a cross-functional lead, regardless of their own area of expertise. So if a lawyer works within the "Savings" tribe, they report into the "Head of Savings", not the "Head of Legal".

## Collective code ownership

The teams collectively own the whole codebase of the company. No team or person "owns" any part of the codebase. Nobody needs to ask permission to anybody else to access and modify any code.

This holds true even across tribes. It's natural that some teams and tribes will focus more on specific areas, but this changes nothing about this point.

## Collective product ownership

The teams collectively own the product and the features. No team or person "owns" an area of the product.

This holds true even across tribes. It's natural that the tribes will tend to work on separate areas of the product, and this is encouraged, but a tribe should never have to ask permission to another tribe to implement or modify a feature.

## Vigorous learning on the job

Vigorous learning should happen as part of the job. Function-specific and cross-function training should both be organized by the company for all employees. Training should be coordinated by both internal and external experts, and can include doing actual work outside of someone's main role.

Training should involve theory and practice, and occur during working hours. Training should be mandatory for everybody, across all the provided subjects.

Cross-function training for developers should include finance, marketing, product management, design, sales, business, and domain knowledge, e.g., industry-specific things. For other functions, it should be similar, and include software development.

20% of working hours is the minimum that's effective, so that's 1.5 hours a day or 1 day a week.

## Continuous collaboration

The teams continuously collaborate, within the team, and with sponsors, experts, inner level managers, cross-functional leads, and function leads. The preferred way of collaboration is synchronous. Whoever liaises with the team joins the team for the duration of the engagement.

From first principles, fully remote co-located teams can hardly ever be as effective as physically co-located teams. It does not mean it's not feasible to run a fully remote team, but inherently the collaboration, even when done perfectly, will be less effective than a perfectly structured in-person equivalent. This might be compensated by other factors. Nonetheless, physically co-located teams remain the preference.

When a team commits to work on an initiative, they engage with that initiative's sponsor. This close collaboration lasts for the entire duration of the work, and terminates when the team pulls another initiative sponsored by another person.

## Product managers stay with the value stream

Product managers are not part of the teams, but focus on a value stream. Each value stream can have one or more dedicated product managers. A product manager can coordinate the work for more than one value stream, even if they're ideally single-threaded.

Every time a product initiative is part of a value stream, that value stream's PM is the sponsor for the initiative. The team working on the initiative will work closely with them for the duration of the engagement. The teams remain responsible for the decision-making, while the sponsor acts as stakeholder and advisor.

## Experts stay within the technical value stream

Experts coordinate the work for their technical value streams. A security expert will act as sponsor for all technical initiatives living under the security value stream. In terms of collaboration with the teams, they behave like product managers do. As usual, the teams remain responsible for the decision-making, while the sponsor acts as stakeholder and advisor.

## Experts are available as advisors

Experts are always available for advice, even when a team is working on an initiative outside of that person's (technical) value stream. If a team needs help, the team calls in the expert, who joins the team for as long as the team deems necessary.

This applies to experts of all sorts, including architecture, product discovery, product observability, security, marketing, compliance, legal, etc.

## The teams own the way they work

Each team is responsible for the way they work. This includes hiring, firing (more on this below), onboarding, training, and the processes and tools the team uses. Managers working at inner levels can coordinate processes and activities to facilitate the adoption of what's working among the teams, but the teams remain responsible for how they work.

The only constraint is that any way the team decides to work should respect these principles.

If a team routinely misbehaves or causes trouble, a mechanism (more on this below) is eventually triggered, and the team is dissolved. 

## No meetings

Meetings should be avoided and replaced by continuous synchronous collaboration. Cross-functional ensemble programming is a good way of avoiding meetings. When somebody wants to know something from a team, they join the team's ensemble and have a chat.

The design goal is for every team member to have access to all the information.

## Nobody manages anybody

Somebody ultimately must be responsible to identify and root out bad actors and bad hires (more about this below), but nobody manages anybody. People can have 1:1s with whoever they feel like, as part of the learning time.

Nobody approves anybody's holidays. Purchases and expenses happen automatically, within a team-level ample budget. Smart credit cards, e.g., Pleo should be used to ensure control and visibility.

The design goal here is freedom and responsibility. Anybody should be able to stand in front of their team or the founders and explain why an expense was in the best interest of the company. Failure to do so should result in termination of employment.

## No seniority roles, specific titles, and promotions

Everybody working in the outer level, close to the customers, should be a "product developer". Titles can reflect somebody's tribe, but this should have no impact in terms of compensation, benefits, or treatment. A title might be "Product developer, Everyday Spending".

Seniority titles should also not appear in any form. No senior, lead, staff, principle anything. Promotions should also not happen. People should only change role when they want to, and when it's needed by the company. In any case, compensation should exclusively be a function of the years of experience the person has, their main skills, their location, and their tenure within the company.

This is in opposition to career ladders and progression frameworks.

## Profit-sharing schemes

No person or team should receive a bonus, since their contribution matters way less that how the work works. Individual or team bonuses foster internal competition within the company, and that's to be avoided.

The whole company should participate in a profit-sharing scheme, distributed according to a person's years of experience, primary skills, and tenure in the company.

This is in opposition to individual-performance-related bonuses.

## No performance reviews

No performance reviews should happen. This applies to both teams and individuals. There should be mechanisms to fire bad actors and bad hires, as described below, but these involve a collective and subjective decision.

Nobody gets normally reviewed in terms of performance. People are not compared, as they're not equivalent. Teams are compared, with the only goal of collectively improving the ways of working across the teams.

## No feature branches

No other branch that the main branch should ever be used. Each team should push small increments directly to the remote main branch, after having run all tests locally. Whenever the main branch gets broken, the team should stop what they're doing and fix it forward, rather than rolling back.

Locally, the code should go from a working state to another working state, incrementally and iteratively, rather than be allowed to become broken before being fixed again.

## Releases happen every day

Releases should happen continuously, every day, without coordination, in an uneventful way. Each commit that's pushed to the main branch should be automatically built, tested, packaged, and deployed. People shouldn't even be aware of when the code is being released. Product releases that need sales or marketing support should be enabled with feature flags after they were already released in the dark, with all the communications and campaigns they might need.

Avoiding releases after a specific hour, or on specific days, e.g., on Fridays is a red flag. Any coordinated release approach e.g., code freezes, tags, "keeping an eye on it" is also a red flag.

## Only production

Production should be the only permanent environment. People should use internal tenants and users for exploratory testing, smoke tests, live demos, etc.

Changes so dangerous than they are impossible to feature-flag or blue/green should be rare. In those cases, an ephemeral detached copy of the production environment should be created with infrastructure as code, and the dangerous changes or the intense testing can happen there.

Having dev, test, or staging environments is a red flag.

## Sustainable pace

Working hours should include 5 hours a day of collaborative work, plus 2 hours of learning activities. Holidays should be unlimited, with a minimum of 25 days a year plus the national holidays.

People should have flexibility in terms of working from home and working hours, but the expectation is that, on most days, during core hours, the whole team is synchronously working together in the same physical location.

## Products, not projects

The company should avoid projects, and work on products. The difference is that work on products is continuous, without start and end date, or without a specific customer in mind.

No need for deadlines, as the company should sell only what's already built. Not much need for estimates either, as initiatives should be funded based on the value they're producing and the pace they're progressing at.

The company should set goals, in terms of qualitative improved user behaviour on the product, and the teams should produce ideas to reach these goals. The assumptions behind each idea should be validated, using the existing data, or using product discovery techniques. The most promising idea, based on the data, should be attempted first. This does not mean the whole idea should be built, but only an initial step, to gain further validation that the idea will work out. If the initial step is working well in the hands of customers, then a second small step should be attempted. Every task should be associated with a step.

This is, in a nutshell, the GIST framework codified by Itamar Gilad, and it's an excellent way of running a product company. Mind that in such an organization, budget is allocated fluidly based on demand, rather than be frozen in large chunks upfront. It's the teams and the goals that get funded, not the ideas, the steps, or the tasks.

## Roles

Apart from product developers (of all sorts, backgrounds, calibre, specialty, etc.), the only possible roles are:

1. Cross-functional lead (CFL): responsible to coordinate and shepherd a tribe. People with different skills, seniority, or expertise align to the cross-functional lead of the tribe they're in. A cross-functional lead e.g., "Cross-Functional Lead, Savings", can come from any background, even if experience in software development and product management are both heavily recommended. CFLs choose the product goals the teams commit to try and achieve.
2. Function lead (FL): responsible to coordinate work and initiatives within their function. People within that function liaise with the function lead, but are aligned to the cross-functional lead of the tribe they're in. A function lead should be a very senior member of their function. As an example, a "Function Lead, Legal" role should be a very senior corporate solicitor; legal experts in the various tribes all align to their tribe's CFL, but liaise with the Legal FL as well. FLs choose the technical goals the teams commit to try and achieve. 
3. Managers: coordinators and shepherds of processes, and work at inner levels in the outside-in organization. Nobody manages people, only processes. Specifically, managers coordinate the continuous improvement of the processes they focus on, liaising with CFLs, FLs, and product developers. A manager should be intimate with the way the work their process aims at improving works. As an example, a software development manager should be intimate with how software development works. This typically means they must have a strong background in software development.
4. Founders or CEO: responsible to protect the system of work, and to come up with and continuously repeat the vision and the mission, so everybody is aligned.

## One-way decisions must be reviewed and can be vetoed

For two-way decisions, those who can easily be reverted, there's no need to seek validation outside a team.

Some decisions, though, are one-way, meaning there's no easy way to undo them, and the consequences might be significant. For these decisions, the teams must present their reasoning and conclusions to the cross-functional lead involved, and the relevant the function leads. During this presentation, the CFL and the FLs can veto the decision made by the team, explaining why they disagree and what negative consequences the company would risk. The team can disagree and escalate this to founders and/or the CEO.

In any case, CFLs, FLs, founders, and CEO shouldn't make a decision themselves, but let the team come up with an alternative decision, to be reviewed once again.

There are many kinds of one-way decisions, and the teams need to receive coaching to identify them correctly. Firing people is a great example of something that it's always one-way, and must thus be presented to a CFL and the relevant FLs before a team can move forward.

## How under-performing teams are addressed

TODO

## How under-performing employees are addressed

TODO

## How misbehaving teams are addresses

TODO

## How misbehaving employees are addressed

TODO

##### TODO

- Bad actors and bad hires get fired (how? by who? when? after trying what? how do people get fired? how do teams get dissolved?)