---
title: "HPC Carpentry Curriculum"
teaching: 10 # teaching time in minutes # FIXME
exercises: 2 # exercise time in minutes # FIXME
---

:::::::::::::::::::::::::::::::::::::: questions 

- What do we intend to convey through our workshops?
- What tools do we use?
- What do we cover, and intentionally *not* cover?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the intentions of the HPC Carpentry lesson program.
- Use the tooling adapted by the HPC Carpentry.
- Learn the scope of the HPC Carpentry curriculum.

::::::::::::::::::::::::::::::::::::::::::::::::

## The HPC Carpentry Curriculum

Currently, the expected model of an HPC Carpentry workshop is
a two-day event during which three lessons will be taught. The
three lessons are the Software Carpentry Unix Shell lesson,
and the HPC Intro and HPC Workflow lessons from the HPC Carpentry
project itself.

As with all Carpentries materials, workshop organizers may wish
to add or remove lessons, depending on the needs of their learners.
For example, your community may already be familiar with the shell,
or have had it in other workshops, in which case it can be omitted
from the HPC Carpentry workshop.

An exception to this is the HPC Workflow lesson, which builds on
material covered in the HPC Intro lesson, and shares a model
executable, the `amdahl` code, with it. Workshop organizers
may find that the HPC Workflow lesson does not stand alone
especially well, although of course the project would be
interested in your feedback if you attempt this.

## Intended Audience

The model HPC Carpentry workshop is intended for novice users
of HPC systems. We assume that the learners are in some technical
field, and have a requirement to run computations on systems
larger than their laptops, but lack the skills to use these
systems effectively.

## Pedagogical Notes

A major feature of the HPC Carpentry lessons are two deviations
from what might be considered pedagogical best practice.

The first of these is the "jargon buster" presentation early
in the HPC Intro lesson. This presentation does not have any
exercises or hands-on component to help with learner retention,
but the development team has nevertheless found it to be
valuable in clarifying HPC terminology, which uses some technical
terms interchangeably ("node", "computer"), and uses some ordinary
English words in a more narrow technical sense ("server", "thread").

The second of these is the use of the `amdhal` executable for
demonstrating both parallel execution, and diminishing returns
to increasing parallelization. In the lessons, this program is
a "black box", and the way it is constructed is not interrogated.
Generally speaking, it's good practice to not have unexplained
or magical-seeming entities in lesson materials, but in this
case, the development team's experience has been that attempting
to explain how MPI executables are coded imposes a high
cognitive burden on novice HPC users, and distracts significantly
from the lesson goals.

## Instructional Themes

The first major focus of the workshop is the mechanics of
working on an HPC cluster. This includes conceptual items,
such as the fact that the cluster log-in node is remote
from the user's laptop, and that when jobs run on the cluster,
they do so at an additional remove from the log-in node, and
the idea of file systems that are shared between computers,
all of which are likely new to learners. It
also includes the actual details of constructing a batch file,
specifying resource requests, and submitting the job to the
cluster and locating and observing the outputs.

The HPC Intro lesson also emphasizes the shared nature of
typical HPC clusters, which is likely to be another novel
feature for novice users. In a shared environment, errors
or misconfiguration can impact not only the user's own
jobs, but the performance of the system as a whole, and
through that mechanism, impact other users. For this reason,
HPC users need to be aware of their resource requirements,
and make realistic resource requests.

In the workflow lesson, this is extended to include the
mechanics of specifying a workflow in the `snakemake` tool,
as well the declarative nature of the specification, where
`snakemake` rules are not run if their outputs already exist.

A second theme of the curriculum is a conceptual introduction
to parallel execution, and to the diminishing returns that arise
from increasing degrees of parallelism, due to the effect of
Amdahl's Law, for which the `amdahl` exectuable is named.

For the workflow lesson, a third theme is relevant, namely the
benefits of workflow automation. HPC resources are at their best
when running multiple jobs in a batch queue. In real-world environments,
the gap between the submission time and dispatch time of a job
might be large, and many HPC-appropriate tasks may require many
jobs. A workflow tool helps to manage this process, allowing
HPC users to operate at a higher level of abstraction, specifying
and executing parametric studies, for example, over many jobs.
The culmination of the workflow lesson is exactly this type of
task, where learners execute an automated scaling study of
the timing of the `amdahl` executable.




:::::::::::::::::::::::::::::::::::::: keypoints

* The lessons have as a pre-requisite the Software Carpentry Unix Shell intro lesson.
* The lessons are aimed at novice HPC users who need to be able to operate a batch resource manager.
* The focus of the lessons are resource manager operations, the benefits and diminishing returns of parallelism, and workflow automation.

::::::::::::::::::::::::::::::::::::::::::::::::
