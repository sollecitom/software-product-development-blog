---
title: "To modularize or not to modularize, that is the question!"
categories: ["architecture", "systems-thinking"]
tags: ["modularity", "scaling", "reuse", "asymmetries", "architecture"]
date: 2023-07-21T17:30:00
published: true
---

_Why are we talking about modules?_

Because we want to scale, and if we don't modularize we won't be able to scale.

_Mmm, but wait a minute, there are giant companies that don't use modules, so we can scale without them!_

Scaling doesn't mean becoming bigger and bigger, kind of the opposite of that.

_What about microservices though? Aren't those kind of modules? Don't they allow to re-use code?_

Nope. They don't. That's why very few companies can re-use the capabilities they develop and achieve scaling.
<!--end_excerpt-->

# What “scaling” means

## Not becoming bigger

_So what does “scaling” means? How does it not mean becoming bigger?!_

Scaling means achieving more and more outcomes, without increasing costs and efforts as much.

_Mmm, can you elaborate?_

Of course! Imagine you create a new company, you launch some products, something sticks, and you make some profits.

_OK, so what?_

You might be tempted to say, hey, if we have 5 teams that make 2 products, and that makes us £1M a year in profit, if we get to 10 teams and 4 products, then we'll make £2M a year in profit. We need to scale!

_Isn't that true?_

Well, at best that would be a very inefficient way of growing, but in practice it never works.

_Why not?_

It's a long story. As an example, the new products you launch might not be as profitable. Or the new features you add to your existing products might not improve your profitability or market share, or at least not as much as it'd take to justify your efforts to add these.

_But we have a great product function, surely we can tackle these issues._

Perhaps, yeah, but there's a more fundamental problem. Complexity.

_Complexity?_

Yeah. Basically the effort required to run a company or a system increases super-linearly with its complexity. And size is a good proxy for complexity, for both companies and
systems.

_What are you saying?_

That the more people you have, the more effort you need to run a company, and this grows faster than the number of people, so your capacity shrinks.

_Mmm, capacity? What do you mean?_

The people you hire in a company generate capacity, and you use capacity to produce outputs. These outputs, if you're lucky, result in outcomes.

_Ah, gotcha, I get what capacity is, it's our ability to do stuff. But what do you mean it shrinks as we add people._

It does, unfortunately. A company of 100 requires more effort to run than 5 times the effort a 20-people company needs.

_Really? Why?_

Many reasons. Management hierarchies become longer, communication slows down, nobody has the full context anymore, you need more processes, more tools, more controls, etc. So the capacity you get from people diminishes (because of diluted culture, processes, controls,
etc.), you spend more of that capacity to run the company (implementing controls, running tools, managing people, etc.), and your outputs don't translate to outcomes as much (looser alignment, features nobody wanted, etc.).

_Okay, makes sense. I actually think we suffer from this now! But what's the alternative really?_

## But achieving more with less

The whole idea of scaling is about achieving more without increasing capacity as much.

_So are you saying we could achieve more with the same capacity, meaning the same number of people?_

Yes! And every company needs to achieve this by the way!

_So we won't increase our capacity?_

Oh no, we will increase it, but by working better, rather than by hiring more.

_But will that be enough?_

It might, or it might not, but capacity is not the whole picture. How you use capacity matters a lot.

_What do you mean?_

Capacity is how much effort you can exert, but outcomes depends on how much effort outputs take, and how much these outputs contribute to outcomes.

_Efficiency and effectiveness?_

Exactly! Doing the thing right and doing the right thing.

_But doesn't efficiency come from having more capacity?_

No. It's about requiring less effort to achieve an output.

_Do you mean working smarter?_

Pretty much. Choosing high-leverage activities and outputs, and ensuring these outputs translate to outcomes.

_Sounds great, but what does it mean in practice?_

It means identifying asymmetrical opportunities, and pursuing those.

_Not sure I follow..._

Among the many things we could do, some of them contribute to outcomes considerably more than the effort they require.

