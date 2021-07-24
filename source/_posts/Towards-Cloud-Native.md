title: Towards Cloud-Native
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
category: cloud
excerpt: Some personal musings about the evolution of cloud-native application development in the 2020s and the role of pragmatism.
---

6 years ago I was chewing the fat over the next tech hype cycle with a few esteemed colleagues. After a couple of weary years delivering and supporting DevOps cookbooks in production there had to be a simpler way. Some of the PaaS players claimed they’d worked it out: speak the language of the developer, git push (provider) (environment) and off the deployment went, backed by postgresql and redis. This opinionated approach had been around for years and for many devs, that was enough.

But for those that needed control of their infrastructural footprint for security, compliance or performance reasons, these PaaS in-a-box offerings were insufficient. Many businesses would continue to crown the Virtual Machine king. The dislodgement of the VM's royal status was inevitable, but it was to be slow. It will remain a core tenet of cloud infrastructure for years to come.

## The container movement

Meanwhile containers, with thanks to Docker’s developer-friendly interface were gaining significant traction. 'Build once, run anywhere' was the moniker. Whilst easy to instantiate a process with a container, stitching processes together is hard. Networking and discovery tools were evolving at a rate of knots, and keeping abreast of changes was laborious. Kubernetes, Mesosphere and Swarm were each orchestration options on top of the container interface to weave the underlying fabric and make containers easier to consume at scale. Kubernetes was soon to win the orchestration race.

## DevOps and SRE

But building repeatable, maintainable environments was hard. The toughest challenge? The federation of dev and ops knowledge. Pushing development teams to think beyond one-off batch scripts, deploying directly from their IDE, and app and infra security. The SRE movement transitioned developers to a world of ports, session affinity, and utilisation impacts on infrastructure knowing they'd be accountable for it in production. Architecting cloud-native applications for scale remains a mystery to most developers today.

## Serverless

Let us not forget serverless. Gaining traction in the later 2010s, serverless remains a viable option for event-based processing, RESTful APIs and microservice architectures, arguably providing greater agilty. As services were becoming increasingly decomposed/fine-grained, stiching these services together would now require a service bus/consolidated ingress point to provide a unified front to consumers. Other challenges arose such as avoiding cold starts and vendor lock-in.

## Spoilt for choice

Fast forward to the 2020’s and many challenges have blueprinted solutions but they are still confronting to solve. It's why the managed service provider and global systems integrator market is booming. The baseline skill demands on an application developer are far greater yet liberating. The public cloud providers drive an al-a-carte model for deployment at scale. The plethora of landing zone and networking options means it’s okay to construct a heterogeneous architecture by way of multiple as-a-service options and hybrid cloud. That’s on the proviso that a consistent operational baseline inclusive of governance, security and compliance has been established and maintained through a centralised cloud center of excellence. Each hyperscaler tells the tale of a Cloud Adoption Framework, key tenets being tagging (establishing a resource taxonomy), cost management, policy, identity and security.

## Fit for purpose

That aside, there continue to be millions of applications running as monoliths, bucking the hype and trend. As many businesses have found, it's okay to rely on simple structured code broken into domain-specific engines. As teams scale in size or different teams take on responsibility for different functional domains, distributed, hetrogeneous services begin to make sense. A reasonable number of supportable, maintainable, traceable services. Interface contracts in the form of RESTful APIs glue subsystems together and the testability of those integrations paramount.

In the 2020s, the al-a-carte of public cloud is incredibly powerful. However, part of growing and developing a software team today is taming the beast that is cloud and choosing what makes sense.

When we focus on customer outcomes, technology choices follow suit.