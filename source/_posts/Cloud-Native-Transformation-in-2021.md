title: Cloud Native Transformation in 2021
date: 2021-07-18 18:50:03
tags:
 - cloud
 - native
 - platform
 - adoption
 - framework
 - functions
 - paas
 - choice
category: public-cloud
---

6 years ago I sat around with a number of esteemed colleagues chewing the fat about the next big tech hyper-curve. After a few weary years delivering and supporting DevOps cookbooks in production there had to be a simpler way. Some of the PaaS players claimed they’d worked it out: speak the language of the developer, git push (provider) (environment) and off the deployment went, backed by postgresql and redis. This opinionated approach had been around for years and for many devs, that was enough.

But for those that needed control for security, compliance or performance reasons, these PaaS offerings were seemingly not enough. For many businesses the VM was still king and the dislodgement of its royal status inevitable but slow.

At the same time, containers with thanks to Docker’s user friendly interface had taken off. Build once, run anywhere was the moniker, typically true. But to truly build repeatable environments was hard - the toughest challenge the federation of dev and ops knowledge - train one or train all? This became evident by the low rate of adoption of the technology in production throughout the mid-late 10s.

Whilst easy to fire a process with a container, stitching processes together is hard. Networking and discovery tools were evolving at a rate of knots, and keeping abreast of changes was itself laborious. Kubernetes, Mesosphere and Swarm were each orchestration options on top of the container interface to weave the underlying fabric and make containers easier to consume at scale.

Let us not forget serverless. It gained traction in the later 2010s and remains a viable option for microservice architectures, arguably providing devs with greater agilty. Stiching these services together would now require a service bus and other challenges arose such as avoiding cold starts and vendor lock-in.

Fast forward to the 2020’s and many of these challenges have solutions but still are challenging. The hyperscale public cloud providers drive an al-a-carte for cloud deployment at cloud scale. The plethora of landing zone and networking options means it’s okay to select multiple as-a-service options and integrate private cloud and on premises workloads. That’s on the proviso that a consistent operational baseline approach to governance, security and compliance is in place. Each hyperscaler tells the tale of a Cloud Adoption Framework, key tenets being tagging (establishing a resource taxonomy), cost management, policy, identity and security.

There continue to be millions of applications running as monoliths, bucking the hype and trend. As many businesses have found, it's okay to rely on simple structured code broken into domain-specific engines. However as teams scale in size or different teams take on responsibility for different functional domains, distributed, hetrogeneous services begin to make sense. A reasonable number of supportable, maintainable, traceable services. Interface contracts in the form of RESTful APIs form the glue between subsystems and testability of these APIs becomes paramount.

In 2021 the al-a-carte of public cloud is incredibly powerful. However, part of growing and developing a software team today is taming the beast that is cloud and choosing what makes the sense, rather than adopting the latest and greatest. The finance team are there to keep you in check. When we focus on the customer and business outcomes, technology choices follow suit.