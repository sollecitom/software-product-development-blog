


Kent Beck famously stated that you should make the change easy, and then make the easy change. 

The context is code structure and its ability to make the same change either trivial or diabolically complicated. 

And therefore you should change the structure of the code until making the change in behaviour you have in mind is easy, before making that change.

Now, I believe that there are other dimensions involved with this statement, so I want to offer some of my thoughts. 

It all revolves around what easy means, and who it applies to. 

An example is that, by writing a test that exposes showcases the behaviour you want to introduce, you're making it easier for yourself, because you'll know when you'll have caused the effect you intended.

By having a covering test suite that runs fast, you're making it easier because you can quickly tell whether you introduced regressions elsewhere. 

Writing good documentation and producing executable specifications is a way of lowering the difficulty of future changes for both yourself and others.

Working in small steps and introducing canary rollouts with feature flags makes things easier because the changes are safer.

Logging appropriately and producing the right metrics makes it easier to operate the codebase.

Finally, it's also sometimes about your knowledge and understanding. If writing a SQL query sounds like a daunting task, spend one hour to improve your familiarity with SQL. Not only the change will become easier, but you'll have become better at your job. 

I really like "make the change easy, and then make the easy change". It's great advice, and it has a broad range of applications.

What do you think? Makes sense? Do you typically go out of your way to make things easy? If not, why not?
