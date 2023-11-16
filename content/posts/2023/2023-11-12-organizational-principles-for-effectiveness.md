---
title: "Organizational principles for effective software product development"
categories: [ "management" ]
tags: [ "system-thinking", "management", "effectiveness", "startups", "organization-design" ]
date: 2023-11-12T05:00:00
draft: true
---

I often rant about what I feel is wrong with an approach, practice, or system. Today, instead, I want to describe some principles that an effective software product development company should adopt.

Why principles? Wouldn't a detailed description of how things should work be more useful? It'd be almost impossible to write, as it'd be a colossal task. Perhaps it'd be good for a book, but definitely not for a blog post.

Also, reality is multifaceted and nuanced. Everything depends on everything. Prescriptive approaches don't cope well with dynamic situations. Principles, on the other hand, allow you to deal with uncertainty.

In hindsight, this blog post turned out to be longer and much harder to write than I originally imagined, so get ready for a rabbit tunnel.

# How to use these principles

You can use these principles to design how a company operates. While you're designing, check whether the system violates any of the principles. If it does, design an alternative one that doesn't.

These principles work in synergy, so the value they bring when implemented together is more than the sum of the parts. However, they're also useful on their own, which means that you can apply them when designing not only whole organizations, but also departments, areas, or teams.

At the very least, they provide a framework to evaluate how effectively a company or a team operates.

# Applicability

Like any model, these principles have specific applicability boundaries. They're only useful when:

1. There's a willingness to strive for excellence. If a company is content with merely doing okay, some of these will sound extreme or dangerous.
2. The results are placed before what's convenient for some people. Keeping people with their comfort zone, supporting the existing control structures, and feeding people's ego are non-goals.

This list is also incomplete. So if I don't mention a specific good principle you have in mind, it doesn't mean I'm saying it's not important.

# Principles

## Outside-in structure

Employees work as part of different levels. Activities range from being closest to the customers, to the innermost level. The time horizons tend to widen as the levels get further from the customers.

The inner levels support the outer levels. It's about coordination, not command and control. The outer levels can pull help from the inner levels, but the decision-making stays with the people working as close as possible with the customers.

The people that work in the inner levels tend to manage how the work works, and shepherd long-term goals, initiatives, and changes.

The opposite of this model is the traditional top-down structure, where each level controls the level below it.

## The unit of work allocation is a team

Work is carried over by teams, rather than by individuals. This means that there are no individual tasks or assignments.

A team is a group of people working together towards the same goal. Sharing a goal is not enough, people need to collaborate synchronously towards achieving it. Ensemble programming is a great example of a practice that embodies this principle.

## Small equivalent teams

Teams should be as small as possible, while still qualifying as a team. A team must abstract who's doing what, be capable of doing any work, and be resilient to absences. To achieve this, teams should be cross-functional and staff people with different backgrounds and strengths.

You want a mix of old and young, senior and junior, academic and self-taught, genders, etc. You also need shapers, fixers, and explorers. A team should also include both starters and finishers. About skills, you should at least cover web development, user experience, distributed systems, codebase structure, Cloud infrastructure, databases, product discovery, scripting, observability, and code maintainability.

People are not interchangeable, and the same person might complement a team while not being a good fit in others. Hire for the specific skills, strengths, archetype, personality, and background you need in a given team.

I believe that 5 team members is the sweet spot in most cases. You can get the necessary diversity, are resilient to 1 or 2 absences, and you don't get so many people that they inevitably need to work on more than 1 thing at a time.

The design goal here is to eliminate cross-team dependencies.

## Work-in-progress limits

Each team should be working on only 1 initiative at a time. So the number of teams you have is the degree of parallelism you get. Not everything counts as an item though, only high-level product goals or technical initiatives do.

A team is always improving various things, but only working on 1 significant piece of work at a time.

## Pull-based just-in-time work

The teams should pull work when they finish their previous work. As a team finishes working, they should pull the next initiative or goal and start working on it.

This means that teams cannot get overwhelmed by having work pushed on them. Information about upcoming work shouldn't reach a team until that team has finished their current initiative.

## Pull-based information

Documentation, expertise, advice, support, and other types of information should also be pull-based, and made available when somebody needs it.