_Ah! Being smart about what we work on, and ensuring we always work on the most valuable things!_

Yes, but also making sure the way we build things allows us to reduce the effort required to build other things in the future.

_You lost me again._

When we build something, say a software product, depending on how we build it, this will have an impact on its operating effort, and it might or might not allow us to re-use this capability in future products and features that we might build.

# Companies re-use very little

_This sounds very theoretical, what about an example?_

Of course. Imagine you work for a very large company, like a super bank with more than 300k employees.

_Woah, 300k! That'd be crazy!_

Indeed! You can easily imagine that 300k employees build many things every year, even after the whole capacity discussion above.

_Oh yeah, they can build whatever really!_

And they do. They build a lot of things, including things they already have.

_Wait, what? They wouldn't do that, would they?_

They do! All the time! They might have 7 or 8 implementations of the same thing, that all do pretty much the same thing.

_Why would they do that?_

Many reasons. Poor visibility, low trust, and dependencies.

_So they don't know about these existing implementations, and they don't trust them?_

Yeah, but that's only part of the problem, dependencies are a big deal.

## Dependencies prevent re-using things

_What about dependencies? What do you mean?_

Dependencies prevent you from re-using the things you have already built. Imagine you want a banana, and as you pull the banana, it pulls a gorilla, which in turns pulls a jungle.

_Are you even serious now?_

It's a silly example, but it works well. You never wanted a gorilla, nor a jungle, but if you want the banana, that's what the banana comes with.

_Alright, sure, so what can I do?_

Well, you might give up and deal with the gorilla and the jungle.

_That's crazy! No way!_

And that's why usually teams end up re-implementing functionality that already exists. Because of its unwanted dependencies.

_Still better than getting the gorilla and the jungle!_

Yeah, but redoing a lot of things many times over and maintaining them is crazy in terms of cost and effort.

_I can imagine! Their annual technology budget must be insane! But isn't this a problem all companies have?_

To an extent, yes, it is, although this is a much bigger issue for large companies. Small companies don't usually have many products and software systems, so the amount of re-use is limited anyway. Re-use is still important of course, but this problem scales super-linearly with the size of a company, unfortunately.

_Right. So what's the alternative in large companies?_

Modularity.

## Microservices don't enable re-use

_You mean microservices? I build a microservice, any service can call it, and we achieve re-use._

No. It's not that simple. It works in theory but not in practice. Microservices are not modifiable or extensible, and you accumulate concentration risk by calling microservices as part of your workflows.

_Once again, I think an example would help._

Oh yeah, sure. Let's say you want to launch a product aimed at increasing retention for businesses. A shop issues reward points, and customers can spend these reward points across different shops. You decide that issuing virtual debit cards that spend these points would be amazing for your users.
So, to recap:
1. You issue virtual debit cards.
2. These virtual debit cards can only be accepted in some shops.
3. These virtual debit cards use reward points that the shops issue.
4. These virtual debit cards look like cards, but don't go through the VISA or MasterCard schemes, just over HTTP.

_Okay..._

And let's imagine that you already have card issuance, card processing, and core banking accounts.

_That's right, it doesn't seem like this should take much effort._

Well, it shouldn't, but it's not that simple.

_Why?_

Well, first of all our use case is similar to a normal card transaction, but also different. The way we credit accounts is different. We don't need statements. Statements cannot even be produced in this case, as they're legal documents. We probably don't need to call a 3rd party vendor to check every transaction for sanction lists restrictions in this case. The transactions don't reach us from VISA or MasterCard, but over HTTP.

_Oh yeah, I see what you mean. But we'd still need to check for fraud attempts, wouldn't we?_

Well, probably, yeah. Can you see that this is a workflow that's very similar to what is there, but we cannot just call a microservice and have our transaction processed?

_Totally, it would never work._

And even if we could, we wouldn't want these marketing-related traffic to be served by the same systems we use for workloads that are way more serious, would be?

