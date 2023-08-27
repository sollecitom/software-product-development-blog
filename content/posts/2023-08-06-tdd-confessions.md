---
title: "Confessions of a TDD fanboy"
date: 2023-08-06T16:00
categories: [ "technical practices", "agile" ]
tags: [ "test-driven development", "design", "object-oriented programming" ]
published: true
---

Test-Driven Development (TDD) is arguably one of the most polarizing and misunderstood approaches in software development. It's love it or hate it.

Let's have a look at TDD and why it provokes such strong reactions. This is going to piss some people off...
<!--end_excerpt-->

# So what is Test-Driven Development?

Put down in words by [Kent Beck](https://en.wikipedia.org/wiki/Kent_Beck) in 2003, Test-Driven Development is a software development process relying on tests to drive the implementation of the code.

The approach adopts the following sequence to introduce changes in behaviour:

## 1. Add a new test

Start by writing a new test case.

- 1 test case, not a whole suite, not all requirements upfront.
- These tests are not unit tests about a specific type. There are collaborative tests, where different types and functions interact to achieve a result. A bad name would be `ShoppingCartTest`, while a good name would be `ShoppingExperienceTests`.
- If you're starting a project or a new module, nothing will even compile at first, and that's fine. Write things as you'd want them, and then make it compile.
- Not talking about BDD here. Tests should be expressed in your main programming language, without a DSL.
- Start from the assertion, thinking about what needs to happen. Try to design the test so that there's a single assertion.
- It's important to write the test so that it provides an example of how the code should be used in that case. No cryptic test functions to template test cases.

## 2. Run all tests. The new test should fail for the expected reasons

Then run all the tests, and confirm the new test case is failing for the expected reasons.

- This should be fast.
  - Minimize the number of tests that interact with IO.
  - A smart build system e.g. Gradle can greatly help by only running tests for the modules that actually changed.
  - Adopt a modular component-level software architecture e.g. Hexagonal Architecture to achieve crisp module boundaries.
- Don't skip the part where you make the new test fail: it prevents you from assuming things work in presence of a mistake in the test logic or in the implementation.

## 3. Write the simplest code that passes the new test

Then write an implementation that passes the new test.

- Don't worry too much about code structure at this stage.
- Once the test passes, changing the structure will be safer and faster.
- Don't get obsessed with the word "simplest" here.
  - Some folks would return stubbed data to make the test pass, just to then change it.
  - Apply any good design patterns at this stage as well (don't make things mutable, etc.).
  - Just don't focus much on finding the right abstractions for the internal code.

## 4. All tests should now pass

Run all tests again, and confirm you haven't caused any other test to fail. If you did, back to #3.

- Once again, this should be fast.
- Time to commit after all tests pass.

## 5. Refactor as needed, using tests after each refactoring to ensure that functionality is preserved

Refactoring means changing the structure of the code without changing its behaviour. Improve the structure of the implementation, running all tests every time to confirm you haven't changed the behaviour.

- Use small steps here.
- Run all tests after each step, not only the test you're using to drive the implementation.
- Commit after each step.

# So what's to love?

So what's the big deal with Test-Driven Development? Why might this be a good idea?

Many people focus on the tests, claiming you could always write them later, but TDD isn't about testing. TDD is a software development process: its goal is to drive code design and facilitate the implementation. The tests you write are a desirable side effect, not the goal.

## Backward design

By writing a new test case first, you focus more on the requirement or desired results. This helps because your work is more intentional, rather than building things and figuring out why later.

Also, you write the code like you'd want to use it, to make your own life easy while writing the test, and to create a readable example of how the code would be used to achieve something. This is a tremendous difference, as how you want the code to behave drives your implementation choices: types, names, functions, arguments, etc. Without this is hard to come up with good design upfront, as you don't visualize the result and the alternatives.

## Many more smaller steps

By cycling through the steps quickly and in small steps, you minimize risk. The fact that you commit often, and that you increment the expected behaviour 1 test at a time means that undoing something is always quick and painless.

Overall it's just harder to get things wrong, and TDD offers frequent rewards, when all tests are green and you commit. It offers a sense of progress and achievement.

It's kind of fun really, far from the hair-pulling debugging some people are used to.

## It's fast!

This is very surprising for most people, and a counter-intuitive fact: Test-Driven Development is fast! The focus on the requirements, structuring the code well, decomposing the problem, and having tests to help you find issues earlier, all ultimately result in increased speed.

Producing a correct implementation is quicker, not to mention how quicker it is compared to producing a correct implementation AND writing the tests for it.

## The code ends up of higher quality

TDD won't turn you into a great software designer if you're not, but it'll likely bring out the best in you in this sense.

Writing the test case upfront like an example of how the code should be used:
- Forces you to think about its usage.
- Forces you to write code that needs to work elegantly in at least 2 places (in the tests, and in the main application).
- Produces crisp abstractions, as they are written before any thinking about the implementation, and thus are much less likely to end up leaking implementation details.
- Forces you to write testable code. This is not only good for testing. Code is easy to test when it's decoupled and well-modularized. So if you're forced to write testable code, you get low coupling and effective modules.
- Results in a stronger and more effective domain model. This is a result of aiming for readable code, and of having to make your life easier by reducing the amount of things to cover, by leveraging the compiler and introducing self-validating types. Separating API and implementation is also easier, as you design these during different steps of the TDD cycle.

## It produces good tests as a side effect

Yeah, let's face it, TDD is not about testing but the tests it produces are a very nice side effect.

The tests produced are great, because:

- They're executable examples, acting as both documentation and regression tests. As they're written upfront, they tend to be readable and self-explanatory.
- They are black-box, focusing on contracts and behaviour, rather than on structure and specific types. The result is that you can change the internal structure without your tests getting broken in the process. A far cry from unit tests here.
- They offer a high degree of confidence. By adding behaviour incrementally you progressively improve the confidence in your tests, catching problems early, and refining their effectiveness.

# So what's to hate?

For all the reasons above, I firmly believe that Test-Driven Development is a great approach to producing high quality software that works, quickly, while having fun. Mind that I'm not a consultant. I write code as a part of my job, and I find TDD invaluable. It brings out the best in me, and helps me get better and better. I'm gutted that I learned TDD late, and I had to do this "by myself", through books, courses, and videos.

And yet many people are very vocal about their hate and distrust for Test-Driven Development? Why? Well, I wouldn't really know to be honest. But I can guess.

There's an element of wanting to belong to a community, so some folks attack things to feel like they belong with other like-minded folks. Some others had bad experiences from meeting fanatics or people who claimed to do TDD but showed something else.

Some other people, simply put, don't value code structure at all. They think their job is about writing code that works, and get satisfaction from being "clever" with algorithms and approaches.

The reality is that in software product development code quality matters more than code correctness. I'd take high-quality incorrect code over low-quality correct and performant code any day.

Why? Because the job isn't about making things work. Except for very few companies, making things work is trivial. Others have done it already. There are books, blog posts, videos, examples, and tutorials.

In most contexts, implementing a sorting algorithm or inverting a linked list manually should be a fireable offense. Your job is to develop a product that does the job well for your customers, under their circumstances. The less code involved, the better. 

And yet some folks buy this myth of the smart lone wolf developer, and pride themselves in their ability to endure long hours of debugging convoluted and obscure logic that solves hard problems. It's people who spend time on LeetCode, or who post unreadable crappy code, asking other people to explain what the console prints. It's people who ask candidates in interviews to manually sort things, or to design Twitter in 1 hour.

Except for the fact that LeetCode "problems" are not problems, but exercises. Exercises are always environment-free. You have to invert a binary tree, or sort something. When there are constrains, they're made up, like you cannot use some functions from the standard library.

Problems, on the other hand, never come isolated, they have interdependencies with other problems, and they're very context-specific. No company ever went out of business because they couldn't solve an exercise.

The difficult part of software product development is figuring out how to deliver value to users while not imploding from increasing entropy. It's keeping the codebase understandable and easy to change. It's not taking 3 steps forward and 2 steps back. It's being able to contribute to a codebase with 50 developers working in teams. It's not ending up taking a month for something that used to take 1 week the year before.

The best thing about Test-Driven Development is that it removes the drama and the heroics from this profession. It's a methodical approach that removes the need to get things right the first time, producing the ability to safely and quickly iterate without regressions until things work and are structured effectively.

And that's what the LeetCode fanboys can't stomach. It's like pulling the rug from under their feet.

"How dare you claim that my hand-made red-black tree implementation isn't going to be a competitive advantage for my company"?

"How dare you claim that my untested, untestable, cryptic, hard to change minefield of an implementation could ever not be perfect"?

And there you have it folks, some people hate TDD because they don't understand what the job is about. They don't consider it a good solution, because they're not aware of the problem.