## Leaderless teams

A team should be a group of equals who are great at different things. Nobody should be the designated leader of the team. Seniority shouldn't formally matter. The team can self-organize in terms of representation when dealing with stakeholders, but nobody should be allowed to represent the team formally or indefinitely.

## Company-wide initiative queues

A company should organize and prioritize goals and initiatives using company-wide queues. This means that prioritization should happen across areas, rather than within each area.

This works well with equivalent teams capable of working on anything, so that the company can focus on whatever is needed.

This is in opposition to deciding what's next for each team or area, leading to inflexible work allocation and suboptimal ability to focus.

## Direct Responsible Individuals for initiatives

Each initiative should have a Direct Responsible Individual (DRI), who's in charge of coordinating the work, escalating risks and issues, and outlining dependencies. The DRI is not responsible for the outcomes, and is also not a decision-maker.

When decisions are of medium importance, the DRI might make a call, but anybody can decide to escalate the decision to people who work in inner levels.

Being a DRI is not a job, and it's always a temporary engagement. The rule is that if an initiative you were DRI for just ended, you're not going to be DRI in the next initiative you work on. The DRI is nominated autonomously by the team that commits to an initiative.

## Tribes as smaller companies

A company should behave as a whole, until it reaches the critical number of 50 developers, roughly 10 teams. At that moment, the company should adopt tribes to coordinate the work better.

Tribes are like mini-companies within the wider company. The principles apply in the same way, except for the fact that everything stays within a tribe (teams, initiative queues, prioritization, etc.). Tribes should focus on end-to-end vertical slices of the business, not on a given function.

When a tribe becomes too big, and has 10 or more teams, it should create nested tribes within itself. Each nested tribe relates to the parent tribe in the same way the parent tribe relates to the company. 

The design goal here is to eliminate cross-tribe dependencies.

## People who work together sit close to each other

People in a team should sit together. Teams that belong to the same tribe should also be near each other. Experts should go to the team that needs their expertise, and be there for the duration of the engagement.

## Evolutionary approach to development

Important decisions and initiatives should be de-risked by leveraging a set-based approach. Different teams should work in parallel towards the same goal, or on the same initiative, without any contact between them, except checking they're not converging towards the same solution.

The importance of the initiative determines the number of teams working on it in parallel. At the end, the different solutions produced can be compared across multiple dimension, and a higher-quality decision or solution is reached.

This is a frequent practice in collaborative knowledge work (policymaking, city planning, vaccine development, scientific research, etc.), and in opposition to the standardization and efficiency factories obsess about.

## Vertically-aligned people

People should be associated with their vertical product organization, their tribe, as opposed to their horizontal function-specific one. As an example, a Java back-end engineer in the "Everyday Spending" tribe would be a product developer within the "Everyday Spending" tribe, rather than a Java developer, or a back-end engineer.

Horizontal structures can exist, but none can be across the vertical structures, only contained within them. So, if the "Savings" tribe decides to adopt a "back-end" chapter to try and coordinate the continuous learning in that area, they're free to do so, but that organization only lives within that tribe, never across tribes.

This means that anybody in a tribe is aligned to the cross-functional lead for that tribe, regardless of their own area of expertise. So if a lawyer works within the "Savings" tribe, they work under the remit of the "Head of Savings", not of the "Head of Legal".

## Collective code ownership

The teams collectively own the whole codebase of the company. No team or person owns any part of the codebase. Nobody needs to ask permission to anybody else to access and modify any code.

This holds true even across tribes. It's natural that some teams and tribes will focus more on specific areas, but this changes nothing about this point.

## Collective product ownership

The teams collectively own the product and the features. No team or person owns an area of the product.

This holds true even across tribes. It's natural that the tribes will tend to work on separate areas of the product, and this is encouraged, but a tribe should never have to ask permission to another tribe to implement or modify a feature.

## Continuous collaboration

The teams continuously collaborate, both within the team and with sponsors, experts, managers, cross-functional leads, and function leads. The preferred way of collaboration is synchronous. Whoever liaises with a team joins that team for the duration of the engagement.

