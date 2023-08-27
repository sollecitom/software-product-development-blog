---
title: "Demand, capacity, outputs, outcomes, and impact"
date: 2023-07-15T12:00
categories: ["management", "systems-thinking", "business"]
tags: ["demand", "management", "capacity", "queues", "output", "impact", "outcomes"]
---

"This year we want to double the number of developers!"

"We can't put UX/UI and QA in each team, it's inefficient!"

Sigh, if only reality was so simple. I wonder when screaming your ignorance and incompetence to the world will start getting frowned upon.
<!--end_excerpt-->

# The problem

Many managers would tell you that management is an art. But what they mean is that they wing it, without paying any attention to theory or thinking things through.

"We need to double the money we make, so we're going to double the number of developers we have!"

Now, if you come from another perspective, this sounds insane. How could anyone come up with this? And how could anyone let them make decisions?

In their "defense", in many cases the actions they suggest would bring personal benefits, like promotions, more power, or merely attention. So often it's not just a matter of incompetence, but one of integrity. This doesn't come with any judgement, as everybody is self-serving and does what they think is best for them. The problem is that some systems encourage these behaviours, but let's not discuss this today.

So what's the common model so many people in so many companies adopt? Well, they assume that the workforce size translates linearly into the impact e.g. Annual Recurring Revenue (ARR). So if we have 2 salesmen, 4 developers, and are making $1M ARR, if we get to 4 salesmen and 8 developers, we'll be able to make $2M ARR.

Admittedly, this level of delusion is rare, and most people immediately recognize that it makes little sense when they're confronted about it (even if their behaviour often follows this assumption anyway). But other equally simplistic and inadequate models are very popular within the software product development industry. This leads to bad considerations, bad decisions, and typically to bad Outputs, Outcomes, and Impact.

# A better model to think about work

Before we can discuss how we can do better, let's remind ourselves of some concepts.

## Some definitions

- Work: work is anything a person, a team, or a Company does, according to what the company expects of them. Meetings, writing code, answering the phone, reports, etc. Checking your personal Facebook page is not work.
- Employee: a person working for the Company. For this analysis we limit this to Line Employees, the ones that generate Capacity, as opposed to Managers. 
- Workforce Size: the number of Employees contributing Capacity.
- Demand (D): all the things a Company asks its employees to work on.
- Outputs: the stuff you build or produce as a Company, a team, or an employee.
- Capacity (C): how much a unit of work allocation contributes to the Outputs. Could be used for an employee, but makes more sense for a team or a company. It's the Outputs progressed over a time window.
- Outcomes: the amount of value a Company delivers to its market. It's the value customers and users get from the company's products and services. Note that Outputs can improve Outcomes, but they can as easily harm them.
- Impact: the amount of value a Company captures from its market. It's the amount of resources (money, attention, loyalty, etc.) the company can get from its market. Outputs cause changes in Outcomes, which cause changes in Impact. Note that Outcomes might improve or harm Impact.
- Wealth: the difference between the value delivered minus the resources absorbed. It's Outcomes minus Impact.
- Company: a social system whose purpose is to produce and redistribute Wealth in its target market, indefinitely over time.
- Busy: the state of an Employee that's carrying over Work.
- Idle: the state of an Employee that is not carrying over Work.
- Utilization (U): the ratio between busy time and idle time. Usually applied to Employees, but could be considered for teams as well. So an employee that's constantly busy will have a Utilization of 100%, while a constantly idle Employee will have a Utilization of 0%.
- Productivity: the percentage of Work which contributes to the Capacity. If an Employee works hard, but most of this work does not contribute to the Outputs, then that Employee is not very productive. Same for a team or a company.
- Value-Added Work: any work that:
  - A customer is willing to pay for.
  - Transforms the product.
  - Is done right the first time.
