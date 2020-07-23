---
layout: post
title:      "Continuous 'Off-Wind' Deployments with Spinnaker "
date:       2020-07-23 18:43:13 +0000
permalink:  continuous_off-wind_deployments_with_spinnaker
---

Ahoy, mateys!

![](https://media.giphy.com/media/M5LEiBwzgXqGA/giphy.gif)

[Spinnaker](https://spinnaker.io/setup/) is an open-source multi-could continuous delivery platform. It is fully configurable, can contain multiple applications and can incorporate itself over many different accounts, regions and stacks. 

That's a mouthful!

Let's take a higher-level view of Spinnaker.

It's a platform that is great at managing apps as they transition from testing to deployment. We can break down its core features into two parts.

1. Application Management

2. Application Deployment

#### Application Management 


Most tech companies manage a collection of different **Services**. A **Service** is a group of applications sometimes called **Microservices**. Theses applications hold **Server-Groups**.

A **Server-Group** identifies the i*ndividual instances* that should be collected to incorporate the *deployable information*(such as a Docker Image or a source location).

The level above a **Server-Group** is called a **Cluster**, which can hold *logical-similar* **Server-Groups**. 

A **Cluster** can then get passed to various **Load Balancer** and **Firewall** configurations, which describe how the **Services** present themselves to users.  

That's a lot of abstraction! Check out the image below to see it all tied together.  

![](https://spinnaker.io/concepts/clusters.png)


#### Application Deployment

To understand how the Spinnaker's application deployment works, let's quickly cover what a **pipeline** is.

A **pipeline** is a set of automated processes to make an application's deployment reliable and efficient. 

The essence of a pipeline to remove human error from the deployment process.

A pipeline can break down conceptually to these five stages/categories.

1. Source Control
2. Build Tools
3. Containerisation
4. Configuration Management
5. Monitoring


Let's check out how Spinnaker utilizes these pipeline concepts. It consists of three stages. These stages can run in parallel to accommodate different regions. 

1. **Bake** - Produces a machine image for deployment
2. **Deploy** - Takes the machine image and creates a Server Group with the specific instances in a particular region or location
3. **Manuel Judgment**- Think of this as the 'point-of-no-return.' Manuel Judgement allows developers the opportunity to intervene, before final deployment. 


There are also 16 more stages Spinnaker can incorporate into a developer's pipeline. The pipeline can be event-triggered automatically or manually. An *automatic function in Spinnaker* is called a **Task**. A collection of **Tasks** makes a **Stage**. Spinnaker makes every "Stage" fully customizable. 

Before we wrap up, I wanted to share my thoughts on why the platform is called Spinnaker. So, let's talk about what a physical Spinnaker is. 

![](https://media.giphy.com/media/j6MMHvVSIAzhAiP2IZ/giphy.gif)

On a sailboat, the wind pushes the boat in the direction the wind is blowing. A sailer can adjust the sail to change course. In other words, they are *manipulating the continuous deployment of wind* to meet the desired direction. Sound familar? However, the range is limited. If the wind is blowing from the front of the boat to the back, you won't be able to sail in that direction.

A spinnaker is an additional sail(not the mainsail) designed to sail 'off-the-wind.' Off-wind means the wind is coming across or perpendicular to the boat as opposed to from behind. I saw another article stating 'off-the-wind' can mean, the wind speed is slow.  If this happens, you can't sail in that direction efficiently. 
A spinnaker is unique because it allows a sailor to manipulate their direction closer to their desired off-wind course. This sail is shaped like a triangle and made of a lighter material than the mainsail. The Spinnaker fills with wind and creates a balloon shape. This is called 'flying.' 

![](https://i.pinimg.com/originals/23/a7/44/23a744be17af57e481bd80f2c1091ec5.jpg)

Due to this shape and weight of a spinnaker it can access a more significant percentage of wind speed than the mainsail. In essence, the wind direction becomes less critical because the Spinnaker needs less wind than the mainsail. 

Clear as mud?

![](https://media.giphy.com/media/WR6kc5Lytbnd6/giphy.gif)

Yes, I did look all that up, and I wore my captain's hat the whole time.  A physical spinnaker and the platform Spinnaker basically do the same thing.

They allow greater control/ human intervention to manipulate an automated process(wind/ deployment) to move toward your destination faster. Instead of 'go with the flow', spinnakers say, 'go with MY flow.'

![](https://media.giphy.com/media/VEsfbW0pBu145PPhOi/giphy.gif)

