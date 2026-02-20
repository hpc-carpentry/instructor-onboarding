---
title: "Workshop Narrative: the _Amdahl_ Executable"
teaching: 10 # teaching time in minutes # FIXME
exercises: 2 # exercise time in minutes # FIXME
---

:::::::::::::::::::::::::::::::::::::: questions 

* What is the central example in an HPC Carpentry workshop?
* What does the _Amdahl_ program do?
- Why do we need `amdahl` when there are lots of parallel applications out there?
- How do I install the __amdahl__ package?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

After this episode, Instructors will be able to...

* Describe the story we tell to guide learners through an HPC Carpentry workshop.
* Describe what the _Amdahl_ executable does.
* Install the _Amdahl_ executable.

::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: keypoints 

* HPC Carpentry workshops are centered on an exploration of Amdahl's law of scaling,
  illustrating the diminishing gains of increasingly parallelisation.
* _Amdahl_ is a Python executable that runs for a specified amount of time but does nothing else.
- `amdahl` is in the Python package index (`pip install amdahl`) as well as the EESSI virtual filesystem
- `amdahl` depends on `mpi4py` and a working MPI installation!

::::::::::::::::::::::::::::::::::::::::::::::::
