---
title: "The Pre-Workshop Checklists"
teaching: 10 # teaching time in minutes # FIXME
exercises: 2 # exercise time in minutes # FIXME
---

:::::::::::::::::::::::::::::::::::::: questions 

- Do I need additional HPC resources for my workshop?
- Which HPC resources can I use for the workshop?
- What are the advantages and disadvantages of the different resource options? 

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Identify which additional resources are needed for the workshop.
- Illustrate advantages and disadvantages of different workshop configurations.
- Choose HPC resources best suited for your workshop.
- Prepare HPC resources for your workshop.

::::::::::::::::::::::::::::::::::::::::::::::::

## HPC Resources and their influence on trainee experience

HPC systems are often highly customized installations.
This can significantly influence the experience of the participants during a specific workshop.
While the nature of Carpentry-style workshops naturally lends itself to weaving system-specific configuration details into the lesson,
a significant divergence between what is experienced during the workshop and what can be read in the material as part of a post-workshop recap can significantly increase cognitive load and confusion for the learner.
The lesson material of [Introduction to High-Performance Computing][hpc-intro] targets a general understanding of high-performance computing and helps learners form an initial mental model of what HPC is and how to interact with HPC systems.
Nevertheless, HPC systems are often unique installations that differ in the details of their software and hardware configurations.
These details may differ considerably from the cloud-based environment used as the reference system in this lesson.

## General Checklist

::: checklist
- Choose HPC resources to use for the workshop
- Choose *Introduction to HPC* material to use (based on resources)
- Prepare material
- Prepare workshop registration and landing page
- Get familiar with common interaction pitfalls for learners
:::

### Choosing HPC resources

High-performance computing differs in some ways from the environment of well-known and proven lessons of other lesson programs in that HPC systems are comparable to other large shared research instruments.
Teaching the use of such large research equipment only works to a limited extent on constrained resources such as a learner's laptop.
Therefore, using something that either simulates an HPC system or is "the real thing" makes sense when teaching how to use HPC systems.

The standard material for [Introduction to High-Performance Computing][hpc-intro] is tailored to a cloud-based virtual HPC environment that learners can use to practice the skills they are learning during the lesson.
This environment behaves very similarly to many other HPC systems the learners might encounter in the future.
As such, using exactly this virtual environment requires no or only very limited adaptation of the lesson material when preparing a workshop.

::: callout
In the future, the Carpentries may assist and/or provide pre-configured resources for individual workshops.
However, until this is decided and set up, workshop organizers are fully responsible for setting up any HPC cloud environment used in a workshop.
:::

Using existing HPC resources that may even be provided by the hosting institution of an HPC Carpentry workshop can reduce the administrative burden for workshop instructors, as the workshop will use existing, well-maintained resources of a production HPC center.
However, the divergence in user experience between the cloud-based environment, which forms the basis of the lesson material, and what the learners experience during the lesson may increase their mental load.
For this reason, the lesson material of [Introduction to High-Performance Computing][hpc-intro] provides mechanisms to easily adapt key information in the rendered material.
Furthermore, the hosting institution may actually want the workshop to not only teach participants about HPC in general, but also about the key aspects of the local HPC platform available to them in the future.

### Choosing the material for the workshop

Based on your choice of HPC resources, you may want or need to adapt the lesson material specifically to the HPC systems used in the workshop.
As mentioned before, using the cloud-based environment that was the basis for creating the material does not require any adaptation on the part of the workshop organizer or instructor.

### Prepare material

Check the following episodes on how to customize and adapt the lesson material to the HPC resources used in the workshop.
Keep in mind that the customization process may be unfamiliar to you, so plan enough time to **customize and check** the material prior to the workshop.

### Prepare workshop registration and landing page

Although the [HPC Carpentry][hpc-carpentry] has been officially adopted by the Carpentries Organization in February 2026, its core lesson program has not yet been fully integrated into the template for the workshop registration and landing page.
Therefore, you will need some time to map the individual episode timings onto the planned schedule manually.
This process may become more comfortable in the future.

### Get familiar with the common interaction pitfalls for learners

Interacting with an HPC system differs significantly from the platforms used in other Carpentries lessons.
The lesson material for learners may not fully discuss or teach how to resolve the different failure scenarios that can occur when working on an HPC system.
Having worked through the lesson material itself may therefore not sufficiently prepare you as an instructor to support learners in identifying and resolving problems in their interaction with the HPC system.
Some pitfalls may be described in the instructor information in the material, but some situations may not yet be foreseen or documented.

::: callout
Help us improve the instructor notes of the material by reporting and/or suggesting additional information that would have helped you as an instructor during the workshop.
:::::::::::

## Using cloud resources

::: checklist

- Apply for cloud resources at a cloud provider
- Set up cloud resources using Terraform / Magic Castle
- Test cloud setup prior to the workshop

:::

### Apply for cloud resources

As the lesson program of HPC Carpentry is still very new to the Carpentries organization, there are not yet centralized resources available for use in HPC Carpentry workshops.
You might therefore need to register with a cloud resource provider to apply for hardware resources.

### Set up cloud resources using Terraform and Magic Castle

We provide a configuration for [Terraform][terraform] and [Magic Castle][magic-castle] to set up cloud resources identical to the setup used as the basis for the material.

### Test cloud setup prior to the workshop

After setup, you should test the different interactions with the environment that are part of your workshop.

## Using local resources

::: checklist

- Apply for a compute budget (as needed)
- Create a reservation (as needed)
- Clarify requirements for accessing local resources
- Ask for any needed information for access at registration time
  - Make sure that the registration deadline is set early enough to allow for any required processing.
- Clarify support during the workshop with local administrators

:::

### Apply for a compute budget

Production HPC environments often have budgeted compute resources.
Although the lesson does not consume a lot of computational resources during the course, you may still have to apply for compute time at the hosting institution.
This application process is highly individual for different institutions, so you need to inform yourself about how to apply for compute time.
The usernames of your learners will need to be associated with the allocated compute budget.

### Create a reservation

HPC systems are a resource shared among all their users.
As HPC resources are usually scarce and compute queues are often full during working hours, your learners may need to compete for computational resources with all other users of the HPC system.
A reservation of resources will keep them free for your workshop users and keep turn-around times low during the workshop, so you don't incur any delays due to excessive waiting time for the learners' jobs to complete.

::: callout
The situation is similar to taking your learners on a driving lesson in the middle of the daily commute.
A reservation will keep a lane free for your learners to use even if the rest of the resource is occupied.
:::

### Clarify requirements for accessing local resources

Data centers often keep HPC clusters in access-restricted networks.
Additional access requirements, such as VPN or two-factor authentication, may need to be set up.
Depending on your workshop parameters (online, on-premises), the constraints for your learners may vary.
Contact the host organization early in the organization process of the workshop to clarify any potential constraints, so you can include them in your planning process.

### Ask for required information at registration time

If any information is needed from workshop participants to set up access to the HPC resources used for the workshop, it is best to ask for this information prior to the workshop at registration time.
This may include, but is not limited to, a valid user account on the HPC system in use, so you can associate a potential compute budget and reservation ahead of time.

### Clarify administrator support during the workshop

If you are not administering the HPC system used in your workshop, having access to an administrator of the HPC resource in use may help with troubleshooting interactions with the job scheduler or system environment during the workshop.

::::::::::::::::::::::::::::::::::::: keypoints 

- The selection of HPC resources depends on your audience.
- Cloud resources are well suited for a general introduction.
- Specific local HPC resources are best for teaching HPC principles *combined* with how to access local resources.

::::::::::::::::::::::::::::::::::::::::::::::::