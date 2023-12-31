---
title: "My belief system for software product development"
categories: [ "system-thinking" ]
tags: [ "software-development", "organization-design", "effectiveness", "management", "belief-system" ]
date: 2023-12-24T05:00:00
draft: false
---

Running a software product development company is complex. People, processes, products, technologies, and operations are all crucially important, and interdependent.

You need to identify a job people struggle with, create a product that addresses it well, price and market it appropriately, defend it against competitors, and react to market changes, all while making a profit.

Additionally, software is a highly abstract medium, meaning that common-sense rarely applies, so that what's effective is often counter-intuitive.

So it's perhaps unsurprising that software companies rarely know how to structure themselves and how to operate, leading to many alternative approaches. Startups copy practices from famous businesses, and there's an abundance of consultants and advisors. Commercial frameworks like SAFe or Scrum promise executives that they won't have to think, and that merely applying the framework will produce great results.

And yet, reality isn't linear or clear-cut. What works in a company won't likely work elsewhere. A practice that's effective in a company with 30 employees will almost surely not work when the same company has 100 employees. Systems are full of interdependencies and nonlinearities, so you cannot improve your sales without changing your product and your marketing, and you cannot change who you hire without changing how you work.

So what should a company do when common sense doesn't work, frameworks aren't effective, and copying what famous businesses are doing won't take you far?

The answer is that you should think deep and write down your belief system, and then use it to orient yourself in this highly complex environment. A belief system is a set of fundamental beliefs that shapes the way you perceive reality and links causes to consequences.

The various beliefs that are part of your belief system shouldn't conflict. If your beliefs are in conflict, question your current beliefs, until the conflict disappears.

What follows are some of my beliefs, when it comes to software product development. When I say "my belief", I mean that I stand by them, not that I came up with them myself. They served me well over the years, but I keep evolving them, and you shouldn't take them at face value.

The important thing is to:

1. Write down what you currently believe, rather than what you'd like to believe.
2. Assess the coherency of your belief system.
3. Check each practice, process, and approach you use or are considering using against your beliefs.
4. Reassess your belief system every time you experience something that your belief system struggles to explain. Don't discount reality if it clashes with your mental model. Discount your mental model if it clashes with reality.

# Holistic

1. Products, people, technologies, processes, incentives, and company structure are interdependent. You shouldn't design them independently.
2. We're all going to be wrong a lot. Remember you can still be wrong, even when you're dead sure you're right. Keep an open mind.
3. Everything is possible, unless it violates the laws of physics. Some things can be prohibitively expensive, or undesirable.
4. When designing something, start from the desired outcomes, and walk back to the technologies and the approaches. Don't decide whether to turn left or right without knowing how that decision fits with your travel plan.
5. Your fight is against entropy. Do nothing, and things will get worse. Order and desired states require a lot of active effort. Chaos and disorder are the natural state of things.
6. The most important job for an executive is to form a core group of high performers, and to remove people that would endanger this.
7. Growth is important, but development equally so. Growth is about doing more, in terms of users, revenue, etc. Development is about becoming better at the activities involved in operating the company.
8. Trust and verify. Treat people like adults. Allow people to do mistakes. Get rid of people who abuse your trust or who keep making the same mistakes. Do not restrict everybody's freedom because a few people abused that freedom.
9. You cannot inspect quality into a product or a system. You need to build quality in, throughout the lifecycle.
10. At some point, quantity becomes quality. Many small issues eventually give your customers the impression of a poor product.
11. If you have formal authority over other people, how good you are at your job can be assessed by how infrequently you have to resort to formal authority.
12. Nobody cares about your business and its customers. Everybody's in for themselves. The best people you can hire are those who are in for the fun of solving problems together. Align the incentives so that what's best for the company is what's best for the employee.
13. Resist the lure of metrics and KPIs. Indicators are useful, but should never become targets. Running a company without metrics and KPIs can be hard. Running a company primarily by metrics and KPIs is usually a disaster. Many important things are not measurable.

# Processes

