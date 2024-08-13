---
title: "My DevOps definition"
date: 2024-08-06
draft: false

showDate : true
showDateUpdated : false
showHeadingAnchors : false
showPagination : false
showReadingTime : false
showTableOfContents : true
showTaxonomies : false 
showWordCount : false
showSummary : false
sharingLinks : false
showEdit: false
showViews: false
showLikes: false
layoutBackgroundHeaderSpace: false

---

I have often seen the word DevOps being misused and because ambiguity hurts communication, I want to share with you what DevOps means to me.  

This definition has been shaped over the years and influenced by the amazing people I have worked with.

## What is DevOps?

Let’s first start with some misconceptions:

- Developers who check logs for operational issues isn’t “doing DevOps”.
- DevOps is also not an Ops person that writes code.
- DevOps is not a business unit within your org. Renaming your ops/infra department to “DevOps team” isn’t doing DevOps.
- Having microservices isn’t DevOps. And DevOps in general isn’t attached to a specific software architecture.
- DevOps isn’t the team that runs the CI/CD pipeline.

What DevOps is:

> DevOps is a <u>mindset</u> that promotes a <u>strong</u> sense of <u>ownership</u> to enable high-quality product building 
and efficient collaboration between teams.

<u>Ownership</u> lies at the heart of DevOps. By owning a service, a team is responsible for that service. Most companies don’t operate like this. Especially in large companies, 
people own processes more than services. One team is responsible for the development process, another for the 
release process, another for the operational process, etc. It’s the traditional siloed org where code is thrown over the fence for someone else to manage. 

<figure class="flex flex-col items-center image">
  <img class="rounded-md" src="/posts/my-devops-definition/images/no-devops.png" />
  <figcaption class="mx-2">
    <em>This traditional siloed model suffers from slow feedback and divergent goals between teams</em>
  </figcaption>
</figure>

A <u>strong</u> 
ownership means you own the service end-to-end. This ownership isn’t limited to the code you write but includes 
all components required for the application's lifecycle such as CI/CD pipelines, artifacts, storage, logging and 
monitoring, etc. And it extends through all stages of the release (dev → staging → prod).

It is in that 
context, that you will find a team tasked with enabling the DevOps mindset through a mix of culture, tooling, 
and processes. This team can be referred to as the DevOps team.

<figure class="flex flex-col items-center image">
  <img class="rounded-md" src="/posts/my-devops-definition/images/devops-diagram.png" />
  <figcaption class="mx-2">
    <em>DevOps model: Team A can quickly iterate</em>
  </figcaption>
</figure>

To drill down the concept, here is a short FAQ to clarify how far the ownership concept spreads:

- <b>Who should be on-call?</b> You should be on call for the services you own. Developers should be on-call for their 
microservices. DevOps engineers should be on-call for Kubernetes, Jenkins, or more generally for the platform they build.
- <b>Who owns the CI/CD pipeline?</b> Developers own the pipelines that are relevant to the services they own. 
DevOps engineers own the pipeline infrastructure (jenkins, Github Actions, etc…)
- <b>Who owns this S3 bucket, that database, or that Kafka queue?</b> Ownership falls on the team that consumes the bucket, 
database, or Kafka queue. DevOps engineers owns the abstraction that make such services available for developers to leverage.

As we can see from these examples, the DevOps mindset isn’t limited to developers. 
Everybody should think in terms of building and owning services:

- For developers that might be building microservices that will be consumed by other microservices or exposed to end-users.
- For the DevOps team that might be building a computing platform where developers can ship their microservices.
- For the infra team that might be building a secure networking foundation that will be used by the DevOps team.
- etc.

## Why is this strong sense of ownership so important?

When teams own processes instead of services the goals of each team won’t be aligned. As code is handed over between teams there is a 
strong chance that it does not answer to the needs of each team in the same way. This can degrade the collaboration 
as different teams will request from each other that they make changes that are in their interest. Overall each team 
will be less effective.

When teams own services end-to-end they have a greater incentive to build a high-quality product. All of a sudden 
it is no longer someone else’s problem if the service they own starts crashing in production, if the logs start 
throwing weird errors, or if a CI pipeline fails. When done right, teams are empowered to strive for excellence because 
they can have an impact through the whole lifecycle of their service, act as soon as a problem occurs, and implement 
and release new improvements quickly. There is a positive feedback loop because any improvement they make impacts them 
directly. This is where the DevOps team plays a crucial role: <b>Being able to manage a service end-to-end should be empowering 
and not feel like a burden.</b>

## How to enable it?

When developers are asked to shift to a DevOps mindset it often feels to them like development time is taken away from 
them and put into other activities such as CI/CD pipelines, documentation, and operational aspects of their service. While 
it is true that the scope of responsibilities has expanded it is up to the DevOps team to ensure that developers can stay 
highly productive. The following should be the main areas of focus:

1. **Define clear ownership**: This is always the first step. It can be as simple as table in a wiki that stores a list of 
all services and the associated team that owns them. Ideally, services should also have a link to some documentation 
that explains how to interact with the service. Once ownership is defined everyone knows what to expect from each other.
2. **Build abstractions**: The DevOps team should enable developers to do their best work and for that, they should provide 
high-quality services that abstract away implementation details. Developers should not have to learn the ins and outs of 
Kubernetes or Jenkins to be able to build and ship their code. The DevOps team should therefore provide services with an 
interface that exposes just the right amount of toggles required for other teams to be able to do their work and customize 
things to their need.
3. **Reduce bottlenecks**: To not slow down developers there should be as little friction between developers and the DevOps 
team. Ideally, developers should not have to submit tickets or wait for approvals. This is only possible when services provided 
by the DevOps team can be accessed on-demand. In addition to being on-demand services will need to be well documented to ensure 
they are used correctly. Automation also plays an important role as a way to offload manual and repetitive tasks.
4. **Embed best practices and security standards**. Making developers responsible for more than just writing code might sound 
like it would be a security risk but that doesn’t have to be the case. On the contrary, there is an opportunity to embed best 
practices and strong security defaults into the tools made available for the developers. One way to do this is to define an operational 
readiness checklist to ensure that all microservices reach a certain standard.

## Final words

DevOps is one of those words everyone assumes they know what it means. This can be detrimental as nobody is working towards 
a common shared goal. Sometimes people agree on what they <em>think</em> it is but actually miss the whole point and will 
therefore never truly unlock its potential. The thing is, unless its key tenants are well understood 
and an honest introspection of the current way of working is done, DevOps will remain elusive. My hope is that with 
this article I have managed to cut through the noise and shine some light on what matters the most: the ownership mindset.