_Of course, that would be dangerous. This traffic could slow things down or create issues for our real transactions. Imagine how pissed off our customers would be!_

Precisely. And by calling a service outside our boundaries, we need to think about different authentication and authorization mechanisms, how we're going to handle observability, and quite a few other operational aspects.

_Yeah, imagine a support rota in such a system!_

Indeed! That'd would be hard, figuring out which team to wake up for what, etc.

_And it would mean you have dependencies across teams, so if we need something from the card issuance service, we need to ask the team responsible for it to build it._

Yeah, and they might have other priorities.

_Bummer! What can we do instead if microservices don't help here?_

# Modularity = an operating system + self-contained modules

You need an operating system, and composable modules that are self-contained.

_An operating system? Do you mean like Windows?_

Haha, no, it's an analogy. You need something that:
1. Allows users to browse which functionality we have already.
2. Allows users to understand how a piece of functionality works.
3. Standardizes identity, authentication, authorization, logging, monitoring, and other operational concerns.
4. Allows users to provision workflows dynamically, on demand, in a self-service fashion.
5. Lets users configure and combine various pieces of functionality into new products.

_Wait, isn't this what a Cloud provider does?_

Well, a Cloud provider:
1. Allows users to browse which infrastructure resources and software services are available.
2. Allows users to understand how an infrastructure resource or software service works.
3. Standardizes identity, authentication, authorization, logging, monitoring, and other operational concerns.
4. Allows users to provision infrastructure resources and software services dynamically, on demand, in a self-service fashion.

_Sounds very similar to me._

Indeed! And the early Cloud providers were born to tackle these issues within the companies that created them! But there is a fundamental difference. Cloud providers provision individual resources and services, leaving you with the effort of configuring how things interact. Say you provision a database and launch a Docker image on ECS, for a microservice that reads from the database...

_Okay..._

It's your responsibility to allow the microservice to communicate with the database, to create and inject credentials, to open an ingress route that lets HTTP requests reach the microservice.

_That's right, that's how Cloud providers work. How is this operating system any different?_

The level of abstraction is different. The modules in our case are more coarse-grained than the ones Cloud providers offer, and we also need to support packaged workflows that use more than 1 module.

_So say the gateway, the microservice, and the database are part of the same module?_

Pretty much.

_But wouldn't that mean we have dependencies, like the microservice depends on the database?_

Oh, no, here we're talking about behaviour dependencies, not infrastructure dependencies.

_What?_

Like, the gorilla is some unwanted business side effect that the banana pulls. It's not an infrastructure dependency. Infrastructure dependencies are good actually, so you don't have to connect the service to the database yourself.

_Makes sense. And how does this help with concentration risk and availability problems?_

By allowing users to import a module into their workflows or products.

_Like importing and deploying this module ourselves, rather than calling an existing module already deployed somewhere?_

Precisely! This way resources and workloads are isolated, and you avoid both problems.

_Nice! And what if I want to change something? If the core accounts module is used as part of the cards processing workflow, we don't want that one, but one that works with rewards points and has no statements. Also, we don't want to screen transactions for issues related to sanctions list, as per our example._

Yeah, that's where dynamic workflows come in. You can have alternative modules for the same workflow step, and import a different module when you want different behaviour.

_Like we'd choose to omit the module responsible for statements in this workflow, but include the fraud checker because we want that behaviour, and replace the VISA and MasterCard connectors with an HTTP-based alternative?_

Exactly! Modules should accept configuration options, and be self-contained, meaning that they shouldn't be aware of other modules, but only of events that can happen system-wide.

## When it comes to modules, ~~size~~ granularity matters

_OK, we want to change what happens based on what's needed, on a case-by-case basis. Now that I think about it, could we not just build something that can behave differently based on what's needed? And then pass configuration options to it? Didn't we just say modules should accept configuration options? Based on configuration, we could produce statements or skip that._

Well, we could, but this approach has many disadvantages over composing self-contained modules.

