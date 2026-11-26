---
title: "Forking the *Using HPC Systems* Repository"
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
- Decide on a branching model that supports customization as well as proposing
  updates to upstream.

::::::::::::::::::::::::::::::::::::::::::::::::

## Creating a Fork

To reduce cognitive load for learners during your workshop, you may want to customize the lesson materials. If customization is necessary before a workshop, it must be done on a separate fork of the lesson materials.

::::::::::::: prereq
The lesson materials are hosted on GitHub, utilizing an automatic build infrastructure powered by GitHub Actions. To follow the workflow described in this episode, you will need an **active GitHub account**.

Support for other Git hosting services and their CI infrastructures is currently not available.
::::::::::::::::::::

:::::::::: callout
The general process of forking a Carpentries Workbench Lesson is already [documented in the Carpentries Handbook](https://docs.carpentries.org/resources/curriculum/lesson-forks.html). Please consult this documentation to generate a fork in any of your workspaces.
::::::::::::::::::

## Contributing Changes Back to Upstream Repository

Since workflows are enabled for your `main` branch without further intervention needed on your part, it is advisable to use this `main` branch for customization purposes. However, this affects how you can continue working with upstream versions of materials when proposing changes or improvements; you will not be able to base these proposals off your customized `main` branch since most customizations should remain within your downstream repository.

Nevertheless, it embodies the culture of contribution that **The Carpentries** hopes to foster that materials undergo constant improvement through community feedback -- your contributions are explicitly welcomed!

The following workflow assumes that you have already forked the official HPC Carpentry repository on GitHub. When cloning a repository, Git automatically configures a remote named `origin`, which refers to the repository from which you cloned (in this case, your fork).

The official HPC Carpentry repository must then be configured as an additional remote named `upstream`.

### Configure the Git remotes
First, clone your fork if you have not already done so:

```sh
$ git clone https://github.com/<YOUR_GITHUB_USERNAME>/hpc-intro.git
$ cd hpc-intro
```

::: callout
Replace `YOUR_GITHUB_USERNAME` with the actual GitHub username.
:::

Check the configured remotes:

```sh
$ git remote -v
```

You should see `origin` pointing to your fork on GitHub, which is the remote repository from which you cloned:

```output
origin	https://github.com/<YOUR_GITHUB_USERNAME>/hpc-intro.git (fetch)
origin	https://github.com/<YOUR_GITHUB_USERNAME>/hpc-intro.git (push)
```

By default, cloning your fork configures only the `origin` remote. The official HPC Carpentry repository is not automatically configured as a remote. We therefore need to add it explicitly as `upstream`.

### Configuring `upstream`, fetching and checking out the upstream `main` branch

As you modify the `main` branch of your fork, you will not be able to branch off its modified state in order to contribute back to the upstream lesson material.

To maintain easy access to future updates from upstream's `main` branch -- which contains ongoing changes and additions -- you first need to add HPC Carpentry's official repository as an additional remote in your cloned copy:

```sh
$ git remote add upstream https://github.com/hpc-carpentry/hpc-intro.git
# Verify the configured remotes
$ git remote -v
```

The expected configuration looks like:

```output
origin	https://github.com/<YOUR_GITHUB_USERNAME>/hpc-intro.git (fetch)
origin	https://github.com/<YOUR_GITHUB_USERNAME>/hpc-intro.git (push)
upstream	https://github.com/hpc-carpentry/hpc-intro.git (fetch)
upstream	https://github.com/hpc-carpentry/hpc-intro.git (push)
```

::: callout
In this workflow, use `upstream` to retrieve official changes and `origin` to publish your contributions. Do not push directly to the official repository.
:::

Fetch the latest branches and commits from the official repository:

```sh
$ git fetch upstream
```

The `upstream` remote provides access to the official HPC Carpentry repository. Fetching from this remote retrieves its latest branches and commits without modifying your local working branches.

With access established via `upstream`, create a new local tracking branch (e.g., `upstream-main`) based on the official repository's `main` branch:

```sh
# `-c`: `--create` flag
# Optional `-t`: `--track` flag
$ git switch --create upstream-main --track upstream/main
```

The `upstream-main` branch now provides a clean starting point for preparing contributions to the official lesson repository.

### Creating a feature branch

You can then create branches containing suggested contributions intended for pull requests back into upstream using:

```sh
$ git fetch upstream
$ git switch upstream-main
$ git merge --ff-only upstream/main
# `--ff-only`: update only when the local branch can be fast-forwarded.
# This prevents accidental merge commits or divergent history.
$ git switch --create <your-feature-branch>
```

Periodically fetch changes from the upstream repository and fast-forward your local `upstream-main` branch to incorporate them. When necessary, rebase your feature branches onto the latest `upstream/main` to incorporate upstream improvements. Keep your customized `main` branch separate from upstream contribution branches to prevent site-specific modifications from entering proposed upstream changes.

:::::::::: callout

The fewer modifications made to the official lesson episodes, the easier it is to maintain your fork.

::::::::::::::::::

### Cherry-picking modifications from your main branch
**Keeping commits focused** and **self-contained** makes it easier to select individual changes for upstream contributions. [**Cherry-picking**](https://git-scm.com/docs/git-cherry-pick) allows you to apply a specific commit from your customized `main` branch to a feature branch based on the upstream repository.

To cherry-pick a specific commit first inspect at your modifications to your `main` branch.

```sh
$ git switch main
$ git log --oneline
```

::: callout
The following output can change from time-to-time.
:::

```output
a1b2c3d Update head-node information
e4f516a Clarify ssh-key generation
f748a9b Add snippet on module output
...
```

Let's assume the example above, the commit `e4f516a` stipulates a clarification worth contributing back to the upstream lesson material. To integrate this commit into a feature branch, first create this branch.

```sh
$ git switch upstream-main
$ git switch --create clarify-ssh-key-gen
```

Now you can cherry-pick the specific commit into your feature branch

```sh
$ git cherry-pick e4f516a
```

:::::::: callout
Before cherry-picking, verify that the selected commit is self-contained and does not depend on other workshop-specific commits. If dependencies exist, include the required changes or prepare a separate self-contained commit.

Double-check that your contribution is self-contained by building the lesson material from your feature branch.
::::::::::::::::

### Submitting your contribution upstream
Once you have cherry-picked the relevant commit and verified that the lesson builds successfully, push your feature branch to your fork:

```sh
$ git push -u origin clarify-ssh-key-gen
```

You can now create a pull request on GitHub to propose merging your changes into the official HPC Carpentry repository.

When creating the pull request, ensure that:

- The base repository is `hpc-carpentry/hpc-intro`
- The base branch is `main`
- The head repository is your fork
- The compare branch is `clarify-ssh-key-gen`

The upstream maintainers can review your proposed changes and decide whether to
merge them.

::::::::::::::::::::::::::::::::::::: keypoints 

- When using cloud-based resources with Magic Castle installation, there is no need to fork materials.
- Fork the lesson repository when workshop-specific customizations are required.
- Use upstream-based feature branches to prepare and submit improvements through GitHub pull requests.
- Keep customizations minimal to simplify maintenance and synchronization with upstream.

::::::::::::::::::::::::::::::::::::::::::::::::
