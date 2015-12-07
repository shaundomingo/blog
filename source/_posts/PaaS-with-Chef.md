title: Building a PaaS with Chef
date: 2015-12-07 08:35:35
tags:
 - chef
 - paas
 - platform
category: PaaS
---

Over the last four years I have been fortunate to be part of a cloud computing company that's thrown the kitchen sink at *cloud* innovation. For us the differentiator was making it crazy easy to deploy and maintain an app. This article is a personal reflection on the consideration and use of Chef in a Platform-as-a-Service (PaaS) to which I was a key contributor.

Identifying the key functional and non-functional requirements is the first step in the journey of product development. To formulate this list, you need to talk to lots of people. How will your customer deploy, update, rollback and debug their service? For a PaaS this forms the key interaction contract between you and a user.

Waiting for anything in this game is pain. One fundamental Chef feature that will hold you back in building your PaaS: idempotency. Don't get me wrong idempotency is a necessity. You need the confidence that you'll get the same resultant state each time you apply a set of resources based on a given configuration. Chef's done a great job at ensuring you have access to pre and post-processors to help skip as much processing as possible (c.f. not_ifs and only_ifs).

If idempotency is so good, why is it so bad? When you're talking about software, applying the same instructions over and over again is costly. I witnessed the evolution of a primary wrapper cookbook that leveraged over 20 community cookbooks to do its thing. It would take a convergence 30 seconds to figure out that there was nothing at all to do. This is bad. If a convergence is triggered with the view of deploying a service the application LWRP isn't engaged until the end of the run ... you have to wait at least 25 to 30 seconds for the activity you care about to occur. Time is money.

Why does it take that long? To answer that question you need to consider the componentary required to drive a PaaS. How would you leverage Chef to perform the following functions? Would you at all?

* Provisioning / Virtualisation
* Orchestration
* Multi-tenancy / isolation
* Package management
* OS Updates / Patching
* Management (Credentials / logging)
* Monitoring
* User Workflow and integration into 3rd party ecosystems
* Application deployment & database migrations

So what are the options? You could carefully craft your cookbooks to only execute the bits you care about at any point in time, but that goes against the grain of Chef. You could update the runlist of a node or nodes prior to executing the bit you care about, but at some point you're going to hit an exception and the node won't return to the starting state.

The answer in my view is fairly simple but in reality difficult to tackle. Choose the right tool for the right job. Provisioning is best handled by platform specific APIs. Orchestration can be handled by any number of distributed, coordination systems. And of course you should consider containers, they take away the pain of OS-level package management.