_Such as?_

Well, here are some:
- Higher complexity for the modules, which would need to behave differently based on configuration values. This is a very significant problem. A module that does 2 things is harder to build, test, release, understand, evolve, and maintain, compared to 2 modules that do 1 thing each. And the increase in complexity is also non-linear, so a module that does 4 things is much harder than 4 modules that do 1 thing each.
- It introduces dependencies on the “supplier” module. So if you need some different/additional behaviour, you now need to evolve an existing module, rather than composing things. This is not only harder, but typically means asking other teams to do this for you.
- It requires modules to be aware of the workflow they're in. Real big issue here. If a module needs to behave differently if another module is in the same workflow, you have workflow-aware modules, so not really modules anymore. Complexity increases significantly, testing becomes incredibly harder.
- Modules that do completely different things based on configuration are harder to understand and to use. A user would need to understand what to enable or disable based on the desired workflow.

_Oh, well, yeah. Like standard Lego blocks, as opposed to configurable and modifiable Lego blocks._

Yeah, and there's more. The coarser the modules, the less the operating system can infer about them.

_What do you mean?_

Let's imagine a product offers an HTTP-based connector, and a Kafka-based connector to ingest data...

_Okay..._

You could implement this product using multiple modules: 1 for the HTTP-based connector, 1 for the Kafka-based connector, 1 for the processor itself, and some more modules for the outputs e.g. webhooks.

_Yeah, makes sense._

But you could also decide to use a single all-in-one module, or even a couple of coarser modules. Let's say you decide to have a single module that allows to ingest data from HTTP and Kafka, using configuration to decide which one you want: HTTP, Kafka, or both.

_Okay..._

Well, in the first case, the HTTP module and the Kafka module would be declared separately, and the operating system would understand what each of them needs in terms of connectivity, security, permissions, etc. In the second case, if you bundle these capabilities into a single module, the operating system wouldn't be able to understand this, because the distinction of which capability is provided would be determined at runtime, based on the configuration option. So the operating system would need to allow the union set of the connectivity, security, and permissions requirements to this coarser module, even if in a given use case some of these permissions might not be needed at all.

_Ouch, that doesn't sound great._

Well, because it isn't! And if you were to import such a module, you'd have to give it all these permissions in any case. Imagine you'd like to use this module to allow Kafka data ingestion, you'd end up opening HTTP routes even if you don't want HTTP data ingestion.

_Yeah, that's definitely a problem._

It gets even worse. By declaring fine-grained modules, you allow the operating system to reason about changes. If you bundle things into multi-purpose modules, you miss out on this.

_Meaning?_

Meaning, as an example, that if a module is declared as stateful, and one as stateless, the operating system could allow to remove the latter without worrying about data retention. If you bundle them into a module that does either, based on a flag, even if you choose the stateless behaviour, this stays within this larger module, so the operating system would now be forced to assume that it could require data retention handling when you unsubscribe from it.

_Ah yeah, of course, the operating system wouldn't know in this case!_

# Simplicity = ~~fewer moving parts~~ more of the same

Many people struggle with the concept of simplicity. They tend to say "keep it simple" every time they don't understand something or instinctively disagree with it. When they see a system made of many parts, they call that complicated.

_Isn't that right? Like the fewer the parts the simpler something is?_

Not really. Simplicity means "more of the same".

_Here we go again, what do you mean?_

Simplicity is not about quantity, but quality. Many simple modules produce simpler systems than the ones you get by using fewer but more complicated modules.

_An examples?_

Oh, examples are everywhere. Think about building a 30-stories skyscraper, as opposed to building 30 1-story houses. Which one is simpler?

_Mmm..._

How about a bridge? Is it simpler to produce a 200m-long composite bridge made of 20 10m sections, or a single-piece 200m-long bridge?

_I see what you mean._

Humanity was able to produce large systems a very long time ago, by composing a large number of simple modules. Only very recently we were capable of producing more complicated modules.