From first principles, fully remote teams can hardly ever be as effective as physically co-located teams. It does not mean that running a fully remote team is not feasible, but the collaboration, even when done perfectly, will inherently be less effective than a perfectly-structured in-person equivalent. This might be compensated by other factors. Nonetheless, physically co-located teams remain the preference. If a company prefers to work remotely, a team should enlist members that are geographically near to each other in terms of timezone. Hybrid teams should be avoided.

When a team commits to work on an initiative, they engage with that initiative's sponsor. This close collaboration lasts for the entire duration of the work, and terminates when the team pulls another initiative that is sponsored by another person.

## Product managers stay with the value stream

Product management experts are not part of the teams, but focus on a value stream. Each value stream can have one or more dedicated product managers. A product manager can coordinate the work for more than 1 value stream, even if they're ideally single-threaded.

Every time a product initiative is part of a value stream, that value stream's PM is the sponsor for the initiative. The team working on the initiative will work closely with them for the duration of the engagement. The teams remain responsible for the decision-making, while the sponsor acts as stakeholder and advisor.

## Experts stay within the technical value stream

Experts coordinate the work for their technical value streams. A security expert will act as sponsor for all the technical initiatives part of the security value stream. In terms of collaboration with the teams, they behave like product managers do. As usual, the teams remain responsible for the decision-making, while the sponsor acts as stakeholder and advisor.

## Experts are available as advisors

Experts are always available for advice, even when a team is working on an initiative outside of that person's (technical) value stream. If a team needs help, the team calls in the expert, who joins the team for as long as the team deems necessary.

This applies to experts of all sorts, including architecture, product discovery, product observability, security, marketing, compliance, legal, etc.

## The teams own the way they work

The teams are responsible for the way they work. This includes hiring, firing (more on this below), onboarding, training, and the processes and tools the team uses. Managers can coordinate processes and activities to facilitate the adoption of what's working well in specific teams, but the teams remain responsible for how they work.

The only constraint is that any way the team decides to work should respect these principles.

If a team routinely misbehaves or causes trouble, a mechanism (more on this below) is eventually triggered, and the team is disbanded. 

## No meetings

Meetings should be avoided and replaced by continuous synchronous collaboration. Cross-functional ensemble programming is a good way of avoiding meetings. When somebody wants to know something from a team, they join the team's ensemble and have a chat.

The design goal is that every team member should have access to all the information.

## Nobody manages anybody

Somebody ultimately must be responsible for identifying and addressing bad actors and under-performers (more about this below), but nobody should manage anybody.

Nobody approves anybody's holidays, and nobody approves purchases and expenses either. Smart credit cards, e.g., Pleo should be used to ensure control and visibility. Anybody should be able to stand in front of their team or the founders and explain why an expense was in the best interest of the company. Not being able to justify it should result in termination of employment.

The design goal here is freedom and responsibility.

## No seniority designations, specific titles, or promotions

Everybody working in the outer level, close to the customers, should be a "product developer". Titles can reflect somebody's tribe, but this should have no impact in terms of compensation, benefits, or treatment. A title might look like "Product developer, Everyday Spending".

Seniority designations should also not appear in any form. No senior, lead, staff, or principle anything. Promotions should also not happen. People should only change role when they want to, and when it's needed by the company. In any case, compensation should exclusively be a function of the years of experience the person has, their main skills, their location, and their tenure within the company.

This is in opposition to career ladders and progression frameworks.

## Profit-sharing schemes

No person or team should receive a bonus. Individual or team bonuses foster internal competition, and that's to be avoided.

The whole company should participate in a profit-sharing scheme, distributed according to a person's years of experience, primary skills, and tenure in the company.

This is in opposition to individual performance-related bonuses.

## No performance reviews

No performance reviews should occur, for neither teams nor individuals. There should be mechanisms to address bad actors and under-performance, as described below, but these are triggered as soon as the problem is spotted, not quarterly or at the end of the year.

People are not compared, as they're not equivalent. Teams might occasionally be compared, with the only goal of collectively improving the ways of working across the teams.

## Continuous Integration

No other branch that the main branch should ever be used. Each team should push small increments directly to the remote main branch, after running all tests locally. Whenever the main branch gets broken, the team should stop what they're doing and fix it forward, rather than rolling the changes back.

