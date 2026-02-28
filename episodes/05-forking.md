---
title: "Forking the *Introduction to HPC* repository"
teaching: 10 # teaching time in minutes # FIXME
exercises: 2 # exercise time in minutes # FIXME
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are the reasons for creating a fork of the material.
- What is the process needed to prepare and maintain a fork of the material.
- How can I still contribute back to upstream from a customized fork.

::::::::::::::::::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: objectives

- Understand the necessity of forking the material.
- Understand the necessary forking workflow.
- Decide on a branching model that supports customization as well as proposing updates to the upstream.

::::::::::::::::::::::::::::::::::::::::::::::::

## Creating a fork

To lower the cognitive load of learners in your workshop by bringing the lesson material and the experience during the workshop closer together, you may want to customize the lesson material.
If you need to customize the lesson material prior to a workshop, this can only be done on a separate fork of the lesson material.

::::::::::::: prereq
The lesson material is hosted on Github and the automatic build infrastructure realized through Github actions.
To use the same workflow described in this episode you will need an **active Github account**.

Support for other Git Hostings Services and their CI infrastructure is currently not available.
::::::::::::::::::::

![The pull-down menu of the fork lets you start to create a fork](fig/hpc-intro_create_fork.png)

Using the pull-down menu next the fork button lets you start the forking process.

![Select the location of the fork and enable forking all branches of the repository](fig/hpc-intro_create_fork_details.png)

The **owner** determines the URL of the generated material.
Choosing a location that resembles the hosting organization will help recognizability and findability of your material.
If the hosting organization needs multiple customized versions of the material (e.g., customization to multiple different HPC systems), you can customized the **name** of the forked repository for distinction.

::::::::: callout
In order to fork the full auto-generate infrastructure you need to make sure that the "Copy the `main` branch only" option is **deselected** before creating the fork.
:::::::::::::::::

## Enabling the Github Actions Workflows

As mentioned before, the repository for the lesson material contains Github Actions workflows.
As these can contain commands, then executed on your behalf, those workflows are disabled by default.
To enable them you have to select the **Actions** tab.

![Warning message of disabled workflows shown after selecting the Actions tab.](fig/hpc-intro_workflows_disabled_message.png)

::::::::: caution
As with all security warnings, you should **verify** what the code contained in the Github Actions Workflow will do **or trust** the providing organization (in this case the HPC Carpentry) to ensure no malicious code is executed on your behalf.
:::::::::::::::::

After selecting **I understand my workflows, go ahead and enable them**, get to the workflow overview of the Actions tab.
There you will see that the three workflows are available are all disabled.

![](fig/hpc-intro_actioncs_tab_workflows_disabled.png)

When selecting one of them, you will see an info message, letting you know why the workflow was disabled.

![Info message about the disabled workflow](fig/hpc-intro_actioncs_tab_workflows_disabled_info.png)

Click **Enable Workflow** for all three workflows.
Then select the **01 Build and Deploy Site** workflow.

There you can see the **Run workflow** button to run the first build manually and test the infrastructure.

![Empty workflow history before the first manual run.](fig/hpc-intro_actions_tab_workflows_manual_run.png)

After the first workflow runs through, you have verified that the overall infrastructure is working.
Your rendered material will then be available at `https://<your-owner-handle>.github.io/<hpc-intro-repo-name>`.

## Contributing changes back to the upstream repository

As the workflows are enabled for the `main` branch without further intervention by you, it is recommended to use the `main` branch for your customization.
However, this impacts how you can keep working with the **upstream** version of the material.
When wanting to propose changes and improvements to the upstream repository, you will **not be able** to base these off your customized `main` branch, because the majority of your customizations should remain in your customized downstream repository.
Nevertheless, the spirit of the Carpentries is that the material should undergo constant improvement and community contributions are explicitly welcome.

:::::::::: callout
To make it easier for you to cherry-pick changes from your customized `main` branch to a branch for a pull request to upstream, you should keep individual commits small, self-contained and separate from general content customization.
::::::::::::::::::

To enable easy access to the upstream `main` branch---containing future changes and additions to the official lesson material---you first need to add the official HPC Carpentry repository as an additional remote to your cloned copy.

```sh
$ git remote add upstream https://github.com/carpentries-incubator/hpc-intro.git
```
With the official main HPC Carpentry repository available as `upstream` you can then create a branch (e.g., `upstream-main`) that tracks the `main` branch of the `upstream` repository.

```sh
$ git switch -c upstream-main upstream/main
```
Any branches that form the basis for pull requests, containing your suggested contributions to the `upstream` repository can then easily be created with

```sh
$ git switch upstream-main
$ git pull --rebase # this branch will never contain any of your commits so --rebase would not be strictly necessary
$ git branch <your-feature-branch>
$ git switch <your-feature-branch>
```

You can keep both, `your-feature-branch` and your `main` branch up to date by continuously rebasing it on any changes coming in from the `upstream` repository.

:::::::::: callout
The fewer your changes are to the official episode source material the easier it will be to keep your material up to date.
::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- When you use the cloud-based resources with the Magic Castle installation, you do not need to fork the material.
- Fork the material when you want or need to customize the material.
- Customization can only be configured for a specific site; different customizations require separate forks.

::::::::::::::::::::::::::::::::::::::::::::::::