- Non-Value-Added Work (or Waste): work that consumes resources, but does not add value to the product or service. Mind that some Non-Value-Added Work (or waste) might be necessary e.g. contracts, regulatory requirements, etc.
- Workflow: the sequence of industrial, administrative, or other processing steps through which a piece of work passes from initiation to completion.
- Processing: the actions performed to progress a piece of work.
- (Processing) Step: a phase of the Workflow for a piece of work. Actions that are intended to design, transform, inspect, or deliver a product.
- Throughput (TP): the quantity of Outputs delivered in the unit of time, averaged out. Assuming all work items are the same, it's the number of finished work items you delivered in the time window you're considering.
- Queue (Q): a backlog of pieces of work a Processing Step must process before it can process other work.
- Queue Time (QT): the amount of time a piece of work spends waiting before getting processed.
- Processing Time (PT): the amount of time a piece of work spends getting processed.
- Total Processing Time (TPT): the total amount of time a piece of work spends getting processed along its whole workflow. 
- Total Queue Time (TQT): the total amount of time a piece of work spends waiting along its whole workflow.
- Cycle Time (CT): it's the amount of time it takes for the Workflow for a piece of work to complete. From when we start working on it, to when it's finished and delivered. It's the Total Processing Time + the Total Queue Time.
- Lead Time (LT): it's the amount of time it takes from a piece of work to go from desired to finished and delivered. It's that piece of work's Cycle Time, plus the Queue Time before first Step of the Workflow can commence.
- Work In Progress (WIP): the amount of work in progress at a given time. So if at any given time you have 4 pieces of work that started their Workflow but haven't finished it, your Work In Progress is 4 at that time.
- [Folks That Matter](https://flowchainsensei.wordpress.com/2018/06/22/the-folks-that-matter/): every person whose needs we need to meet, for otherwise this will have negative consequences for the company. Folks That Matter can be external e.g. customers, users, suppliers, regulators, shareholders, investors, etc. or internal e.g. finance, legal, engineers, product people, sales folks, etc. Kudos to [Bob Marshall](https://flowchainsensei.wordpress.com/) for coming up with this awesome concept.
- Quality: the degree to which a product meets the needs of all the Folks That Matter.
- External Quality: like Quality, but only when considering the needs of the external Folks That Matter.
- Internal Quality: like Quality, but only when considering the needs of the internal Folks That Matter.
- Failure Demand: it's all the work we must do because we failed to fully meet the needs of some of the Folks That Matter.
- Value Demand: it's the work we must do because it delivers value to somebody. It's the Demand, minus the Failure Demand.
- Cost of Delay: the cost of delaying some piece of work. This is typically expressed in "bucks a day", and in terms of how it changes over time.
- Efficiency: how much Capacity we can generate, for a given number of Employees. All else being equal, if it takes 5 people 1 week to produce the same Output 10 people would produce in a week by using another approach, then the first approach is twice as efficient. Efficiency concerns itself with doing the thing right.
- Effectiveness: it concerns itself with doing the right thing. Given a fixed capacity, how much we can make a positive difference in Outcomes and Impact, by producing Outputs. So whenever we use our hard-earned Capacity to produce Outputs, but then those Outputs do not produce desirable changes in Outcomes and Impact, we're not being effective. Failure Demand subtracts from Effectiveness, as it requires us to use our Capacity to carry over work which wouldn't be needed in the first place, if we hadn't failed at meeting the needs of all the Folks That Matter.

Now that we can name things, let's attempt a better way of thinking about work. This model is not "true", because the point of a model is not to correct, but to be useful. Therefore, even this model omits large amounts of details and information that are not deemed useful in order to facilitate making predictions and decisions within the context of software product delivery.

## The context

A company:
- Has a number of Employees.
- Has Employees working in a certain way.
- Has a level of Capacity, deriving from the quality and quantity of its Employees, and the way the work.
- Has Demand as what Outputs to deliver to address the needs of the Folks That Matter.
- Invests its Capacity over time to produce Outputs and address Demand.
- Sees changes in Outcomes and Impact from the Outputs it delivers. These can be positive, negative, or completely unaffected.

## Desirable properties

Many companies implicitly assume that their Capacity is proportional to their number of Employees. This applies overall, or within the context of a given project.

In terms of desirable properties, in order of importance, we got:

1. High Quality: our efforts meet the needs of all the Folks That Matter.
2. High Effectiveness: we only work on what moves the needle. Our Outputs produce desirable Outcomes and Impact.
3. Low Lead Time: once we set our mind and want something, we can deliver it quickly. This is key to minimize Cost of Delay, and to stay reactive to risks and opportunities.
4. Even flow: we deliver things often in increments, as opposed to staggering our value delivery so that things happen in bulk. This way we deliver value early, and we get earlier feedback on our Quality.
5. High Throughput (or Capacity): within a time window, we deliver a lot of Outputs.
6. High Efficiency: we can generate more Capacity with fewer Employees.

It's important to keep in mind that these things need to be optimised in order, and for the long term. If by doing something we become more efficient but less effective, or our efficiency collapses after a quarter, that's not something we should do.

## How to maximise outputs

There's a lot to talk about in terms of how to design a system of work that caters for the desired properties above, in a way that's resilient and sustainable.

But alas this is a blog post, not a book!

So instead of attempting to discuss a good model now (I'll try in another post), I'll leave it to you to consider how you work and what assumptions are behind this way of working:

1. Does your software product development workflow involve more than 1 step?
   - If so, how many? Why? Which ones?
   - Do you have Specification -> Design -> Development -> QA -> Release?
   - Are these steps performed by the same people or by different people?
   - What happens when Development is "finished" for a piece of work, but QA is not free to start working on it? To work in progress? To lead time?
   - What happens when Development is "finished" for a piece of work, but nothing is in the queue because "Design" is lagging behind? To work in progress? To lead time?
   - What are the assumptions behind this way of structuring a workflow?
2. For a single step e.g. Development or QA:
   - Do you think that adding more people will increase the capacity of that step?
   - What are the assumptions behind this if you do? Which ones if you don't?
3. Do your teams specialise in or own an area?
   - Why?
   - What are the consequences of specialisation?
   - What happens when you split a piece of work across teams?
   - How do you structure your on-call for customer support?
   - What assumptions are behind this way of working?
4. How much of your Demand is Failure Demand?
   - Everything that wouldn't happen if your products and services fully met the needs of all the Folks That Matter.
   - How often are you reactive vs strategic in terms of what your teams work on?
5. How often do you release?
   - What happens if we need something really urgently?
   - Do we stop people and ask them to switch context? What happens to the work they were doing before? What happens when you switch context?
   - How likely is that a release will impact your users negatively (bugs, slowness, unavailability, etc.)? Why?
   - What assumptions are behind your release cadence?
6. Do your people work individually or together as a team?
   - Do you have individual tasks? Who decides who works on what? Based on what? What if this decision is not optimal?
   - Do you have individual rewards e.g. bonuses? What's the implicit message you're sending your employees?
   - What does teamwork mean to you? Do your "teams" behave like street cleaners, or like basketball/football/military teams? What's the difference?
   - What assumptions are behind the way your teams work?
7. What does your company believe about speed and quality? What about quality and cost?
   - Do people see these as a trade-off?
   - What's the effect quality has on the time and cost of performing an activity?
   - What effect does it have on Failure Demand?
   - What does this mean for cost?
8. What's the relationship between the Utilization of the members of a team, and the effectiveness of that team?
   - What effect does high Utilization have on throughput? On lead time? On cycle time? On quality?
   - What happens when a road gets to 100% Utilization? What happens to lead time and throughput?
9. What percentage of the things your company decides to build are valuable to your customers?
   - How do you know?
   - How can you not know?
10. Which incentives does your company use on its employees?
    - Why?
    - Which behaviours do they encourage?
    - Are these behaviours desirable?
11. What other implications do your ways of working have on the employees?
    - How do you think people feel, given the ways of working and the incentives?
12. Do you use GitFlow?
    - Why?
    - Do you see any queues, handovers, and waste?
13. Do managers in your company talk about these things?
    - Why? Why not?
    - What are the implicit assumptions?
    - Do they manage the work or how the work works? Why? What are the consequences?
14. Why do companies want to double their number of developers?
    - What are the implicit assumptions here?
    - Why might this not be a great idea?
    - What should they be doing instead?