Locally, the code should go from working state to working state, incrementally and iteratively, rather than be allowed to become broken before getting eventually fixed.

## Continuous Delivery (even on Fridays)

Deployments should happen continuously, every day, without coordination, in an uneventful way. Each commit that's pushed to the main branch should be automatically built, tested, packaged, inspected, and deployed. People shouldn't even be aware of when the code is being deployed. Changes that require sales or marketing work should be enabled with feature flags after they were already released in the dark, with all the communications and campaigns they might need.

Avoiding deployments after a specific hour, or on specific days, e.g., on Fridays is a red flag. Any coordinated release approach e.g., code freezes, tags, or "keeping an eye on it", is also a red flag.

## The only manual testing is exploratory

No regression testing should ever be performed manually. Manual testing should be strictly exploratory. Teams should be encouraged to routinely perform exploratory testing.

A cross-functional team dedicated to exploratory testing isn't a bad idea, but exploratory testing should leave outside the software product lifecycle. In particular, manual testing as part of the release process is a red flag.

## Only production

Production should be the only permanent environment. People should use internal tenants and users for exploratory testing, smoke tests, and live demos, directly in production.

Changes so dangerous than they are impossible to feature-flag or rolled out using a blue/green approach should be rare. In those cases, an ephemeral clone of the production environment should be created with infrastructure as code, and the dangerous changes or the intense testing can happen there.

Having dev, test, or staging environments is a red flag.

## Sustainable pace

Working hours should include 5 hours a day of collaborative work, plus 2 hours of learning activities. Holidays should be unlimited, with a minimum of 21 days a year plus the national holidays (typically 9 days). Holidays booked past the 21 days minimum should not be recorded.

People should have flexibility in terms of working from home and working hours, but the expectation is that, on most days, during core hours, the whole team is synchronously working together in the same location.

## Products, not projects

The company should avoid projects, and work on products instead. The difference is that the work on products is continuous, without start and end dates, and with no specific customer in mind.

There's also no need for deadlines, as the company should only sell what's already built. Estimates become unnecessary as well, as the initiatives should be funded based on the value they're producing and the pace they're progressing at.

The company should set goals, expressed as qualitatively improved user behaviour, and the teams should produce ideas to reach these goals. The assumptions behind each idea should be validated, using the existing data, or through product discovery techniques. The most promising idea, based on the evidence, should be attempted first. This does not mean the whole idea should be built, only an initial step, to gain further validation that the idea will work out. If the initial step is working well in the hands of the customers, then a second small step should be attempted. Every task should be associated with a step.

This is, in a nutshell, the GIST framework codified by Itamar Gilad, and it's an excellent way of running a product company. Mind that, in such an organization, funds get allocated fluidly based on demand, rather than being frozen upfront in large amounts. It's the teams and the goals that get funded, not the ideas, the steps, or the tasks.

## Employing great people

The company should strive to ensure it employs great people. This should be reflected across many aspects, including salaries, benefits, but also on-the-job training. The acquired capabilities and the teams are the most important assets of a company, so they must be protected at all costs.

## Roles

Apart from product developers (of all sorts, backgrounds, calibre, specialty, etc.), the only other roles are:

1. Cross-Functional Leads (CFLs): responsible to coordinate and shepherd a tribe. People with different skills, seniority, or expertise align to the cross-functional lead of the tribe they're in. A cross-functional lead e.g., "Cross-Functional Lead, Savings", can come from any background, even if experience in software development and product management are both heavily recommended. CFLs propose the product goals the company prioritizes.
2. Function Leads (FLs): responsible to coordinate work and initiatives within their function. People within that function liaise with the function lead, but are aligned to the cross-functional lead of the tribe they're in. A function lead should be a very senior member of their function. As an example, the "Function Lead, Legal" should be a very senior corporate solicitor. Using the same example, legal experts in the various tribes would all align to their tribe's CFL, but liaise with the Legal FL as well. FLs propose the technical goals the company prioritizes. 
3. Managers: coordinators and shepherds of processes. Nobody manages people, only processes. Specifically, managers coordinate the continuous improvement of the processes they focus on, liaising with CFLs, FLs, and product developers. A manager should be intimate with the way the work their process aims at improving works. As an example, a software development manager should be intimate with how software development works, meaning that, in this example, that manager would have to have a strong background in software development.
4. Founders or CEO: responsible to protect the system of work, and to come up with and continuously repeat the vision and the mission, so that everybody aligns.

