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

## Amdahl's Law

[Amdahl's Law](https://en.wikipedia.org/wiki/Amdahl%27s_law) is an 
important idealization in the field of parallel computing. Generally
speaking, the purpose of parallelizing a program is to spread
the computational work across multiple processing units to 
increase performance.

In [strong scaling](https://en.wikipedia.org/wiki/Scalability#Weak_versus_strong_scaling), the success of parallelization scheme is measured by the 
speed-up, which is to say, the ratio of the amount of time it takes
to complete the task with no parallelization, to the amount of time
it takes with some degree of parallelization $n$.

If the program parallelizes perfectly, then this speedup is 
simply $1/n$.

Amdahl's law describes how this applies to the simplest non-ideal
program. It assumes that only some fraction of the code can be
parallelized perfectly (the "parallel part"), and that a fixed
fraction of the code is intrinsically serial. In real-world codes,
the serial part might involve problem set-up or tear-down, or
data aggregation steps that integrate the resulsts of the 
parallel tasks.

In this case, there are diminishing returns to increasing 
the degree of parallelization, and after a point, developer 
effort is better invested in other performance strategies, 
such as speeding up the serial part of the program, or 
selecting a better algorithm.

In the HPC Intro lesson, the law is derived, and is written 
as $T(n) = (1-p)T + (p/n)T$, where $T$ is the serial run-time
of the program, $p$ is the parallel fraction of the program,
and $n$" is the degree of parallelism.  It's clear by inspection
of the equation that as $n$ becomes large, $T(n)$ becomes 
approximately equal to the duration of the serial part, 
$(1-p)T$, and increases in $n$ only have a small effect on the
runtime.

The "speedup" for a given degree of parallelization $n$ 
is $T(1)/T(n)$.

## The Amdahl's Law Executable

The HPC Carpentry development team has provided an executable,
called `amdahl`, that illustrates this law at low computational
cost, and is easy to run even on very small educational 
clusters.

The program divides a fixed amount of execution time 
(given in seconds by an argument, `-w`, which 
defaults to 30 seconds) into a parallel fraction (given by 
another argument `-p`, which defaults to 0.8) and a 
serial fraction (equal to $1-p$, inferred from the `-p` argument). 

The program takes another argument, `-np`, which tells it the
degree of parallelism to use.

Then, what it actually does is sleep (go into a wait state)
for the amount of serial run-time that has been inferred from
the arguments, and then launch a number of MPI ranks equal
to the value of the `-np` argument, each of which sleeps 
for an amount of time equal to the parallel portion of the
run-time divided by the number of ranks.

By default, the program adds a certain amount of jitter to
the results, so that they don't necessarily exactly lie on
the Amdahl's law curve.  The amount of jitter can be 
set (as a fraction of the total run-time) by the `-j`
argument, or disabled entirely with the `-e` (for "exact")
argument. 

The program then outputs the number of ranks and the
duration of the run-time. Depending on the `-t` flag
(for "terse"), the output is either human-readable plain
text (the non-terse case) or a bit of JSON suitable for 
machine ingestion.

The expectation is that learners will use the non-terse output
initially in HPC Intro, to get a feel for the diminishing 
returns of parallelization, and then use the JSON output
format to do an automated scaling study and create a plot
in the HPC Workflows lesson.

## Obtaining the Amdahl Code

The source code is available 
on [a repository](https://github.com/hpc-carpentry/amdahl) on the
HPC Carpentry's GitHub project. It's a Python code written to use
the parallel Message Passing Interface library, which is a 
dependency of it. 

It is also registered with the Python package index, PyPI, and so 
can be installed via `pip`. 

Alternatively, if your cluster uses the EESSI software suite, 
the Python Amdahl code is available there also.

For clusters where users are unable to download files from the
internet, it's possible to download the `pip` package and 
install it directly.  TODO: Is this true? 

Whichever scheme is used to install it, the installation should
take place in an environment where the `mpi4py` Python functionality
is available. This may be available by default on your cluster,
or you may need to load some combination of Python and MPI 
modules for it to be available.


::::::::::::::::::::::::::::::::::::: keypoints 

* HPC Carpentry workshops are centered on an exploration of Amdahl's law of scaling,
  illustrating the diminishing gains of increasingly parallelisation.
* _Amdahl_ is a Python executable that runs for a specified amount of time but does nothing else.
- `amdahl` is in the Python package index (`pip install amdahl`) as well as the EESSI virtual filesystem
- `amdahl` depends on `mpi4py` and a working MPI installation!

::::::::::::::::::::::::::::::::::::::::::::::::


