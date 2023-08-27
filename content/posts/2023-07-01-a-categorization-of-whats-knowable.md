---
title: "A categorization of what's knowable"
date: 2023-07-01T10:30
categories: ["systems-thinking"]
tags: ["knowledge", "information"]
---

We often use different words for what we know, like in data-engineering, information systems, and knowledge workers. But do we really understand their meaning and implications? 
<!--end_excerpt-->

### So what are these categories?

[Russell Ackoff](https://en.wikipedia.org/wiki/Russell_L._Ackoff) used to say and teach that the content of the human mind can be classified into five categories:

1. Data: individual observed phenomena
2. Information: data that's been processed and organized to be useful; provides answers to "who", "what", "where", and "when" questions
3. Knowledge: applied information and data, answers "how" questions
4. Understanding: appreciation of "why"
5. Wisdom: evaluated understanding

#### Data

A data point is a single observed phenomenon. Data has no significance beyond its existence. It doesn't have meaning of itself.

Data is everywhere, with phenomena continuously happening, being observed, and being recorded.

##### Examples

- It's raining.
- The sky is blue.
- There's a drop on blood on the floor.

#### Information

Information is data that's been processed and organized to be useful. Information gives meaning to data, by creating relations between data points, which typically involves tagging, categorizing, and aggregating. Mind that the meaning information gives to data isn't intrinsically useful.

Information needs to be actively produced, by processing data based on a "who", "what", "where", or "when" question, and can be inferred from data e.g. when we produce an average.

##### Examples

- The average height of Italian men is 175 cm.
- Yesterday Bob woke up at 6 a.m., went to the gym at 6.30 a.m., came back home at 8 a.m., went to work at 9 a.m., and came back home at 7 p.m.
- The rainfall in Paris was 641 mm this year.

#### Knowledge

Knowledge is the appropriate collection of information, such that it's intent is to be useful. This hierarchy adopts knowledge as know-how, or skill, rather than knowledge in the sense of the know-that of propositional knowledge.

Knowledge as know-how transforms information into instructions. It makes control of a system possible, in virtue of knowing how the system works. To control a system is to make it work efficiently. Knowledge is gained by analysis, by taking something apart, figuring out how its parts work, and by then putting together the knowledge of the parts into the knowledge of the whole.

This knowledge has useful meaning, but it does not provide for, in and of itself, an integration such as inferring further knowledge. Also, knowledge is deterministic.

##### Examples

- Knowing how Spring Boot works, and thus knowing how to operate Spring Boot.
- Knowing how an electric hob works, what to press to start it, how long to keep it on to make it reach a certain temperature.
- Knowing which underground lines are involved in a journey, where to take the train, where to change, where to hop off.

#### Understanding

Understanding answers "why" questions. Understanding is the process by which people can take knowledge and synthesize new knowledge based on the previously held knowledge. While knowledge copes well with the deterministic, understanding can cope with interpolation and probability.  

The difference between understanding and knowledge is the difference between "learning" and "memorizing". People who understand something can infer new knowledge and adapt it to new situations.

Understanding is intrinsically systemic, as you can never understand why a system works they way it works by analysis, by taking the system apart. The reason a system works the way it works does not reside in the system itself, but in its containing system. You cannot, as an example, understand why a university works the way it works by analyzing how its various parts operate. You need to understand the education system that university is part of to even attempt an answer to this question.

Understanding allows to design a system, rather than merely controlling it and operating it. 

##### Examples

- Knowing why Spring Boot works the way it works, by understanding the JVM ecosystem, its history, Dependency Injection, how companies that hire Java developers operate, which technologies are most common in a JVM environment, Cloud providers, etc.
- Understanding the web ecosystem, and thus being able to infer how a framework new to you e.g. Vue.js works, based on previous knowledge e.g. React.js, Ajax, JSON, jQuery, JavaScript, etc.

#### Wisdom

While the previous levels help you do the thing right, wisdom is about doing the right thing. Wisdom is therefore the process by which we also discern, or judge, between right and wrong, good and bad.

Wisdom allows to design and create effective systems, which produce the desired outcomes.

The wise person must not only possess great understanding and wide appropriate knowledge, but start from the desired outcomes and walk back to the approach, the decisions, and the instruments, using their knowledge and understanding as selection criteria throughout.

Wisdom is developing mental models about what's desirable, what works, what doesn't, and why, about making predictions on reality based on these models, and about discarding or evolving the models when reality proves them wrong.  

##### Examples

- Achieving effective staffing for a company, given that company's size, goals, strategy, industry, and location, but also given the market in the company's country, the belief system of the executives, the budget, the laws and regulations in place, etc.
- Raising children, governing a country, choosing a life-long partner, etc.
- A principled approach to sustainable software product development.

### So what? How does this help me build a company and better products?

Why is important to keep in mind these various categories of what's knowable? Because it's easy to expect unachievable outcomes or focus on the wrong things otherwise.

What's your approach with data and data engineering? Do you use data as a drunk uses a lamppost: for support rather than illumination?

What do you expect from your employees? Knowledge? Or wisdom and understanding? Do you interview accordingly? 

#### Some examples of problematic behaviours

- A "data-driven" strategy. Data asks no questions, but it might give answers to a question when organised and processed correctly. Do you know which questions you're asking your data? How do you know those are the right questions? Data and information are for feedback and model validation only.
- Do you ask information questions when you interview candidates e.g. "What is the name of the property that does this in Spring Boot"? Or do you try and gauge their understanding and wisdom? Why?
- Do you understand the limitations of domain knowledge and of knowing an industry? What is this useful for? What can it not ever be enough for?
- Do you understand the difference between efficiency and effectiveness? About doing the thing right and doing the right thing? Is your company acting accordingly in this sense?
- Do you design your approaches based on the desired end results? Do you walk back from the outcomes to the approaches, the teams, the ways of working, the technologies, etc.? Or do you think doing the thing right will be enough to take you there?