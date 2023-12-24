---
title: "My belief system for software product development"
categories: [ "system-thinking" ]
tags: [ "software-development", "organization-design", "effectiveness", "management", "belief-system" ]
date: 2023-12-21T05:00:00
draft: true
---

Product development is a complex endeavor. It involves identifying a job to be done people struggle with, creating a product that addresses it well, pricing and marketing it appropriately, defending it against competitors, and reacting to market changes, all while making a profit.

Additionally, software is a highly abstract medium, meaning that common-sense rarely applies, so that what's effective is often counter-intuitive.

And so it's perhaps unsurprising that software companies rarely know how to structure themselves and how to operate, leading to many alternative approaches. Startups copy practices from famous businesses, and there's an abundance of consultants and advisors. Commercial frameworks like SAFe or Scrum promise executives that they won't have to think, and that merely applying the framework will produce great results.

And yet, reality isn't linear or clear-cut. What works in another company won't likely work elsewhere. A practice that's effective in a company with 30 employees will almost surely not work when the same company has 100 employees. Systems are full of interdependencies and nonlinearities, so you cannot improve your sales without changing your product and your marketing, and you cannot change who you hire without changing how you work.

So what should a company do? When common sense doesn't work, frameworks aren't effective, and copying what famous businesses are doing won't take you far?

The answer is that you should write down a set of principles that derive from your belief system, and then use these to orient yourself in this highly complex environment. A belief system is a set of fundamental beliefs that shapes the way you perceive reality and link causes to consequences.

You should evaluate the coherence of your belief system and your principles overall. So if two beliefs or principles conflict, you should think deeper and evolve them, until the conflict disappears.

> What follows is some of my personal beliefs when it comes to software product development. I stand by them, and they served me well over the years, but I keep evolving them, and you shouldn't take them at face value. The important thing is that you write down your beliefs, evaluate them as a whole system, write down your principles, and use them to orient yourself when designing how your company operates.

# Belief system

1. A software product is a set of promises, not a set of features.
2. Customers hire your product to do a job they would otherwise attempt to do in other ways.
3. Product development is about finding a good job to be done, and tailoring your product to meet the customers' needs well, given the circumstances your users find themselves in.
4. A software system is not the sum of its parts: every time there's a new requirement, you need to modify the software to meet this new requirement plus all the previous ones.
5. The cost (effort, risk) involved in modifying a software system depends on its internal quality, which is how well the code is structured.
6. The cost (effort, risk) involved in modifying software depends on how easy it is to understand where to operate the change, and on how contained the change is in terms of testing.
7. The cost of modifying the software because of new requirements always ends up trumping the initial cost involved in writing it.
8. The unit of work allocation should always be a team.
9. Teams should abstract who's working on what, and be resilient to holidays, illness, etc.
10. A team should be able to work on anything the company needs.
11. The coordination effort required in a team, department, or company increases super-linearly with its number of people.
12. We're all going to be wrong a lot.
13. Behind every bad idea that were people thinking it was an excellent idea.
14. The biggest risk for a new company is solving a problem not worth solving.
15. Whenever people disagree, a prototype or test is the right way forward. Whenever people agree, still, a prototype or test prevents embarrassing mistakes.
16. You cannot create an effective system by building its parts sequentially.
17. Consistency of technologies is overrated. Even if you're right, changing your mind when needed will require convincing everybody and changing things company-wide.
18. Consistency in architecture is underrated. You won't benefit from any desirable system-wide properties, unless you design your whole system to achieve these.
19. Products, people, technologies, processes, incentives, and company structure are interdependent.
20. The cost (effort, risk) involved in modifying software depends super-linearly on how many possibilities you need to take into account.
21. A strongly typed domain model makes undesired possibilities impossible.
22. Software architecture is about limiting the degrees of freedom involved in moving and storing information.
23. Every employee should want to do their best, and to continuously improve their best.
24. Team members should vary in strengths, backgrounds, and experience, but should have compatible belief systems.
25. The tell-sign of a high-performing team is the pride they take in their craftsmanship.
26. People should be passionate and have strong opinions. Bad opinions can be fixed, but a lack of passion cannot.
27. Teams should be co-located: either all sitting closely together most days, or all entirely remote.
28. The teams of product developers should make most decisions: about the product, and about their ways of working. Push authority to where information is.
29. The most important job for an executive is to form a core group of high performers, and to remove people that would endanger this.
30. Early feedback prevents waste.
31. You cannot inspect quality into a product.
32. The 10x developer is a myth. When you factor in how bad decisions compound over time, a 10x factor isn't even near the difference between bad and great.
33. Fewer and better people will run circles around many more worse employees.
34. Staffing the best people you can find is the single most important thing for any company.
35. Nobody cares about your business and its customers. Everybody's in for themselves. The best people you can hire are those who are in for the fun of solving problems together. Align the incentives so that what's best for the company is what's best for the employee.
36. Growth is important, but development equally so. Growth is about doing more, in terms of users, revenue, etc. Development is about becoming better at the activities involved in operating the company.
37. Storing the history of changes, as opposed to the state itself, yields amazing possibilities.
38. The number of features and bugs is irrelevant. One great feature might make your product. One bad bug can kill your company. Most features and bugs won't move the needle.
39. At some point, quantity becomes quality. Many small issues eventually give your customers the impression of a poor product.
40. Bureaucracy kills. Stay lean, keep things flat and collaborative, ensure every requirement comes with the name of the person behind it. Needs must be met, but the suggested ways of meeting those needs do not need to be observed.
41. The job of management is to ensure that your system of work is effective. This requires an intimate understanding of both how the work works, and of how it should work.
42. Management by objectives is a travesty. Replace it with management by means.
43. Executives, managers, and product developers have different jobs. Use clear boundaries to who's responsible for a decision. Avoid splitting your company into people who think and people who do.
44. Experts working outside a team should be advisors. Advisors are not decision-makers. The authority should remain with the team getting the advice. Including architecture, security, product management, design, etc.
45. When people capable of doing the thing disagree with people who wouldn't be capable themselves, the former should have authority.
46. Everything is possible, unless it violates the laws of physics. Some things can be prohibitively expensive, or undesirable.
47. When designing something, start from the desired outcomes, and walk back to the technologies and the approaches. Don't decide whether to turn left or right without knowing how that decision fits with your travel plan.
48. Your fight is against entropy. Do nothing, and things will get worse. Order and desired states require a lot of active effort. Chaos and disorder are the natural state of things.
49. 

[//]: # (TODO)

# Parting words

[//]: # (TODO)

I wrote down quite a few organizational principles in [a previous article](https://sollecitom.github.io/software-product-development-blog/posts/2023/2023-11-16-organizational-principles-for-effectiveness/). These principles derive from my current belief system, so they won't resonate if you hold a different set of beliefs.