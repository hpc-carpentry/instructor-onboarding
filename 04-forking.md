---
title: "Forking the *Introduction to HPC* Repository"
teaching: 10 # teaching time in minutes # FIXME
exercises: 2 # exercise time in minutes # FIXME
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are the reasons for creating a fork of the material?
- What is the process required to prepare and maintain a fork of the material?
- How can I contribute back to upstream from a customized fork?

::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: objectives

- Understand the necessity of forking the material.
- Familiarize yourself with the forking workflow.
- Decide on a branching model that supports customization as well as proposing updates to upstream.

::::::::::::::::::::::::::::::::::::::::::::::::

## Creating a Fork

To reduce cognitive load for learners during your workshop, you may want to customize the lesson materials. If customization is necessary before a workshop, it must be done on a separate fork of the lesson materials.

::::::::::::: prereq
The lesson materials are hosted on GitHub, utilizing an automatic build infrastructure powered by GitHub Actions. To follow the workflow described in this episode, you will need an **active GitHub account**.

Support for other Git hosting services and their CI infrastructures is currently not available.
::::::::::::::::::::

:::::::::: callout
The general process of forking a Carpentries Lesson is already [documented in the Carpentries Handbook](https://docs.carpentries.org/resources/curriculum/lesson-forks.html). Please consult this documentation to generate a fork in any of your workspaces.
::::::::::::::::::

## Contributing Changes Back to Upstream Repository

Since workflows are enabled for your `main` branch without further intervention needed on your part, it is advisable to use this `main` branch for customization purposes. However, this affects how you can continue working with upstream versions of materials when proposing changes or improvements; you will not be able to base these proposals off your customized `main` branch since most customizations should remain within your downstream repository.

Nevertheless, it embodies the culture of contribution that The Carpentries hopes to foster that materials undergo constant improvement through community feedback -- your contributions are explicitly welcomed!

### Checking out the upstream `main` branch.

As you modify the `main` branch of your fork, you will not be able to branch off its modified state in order to contribute back to the upstream lesson material.

To maintain easy access to future updates from upstream's `main` branch -- which contains ongoing changes and additions -- you need first to add HPC Carpentry's official repository as an additional remote in your cloned copy:

```sh
$ git remote add upstream https://github.com/carpentries-incubator/hpc-intro.git
```

With access established via `upstream`, create a new tracking branch (e.g., `upstream-main`) based on upstream's `main`:

```sh
$ git switch -c upstream-main upstream/main
```

### Creating a feature branch

You can then create branches containing suggested contributions intended for pull requests back into upstream using:

```sh
$ git switch upstream-main
$ git pull --rebase # The --rebase isn't strictly necessary since this branch won't contain any commits from you. It should always support fast-forward merges.
$ git branch <your-feature-branch>
$ git switch <your-feature-branch>
```

Keep both `your-feature-branch` and `main` updated by continuously rebasing against incoming changes from upstream's repository.

:::::::::: callout

The fewer modifications are made relative to official source material episodes, the easier maintenance will be when keeping content up-to-date.

::::::::::::::::::

### Cherry-picking modifications from your main branch 

If you **keep commits focused** and **self-contained** on a specific contribution, or individual steps towards a larger contribution, it is easier to pick individual changes to be part of your feature branch.
The process of integrating a specific commit of your `main` branch into your feature branch is called [**cherry-picking**](https://git-scm.com/docs/git-cherry-pick).

To cherry-pick a specific commit first take a look at you modifications to your `main` branch.

```sh
$ git switch `main`
$ git log --oneline
```
```output
a1b2c3d Update head-node information
e4f516a Clarify ssh-key generation
f748a9b Add snippet on module output
```

Let's assume the example above, the commit `e4f516a` stipulates a clarification worth contributing back to the upstream lesson material.
To integrate this commit into a new feature branch first create this branch.

```sh
$ git switch `upstream-main`
$ git branch clarify-ssh-key-gen
$ git switch clarify-ssh-key-gen
```

Now you can cherry-pick the specific commit into your feature branch

```sh
$ git cherry-pick e4f516a
```

:::::::: callout
Double-check that your contribution is self-contained by building the lesson material from your feature branch. 
::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- When using cloud-based resources with Magic Castle installation, there is no need to fork materials.
- Fork if you wish or require customizations.
- Customizations can only be configured per specific site; different customizations necessitate separate forks.

::::::::::::::::::::::::::::::::::::::::::::::::