It's important to stress again the fact that nobody is managed by anybody. If required, every employee formally reports to the CEO. CFLs, FLs, and managers coordinate the work of those teams closest to the customers, but this is nothing more than coordination. Managers are not subordinated to CFLs or FLs, it's just a different focus. So thinking about CFLs and FLs as directors, under the executives, and above management is incorrect here.

## One-way door decisions are reviewed and can be vetoed

Most decision can be easily reverted. These 2-way door decisions are made autonomously by the teams.

Some decisions, though, are more like one-way doors, meaning there's no easy way to revert them, and their consequences can be significant. The teams must present their reasoning and conclusions to people in an inner circle, whenever they make a one-way door decision. The reviewers can veto the decision, explaining their reasoning, but cannot force a decision. The review board includes the relevant cross-functional lead and function leads.

If a team disagrees with the review board, they can escalate this further to the founders and/or the CEO.

In any case, whenever a decision is vetoed, the team must make a different decision, and repeat the process. CFLs, FLs, founders, and CEO shouldn't make the decision themselves.

There are many kinds of one-way door decisions, and the teams need to be trained to identify them correctly. Firing people is a great example of something that is always a one-way door, and must thus be presented for review before a team can move forward.

## Transparency and access to information

TODO most things accessible by everybody.

## Vigorous learning on the job

Vigorous learning should happen as part of the job. Function-specific and cross-function training should both be organized by the company for all employees. Training should be coordinated by both internal and external experts, and can include doing actual work outside of someone's main role.

Training should involve theory and practice, and occur during working hours. Training should be mandatory for everybody, across all the provided subjects.

Cross-function training for developers should include finance, marketing, product management, design, sales, business, and domain knowledge, e.g., industry-specific things. For other functions, it should be similar, and include software development.

20% of working hours is the minimum that's effective, so that's 1.5 hours a day or 1 day a week.

## Under-performance is addressed

A person or a team might sometimes under-perform. This can be noticed by anybody, including the person or team themselves. At first, the subject should try to diagnose and fix the problem on their own, asking help to anybody they deem might help them.

This variation of performance can be normal, or special. If it's normal, then there's no point in addressing anything, as things tend to fluctuate anyway. You can tell whether a measurement is within normal variation by using control charts, but a subjective assessment is usually enough.

If the performance variation is deemed special, though, it remains to be seen whether it's a temporary condition. If temporary, it might have to do with some external conditions: maybe a new joiner joined the team and the equilibrium will be restored soon, or a family situation is distressing a person, etc. The important thing in this case is identifying probable causes, and monitoring how the situation evolves.

If it's not a temporary condition, or no probable causes have been identified, it's probably a result of the ways of working. Are the current ways of working new? Will the situation take care of itself? What's working less effectively? Identifying the systemic pulls that might be causing the under-performance is important.

If the person or team think they addressed the situation, they should ask the person who spotted the problem (might be themselves as well) if they agree that the problem has been addressed. If the answer is no, this should be escalated to management.

Managers should review what's happening by joining the relevant team for a duration. The time this take varies, but it's usually not short. Two weeks at a minimum for a person, and at least a month for a team. While embedded in the team, two managers will immerse themselves with everything the team does.

In a first phase, the managers will simply observe and take notes, with the occasional question. In a second phase, the managers might suggest improvements or other actions.

About teams, if no other action fixes the problem, the managers can decide to disband the team, merging each person into different teams.

When it comes to people, skills can be learned most of the time, and alternative jobs can be tried within the same company. However, sometimes a person's belief system makes them incompatible with the working principles described here, or even with software product development in general. In this case, the managers can decide to terminate that person's employment.

In all cases, this is always a one-way decision, so it should be presented to the CFL for that area, and to the relevant FLs, as usual.

If the person who's under-performing is:

1. A CFL or a FL, the procedure is identical, apart from the fact that the decision made by the two managers will be presented to the founders and/or CEO instead.
2. A founder or CEO, the procedure is identical, apart from the fact that the decision made by the two managers will be presented to the board of the company. If there's no board, and it's a fully-owned private company, and the founder and CEO is under-performing, then people will have to live with that. That's why boards are important.

If the person who reported the problem:

1. Would be part of the group the managers' decision is presented to, then this is escalated to an inner level instead.
2. Is a manager, or if it's the manager who is reported to be under-performing, the procedure is identical, but different managers are involved.

Everytime under-performance results in a person being fired or a team being disbanded, an email should be sent to the whole company explaining what happened, who made the decision, and what the reasoning was. This is to avoid rumors. 

## Bad behaviour is addressed

Bad behaviour is different from under-performance, and it's important to address it differently. A person or a team are bad actors when they damage others or the company with their actions, and they do so consciously.

The system of work and the incentives can hugely influence everybody's behavior in this sense. And yet, when facing the same systemic pulls, some people decide to do the right thing, while others easily give in and become bad actors. So, while under-performance is usually something fixable, and the company has a duty to try the best it can to address it, bad behavior is a different story.

It's important to stress again that being aware of the damage they cause is a key requirement for somebody to qualify as a bad actor. Also, realizing it after doesn't count, so if somebody that something bad, then realizes it caused damage, and reports it, they're not bad actors. But if they do that intentionally, or even if they decide to cover it up after realizing, they need to be rooted out.

Bad actors are a fundamental threat to companies. While truly malicious actors are rare, selfish and toxic behaviors are quite common, can destroy morale and culture, and spread like mold when not addressed.

The self-identification part of the process doesn't apply here, for otherwise it wouldn't be bad behavior. Anybody can report they feel that a person or a team has a toxic or selfish behavior. Reporting should not happen anonymously, but management should keep the identity of the person who reported it secret. This is an exception to the default transparency for all things, aimed at creating a safe space to have these conversations. It's also imperative that, whenever an escalation is deemed unfounded, the reporter isn't negatively impacted. If the reviewers suspect that the reporter acted maliciously in the first place, though, the reporter should also be investigated as a potential bad actor.

The investigation is conducted by two managers, who review the information reported, interview people in private, collect the anecdotes and evidence in a file, and finally talk to the person being investigated.

The person is informed of the investigation only if the initial anecdotes and evidence substantiate the claim. If that happens, before making a decision, the two managers speak with the person being investigated, in private. They explain what the claim was, without mentioning who opened it, explain how the process was run, and expose the anecdotes and evidence collected, striving not to reveal the names of the people interviewed. The person being investigated can then explain their reasoning, behavior, and version of the story. The two managers make a decision, and then, if the claim is deemed founded, proceed to seek validation from people at an inner level, because these are always one-way decisions.

Whenever revealing anecdotes or evidence might betray the source, the managers should tell the person investigated anyway, as their right to explain themselves takes precedence over the attempt to keep all the involved people anonymous.

If the person who's being investigated as a bad actor is:

1. A CFL or a FL, the procedure is identical, apart from the fact that the decision made by the two managers will be presented to the founders and/or CEO instead.
2. A founder or CEO, the procedure is identical, apart from the fact that the decision made by the two managers will be presented to the board of the company. If there's no board, and it's a fully-owned private company, and the founder and CEO is under-performing, then people will have to live with that. That's why boards are important.

If the person who reported the problem:

1. Would be part of the group the managers' decision is presented to, then this is escalated to an inner level instead.
2. Is a manager, or if it's the manager who is reported to be a bad actor, the procedure is identical, but different managers are involved.

If the decision to accept the claim is validated, the person being investigated is subjected to disciplinary action. In most cases, this should be termination of employment, as minor cases like a one-time off hoarding of candies should be dismissed by the managers in the first place.

Whenever the investigation impacts a team, rather than a person, the disciplinary action should affect all the team members that were aware, determined by the managers, and part of the decision that gets reviewed and validated by the people at inner levels.

Everytime bad behavior results in a person being fired or a team being disbanded, an email should be sent to the whole company explaining what happened, who made the decision, and what the reasoning was. This is to avoid rumors and reinforce the message that bad behavior is not tolerated.