title: The Fascinating Evolution of Application Delivery.
date: 2018-03-24 21:00:00
tags:
  - containers
  - docker
  - kubernetes
  - shipping
---

_Disclaimer: The contents of this post were first delivered by me in a talk for [Macquarie Cloud Services](https://macquariecloudservices.com) at VMWare vForum Sydney in November 2017._

In 2001 VMWare launched the first commercial server virtualisation products VMWare GSX and ESX which paved the way for the standardisation of virtualisation in every enterprise across the globe. Virtualisation became all pervasive, and by the beginning of the public cloud era the perception was if you weren’t virtualising your data centre you were missing significant cost and efficiency benefits.

Fast forward 17 years and we’re still on the search for cost savings and greater scalability. And why wouldn’t we? Virtualisation is great however it hasn’t allowed us to fully utilise our compute resources.
Containers provide a solution to that issue. Containers are light-weight, standalone, portable units. Think of them as isolated application processes running in user space. Containers should only package the code and application dependencies required to run that process ... nothing more.

With containers you achieve greater density because the bloat that comes from installing and running an operating system in line with your application is removed. Instead, containers share the host’s operating system kernel, start instantly and overall use less compute and storage.

Containers take the guess work out of deploying applications. [insert MakeAGIF.com gif here] Containers run based on images defined by ... you. If you are a developer or engineer, you construct a descriptor that declares what a container image should look like. In the instance of Docker, that’s a Dockerfile. That container is typically based on some other container where most of the heavy lifting has been done for you. As you add instructions to the descriptor, a layered filesystem stores the files that correspond to that instruction and records the diff between itself and the previous instruction, allowing you to uniquely address any layer across the persisted container image history.

There are a couple of types of containers, CoreOS’ rkt (CoreOS now acquired by RedHat) and the most popular preference, Docker.

So who’s the target audience here? The truth is, everyone. The power of containers is truly build once, run anywhere. If you’re running Docker, that’s anywhere there is a Docker daemon with access to dependent build images. The old developer mantra "but it works on my machine!"" should now actually be verifiable, if it works locally it will work in every single place that container image has been deployed.

Containers are critical in the deployment of automated continuous integration workflows. They ensure consistency between environments, ensure workloads fire up fast and provide us with higher density across our compute and storage resources.

![Software Delivery - the last 50 years](/images/SoftwareDelivery-TheLast50Years.png)

The process of shipping software has undergone serious transformation in the last 50 years. In the early days we were bound by limitations in computer hardware, but with the advent of the internet, ecommerce and soon after, the cloud, software delivery has increasingly become an concern about automation. The more things are automated, the greater the saving.

## The undeniable future.

So if the deployment of software is already driven by software, where exactly are we going? In many ways the future is shaped by our past.

One thing is certain, "Software is eating the world" (Marc Andreesen). And we’re getting better at creating that software. As humans we are inherently lazy. That plays a big role in our desire for self-improvement and has compelled us to invent ways of generating code and automatically deploy it. It would be hard to deny that software will eventually write software, and self-inform that process.

But until that day we have a challenge, don’t we? We’re on a constant drive to ship code quickly. Why? Because the faster we can release to our customers the more responsive we are perceived to be and resultantly, increased customer satisfaction.

But how do we continuously deploy code without risk or fear? There will always be resistance to consistent change however containerisation and the continuous integration, delivery and deployment model gives a guaranteed way of building, testing, packaging and deploying code across environments in an idempotent way. More about this shortly.

For the first time, containers also allow us to keep an infrastructural building block that’s storable, archiveable and transferrable between environments. This is a win-win for dev and ops, and this allows us to design for platform independence.

*Containers offer platform independence, resource density, isolation, speed and operational simplicity. They are portable and run on any modern operating system.*

I find this evolution fascinating, because our advancement in the container space runs strong parallels to the advancements in tech in the shipping industry over 200 years.

## The nature of what we ship doesn't change, the way we ship does.

It’s no wonder Docker has built it’s brand and nomenclature around the shipping industry. We’ve had thousands of years to learn from a now well-refined industry. So here’s 3 quick facts about the shipping industry you may not have known.

![Software Delivery - the last 50 years](/images/ChangingShippingInfrastructure.png)

<div style="text-align: right">_References [1](https://getsimplebox.com/bit-history-cargo-containers/), [2](http://tinyhouselistingscanada.com/wp-content/uploads/2016/03/shipping-.png), [3](http://www.worldshipping.org/about-the-industry/history-of-containerization/before-container-shipping)._</div>

Take a look at these fine vessels. They are all marvels of their time. Did you know that containerisation of cargo has been around since the 18th century? They became popular because containers could be transferred from one mode of transport to another, including horse drawn carts!

Although relatively slow in today’s terms, technological innovation around the burning of fossil fuels and the improvement in boiler technology meant that steam engines became bigger, faster and more efficient at moving cargo.

Can you draw any parallels to our recent journey through server, storage and networking technology?

## Intermodalism revolutionised the shipping industry.

Intermodalism, a system that is based on the theory that efficiency is vastly improved when the same container can be transported with minimum interruption via different transport modes from an initial place of recept to a final delivery point many kilometres away revolutionised the shipping industry. They could move seamlessly between ships, trucks and trains.

![Intermodalism revolutionised the shipping industry.](/images/Intermodalism.png)
<div style="text-align: right">References: [4 (CC BY-SA 3.0)](https://upload.wikimedia.org/wikipedia/commons/f/f6/LMS_freight_containers_on_lorry_and_rail_wagon_%28CJ_Allen%2C_Steel_Highway%2C_1928%29.jpg), [5](https://commons.wikimedia.org/wiki/File:Intermodal_ship-to-rail_transfer.JPG)</div>

Did you know until the 1970s virtually all goods were shipped around the world loose? Crammed into the holds of old fashioned cargo ships?

Can you relate to that in your environments? If you’re like me you’re reminiscing, oh the days of FTPing files into random cPanel environments.

Again, does this draw any parallels to your journey?

## Globalisation could not have existed without containerisation.

Globalisation could not have existed without containerisation. The advancement in shipping technology brought about worldwide interconnectivity and now 90% of what we buy arrives by ship. And ecommerce has directly played a central role in that development. Studies online say that we’re now shipping in excess of 10 billion tons of cargo a year and that will expand to 23 billion tons by 2060.

![Containerisation enabled globalisation](/images/ContainerisationEnablingGlobalisation.png)

<div style="text-align: right">References: [6](https://people.hofstra.edu/geotrans/eng/ch3en/conc3en/worldcontainertraffic.html), [7](https://www.isl.org/en/news/rwi-isl-container-throughput-index-reaches-new-heights-in-september)</div>

As we look more and more to containerisation in the tech world, the parallels are striking, aren’t they? Containers grant so much power. The intermodal nature of Docker and rkt containers across any type of platform is supremely powerful, particularly in this day of Hybrid IT and Cloud. Containers fire up instantaneously, so the power of being able to scale horizontally in seconds is a huge advantage when you need to respond to traffic demands quickly.

The parallels to our development in software delivery is uncanny. Evidently we’ve learned a lot from the advancements in the shipping industry.

## The nature of what we ship doesn’t have to change, the way we ship should.

![Microservices and Containers](/images/MicroservicesAndContainers.png)

In software, we’ve been breaking down and compartmentalising our applications for years. There’s nothing new here. However, containers have given rise to a new pattern, Microservices. Microservices are effectively self-contained applications that are responsible for a single purpose. They are great because they can maintain their own interface contracts and take on their own release pipeline. This brings challenges too. How will you tag your source and build releases such that they are truly independent? What happens with shared libraries and services, where do they get sourced from?

Regardless of what we’re shipping, containers give us the ability to be much more efficient in deploying our workloads. Pushing to prod shouldn’t be a pain. In fact as much as possible it shouldn’t even be thought of.

The real value of containerisation is realised through true platform independence. The ability to push a workload to any underlying cloud provider. Deploying an App to [Macquarie Cloud Services](https://macquariecloudservices.com) will look and feel similar to deploying to another provider.

## Intermodalism is revolutionising the way we deploy workloads.

![Intermodalism revolutionising workload deployment](/images/IntermodalismAndCICD.png)

Intermodalism has revolutionised the way we deploy workloads. Continuous Integration, i.e. the ability to constantly integrate with a centralised source code management tool, pull some code, automatically run tests thus verifying the build and automatically shipping across multiple environments truly realises the value of containers. You can fire up build slaves in containers, spawn builds from those containers, then ship a container to a registry and automatically deploy out to a container delivery platform of choice. And your choices here are currently quite large – Kubernetes, Docker Swarm, and Rancher.

## Containerisation is enabling standarisation and portability at global-scale.

![Containers enable standardisation and portability](/images/DockerAdoptionHighSaysDatadog.png)

<div style="text-align: right">Reference: [8](https://www.datadoghq.com/docker-adoption/)</div>

While containers in the shipping industry were a massive enabler for globalisation, containers in the IT industry are evidently enabling agility in small business all the way through to the enterprise. Data dog HQ a company that provides monitoring and analytics, crunches the numbers over their installbase every year. They’ve seen incredible growth over the last 24 months. And for the first time they’re seeing that larger companies are leading the adoption. This means that more workloads are going to be shipped in the enterprise than ever before.

## Microservices hierarchy of needs.

![Bilgin Ibryam's microservices hierarchy of needs](/images/MicroservicesHierarchyOfNeeds.png)

The benefits of containers are self-evident: fast start-up speed, compact and nimble. They are not magical though! How you tie containers together, monitor them and otherwise operationalise them requires thought.

You're probably familiar with psychologist Albert Maslo’s hierarchy of needs. In early 2017, a guy by the name of [Bilgin Ibryam had a go at defining what our microservices hierarchy of needs might look like](https://medium.com/@bibryam/microservices-hierarchy-of-needs-151df49fc678). Outside of the infrastructural delivery of containers, how are we going to manage capacity in the cluster? How do we run health checks and auto-heal services that are running slow or are simply unresponsive? How are you going to do service discovery? How will you automatically inject environment configuration into your running containers?

Thankfully the opensource community with the help of some amazing companies have been working on container orchestration platforms: Kubernetes, Swarm, Mesos ... to provide the framework required to look after these characteristics. And the most mature enterprise option, Openshift adds a nice PaaS layer on top of Kubernetes.

Where are you going to host your containers? Is it going to be in a secure private cloud, or public? Where are you going to run dev? Locally, or in the cloud? How are you going to scale your virtualisation or compute to adopt?

As you can see there are non-tech considerations to think through also ... how will you train your organisation to leverage containers, to automatically test and continuously deliver then deploy, to deliver services that are anti-fragile?

## 10 years of application deployment has taught us a lot.

![10 years of Application Deployment](/images/10YearsOfAppDeploymentHasTaughtUsMuch.png)

We’ve come a long way in 10 years. We’ve established that virtualisation is a fundamental building block now, and into the future. It’s not going away. However, the way we leverage that building block will. A lot. Consider Function-as-a-Service and the additional delivery power that provides.

We’ve also learned that:
  * Deploying software by hand is wasteful and error-prone.
  * Testing software manually is expensive and ineffective.
  * Idempotent automation is crucial, and automation is key.
  * Services are best built stateless, immutable.
  * Upgrading systems is laborious and torturous (even when automated).
  * Configuration management (vRealise, Ansible, Chef, Puppet ... ) tooling is powerful because it facilitates idempotent automation.
  * Performance matters.

The great advantages sometimes obfuscate some of the difficulties of building and managing containers. For example, how are you going to ensure your workloads are sufficiently firewalled away from each another. How are you going to meet your compliance and regulatory requirements, do containers change that? The truth is that dependency management is hard, and mastering the art of managing microservice dependencies is key to success in this space.

The great news is that the container community have been developing solutions for years now, and while container foundations have nearly completely settled there has still been a lot of movement on the orchestration platform side. Now that the community is pretty firmly settled on Kubernetes as the winning orchestration layer formula, the ecosystem is really starting to stabilise.

All good things to those who wait. Malcolm McLean didn’t build the intermodal shipping container in a day!

## In Conclusion.

Having used containers for a few years now, here are my top 10 containerisation tips:

  1. Start with something achievable. Just one thing.
  2. Define your DevOps goals before embarking on transformation.
  3. Stick to the patterns defined by the [12-factor app](https://12factor.net).
  4. Flock to Kubernetes as it's the most popular with the best community support. Use [RedHat Openshift](https://www.openshift.com) if you want Enterprise Support and PaaS on top.
  5. Keep the process of continuously integrating as similar as possible to the Development environment. No surprises.
  6. Ensure you have a platform for centralised logging and monitoring. Check out the [ELK stack](https://kubernetes.io/docs/tasks/debug-application-cluster/logging-elasticsearch-kibana/).
  7. If you’re using Docker, ensure you read about [Dockerfile best practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/).
  8. Always clean your container image of package cruft after you’re done installing images to keep your images small.
  9. If using Docker, make use of [multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/) (build vs run).
  10. Docker doesn’t replace configuration management. You still need a way to manage your secrets, config, information across your docker hosts. Even if that is Kubernetes.

There is a lot of buzz regarding containers, but the DevOps community has moved beyond it. I remember visiting [the inaugral Docker meetup in Sydney, Australia](https://www.meetup.com/en-AU/Sydney-Docker-User-Group/events/180666312/) in June 2014. "Who's using Docker in Production", was one of the questions. 2 hands went up. For a couple of years the same question was asked. Thankfully we've moved well beyond the concerns around adoption, maturity and security and Docker is now prevalent in continuous delivery pipelines everywhere.

Containers are the new go-to for app deployment and delivery in medium to large enterprises. The journey to containers isn't as simple as it might first seem. Many organisations I've spoken to and worked with are trying to puzzle together how to manage containers and best leverage them to drive agility within their respective organisations.

We’ve now hit a pivotal point in the container journey. Scheduling and managing container workloads is easier than ever before, and we’re now properly thinking about security and what this tech means for our business.