1. Bureaucracy kills. Stay lean, keep things flat and collaborative, ensure that every requirement comes with the name of the person behind it. Needs should be met, but the suggested ways of meeting those needs does not need to be observed.
2. The job of management is to ensure that your system of work is effective. This requires an intimate understanding of both how the work works, and of how it should work. Management by objectives is a travesty. Replace it with management by means.
3. Executives, managers, and product developers have different jobs. Use clear boundaries for decision-making. Avoid splitting your company into people who think and people who do.
4. Push authority information, rather than information to authority.
5. The teams of product developers should make most decisions: about the product, and about their ways of working.
6. Whenever people disagree, a prototype or test is the right way forward. Whenever people agree, still, a prototype or test prevents embarrassing mistakes.
7. The coordination effort required in a team, department, or company increases super-linearly with its number of people.
8. Early feedback prevents waste.
9. The unit of work allocation should always be a team.
10. Teams should abstract who's working on what, and be resilient to holidays, illness, etc.
11. A team should be able to work on anything the company needs.
12. Experts working outside a team should be advisors. Advisors are not decision-makers. The authority should remain with the team getting the advice. Including architecture, security, product management, design, etc.
13. When people capable of doing the thing disagree with people who wouldn't be capable themselves, the former should have authority.

# Product

1. Customers hire your product to do a job they would otherwise attempt to do in other ways. Nobody cares about your product, people care about the job your product does for them.
2. Product development is about finding a good job to be done, and tailoring your product to meet the customers' needs well, given the circumstances your users find themselves in.
3. A software product is a set of promises, not a set of features. A product is still the same product if the features evolve, but not if the needs it meets changes.
4. The biggest risk for a new company is solving a problem not worth solving.
5. Behind every bad idea that were people thinking it was an excellent idea. Write down your assumptions, and test these assumptions, before fully committing. Finding evidence should rarely require building things.
6. Being a big fish in a small pond is better than being a small fish in a big pond. The right starting pond can be expanded after you outgrow it.
7. People make emotional rather than rational decisions. Their perception of your company, their job, your product, and the competition will determine their behavior. Positioning is the battle for the mind of your prospects.
8. The number of features and bugs is irrelevant. One great feature might make your product. One bad bug can kill your company. Most features and bugs won't move the needle.

# Technology

1. A software system is not the sum of its parts: every time there's a new requirement, you need to modify the software to meet this new requirement plus all the previous ones.
2. You cannot create an effective system by building its parts sequentially.
3. Consistency of technologies is overrated. Even if you're right when you choose something, changing your mind when needed will require convincing everybody and changing things company-wide.
4. Consistency in architecture is underrated. You won't benefit from any desirable system-wide properties, unless you design your whole system to achieve these.
5. Humans can only keep so many things in their head. Well-designed modules compartmentalize complexity.
6. The cost (effort, risk) involved in modifying a software system depends on its internal quality, which is how well the code is structured.
7. The cost (effort, risk) involved in modifying software depends on how easy it is to understand where to operate the change, and on how contained the change is in terms of testing.
8. The cost of modifying software because of new requirements always ends up trumping the initial cost involved in writing it.
9. The cost (effort, risk) involved in modifying software depends super-linearly on how many possibilities you need to take into account.
10. A strongly typed domain model makes undesired possibilities impossible.
11. Software architecture is about limiting the degrees of freedom involved in moving and storing information.
12. Storing the history of changes, as opposed to storing the state itself, allows amazing options.

# People

1. Staffing the best people you can find is the single most important thing for any company.
2. Every employee should want to do their best, and to continuously improve their best.
3. Team members should vary in strengths, backgrounds, and experience, but should have compatible belief systems.
4. The tell-sign of a high-performing team is the pride they take in their craftsmanship.
5. People should be passionate and have strong opinions. Bad opinions can be fixed, but a lack of passion cannot.
6. Teams should be co-located: either everybody sitting closely together most days, or everyone entirely remote.
7. The 10x developer is a myth. When you factor in how bad decisions compound over time, a 10x factor isn't even near the difference between bad and great.
8. Fewer and better people will run circles around many more worse employees.