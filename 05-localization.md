---
title: "Customize the lesson material"
teaching: 10 # teaching time in minutes # FIXME
exercises: 2 # exercise time in minutes # FIXME
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is the purpose of customizing the material?
- What are the different ways of customizing the material?
- Which best practices apply to customizing the material?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the purpose of customizing the material.
- Use the customization method best suited to a specific purpose.
- Apply best practices when customizing the material.

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::: caution

The customization infrastructure is **not intended** for changing or adding **significant amounts of additional course content**.
You should always consider whether the customizations you make **serve to reduce cognitive load during and after the workshop**.

:::::::::::::::::

## Creating a repository for the customizations

The customization framework for the [Introduction to HPC][hpc-intro] lesson extends the standard [Carpentries Workbench][carpentries-workbench] infrastructure and works by using a **base template** and a **customization template**.
These templates are directories containing configuration and content source files that will be used when rendering the lesson material.

Customization can be done in two different ways:

1. By redefining a variable that is used in one or more places of the episode markdown, or
2. By providing a snippet file with the same name as the one used in the episodes.

The **base template** defines all *variables* and *snippets* used in the episodes.
The **customization template** can then selectively override any of those variables.
The lesson material already provides a complete base template with `HPCC_MagicCastle_slurm`, so you only need to create a customization template for your local adaptations.
Variables are often small strings of one or a few words, representing hostnames, commands, arguments, URLs, and similar items.
Snippets are larger text files that are inserted as-is into the Markdown source during the rendering process.


## Generating a customization directory

The customization files reside in the `episodes/files/customization` subfolder.
There you can find two subdirectories:

1. `HPCC_MagicCastle_slurm`, the **base template** from HPC Carpentry, and
2. `Ghastly_Mistakes`, an **example customization template**.

We recommend using `HPCC_MagicCastle_slurm` as the base for your customization.
It contains the customization for a cloud-based cluster installation, based on Magic Castle using the Slurm scheduler.
The files in `Ghastly_Mistakes/` provide an example customization for reference.
They contain values different from the base template, and are sometimes used to check whether the customization works in general.

To start your first customization, create a new subdirectory for the configuration and snippets.

```sh
$ cd episodes/files/customization
$ mkdir YourCustomizationDirectory
```

<!-- You can do this either by creating a directory manually, or by including a Git submodule based off the [customization template][customization-template] provided by HPC Carpentry. --->

Add a minimal configuration file `_config_options.yml` to this directory, containing the variable `snippets`, set to the directory name of your customization:

```yaml
snippets: "YourCustomizationDirectory"
```

And create an empty `snippets` directory, to be populated with more customizations later:

```sh
# in YourCustomizationDirectory...
mkdir snippets
```

## Enabling the customization in the GitHub Actions workflow

To enable the use of this customization, set the environment variable `HPC_CARPENTRY_CUSTOMIZATION` to the location of the customization configuration during the build process.

### Local builds
For local builds, set the variable in the shell from which you start R to build the lesson material (or from a Terminal if working in an IDE).

```sh
$ export HPC_CARPENTRY_CUSTOMIZATION=/full/path/to/episodes/files/customization/YourCustomizationDirectory/_config_options.yml
```

:::::::::: callout

Currently, the standard build process does not recognize changes in the customization configuration or the snippets. To get a clean build after changing anything in the customization, you need to **reset the site** by calling `sandpaper::reset_site()` and **trigger the build** with `sandpaper::build_lesson()`.

```sh
$ r -e "sandpaper::reset_site();sandpaper::build_lesson()"
```

::::::::::::::::::

### On GitHub
To set this during the GitHub Actions workflow, you need to select *Secrets and variables* in the left menu of the *Settings* tab.
Then you select *Actions* and select the *Variables* tab.

![Viewing the Github Actions secrets](fig/hpc-intro_actions_variables_overview.png)

There you set `HPC_CARPENTRY_CUSTOMIZATION` as a **Repository variable**.

![Adding a new repository secret](fig/hpc-intro_actions_new_repository_variable.png)

This will then be passed to the build workflow.

## Customize via in-paragraph variables

You can modify individual variables in the `_config_options.yml` file of your customization.
You do not have to redefine all variables, so your customization config can list only the variables you want to change in the lesson.

For example, you could adjust the hostname of the login node (referred to with `config$remote$login` in the lesson source) by adding the following to your `_config_options.yml`:

```yaml
remote:
  login: "login.YourCustomization.org"
```

::: callout

The hierarchy in variable names is important (e.g. `login` within `remote`, above). Please ensure that you retain the variable hierarchy for the variables you do redefine.

:::::::::::

## Customize via 'snippets'

The following *snippets* are currently used in the episodes.
You can generate the current list of supported snippets in the `HPCC_MagicCastle_slurm/snippets` directory yourself like this:

```sh
$ HPCC_MagicCastle_slurm/snippets $ find . -type f
```
```output
cluster/queue-info.Rmd
cluster/specific-node-info.Rmd
scheduler/basic-job-status.Rmd
scheduler/runtime-exceeded-output.Rmd
scheduler/using-nodes-interactively.Rmd
scheduler/print-sched-variables.Rmd
scheduler/basic-job-script.Rmd
scheduler/option-flags-list.Rmd
scheduler/terminate-job-cancel.Rmd
scheduler/job-with-name-status.Rmd
scheduler/terminate-job-begin.Rmd
scheduler/terminate-multiple-jobs.Rmd
scheduler/runtime-exceeded-job.Rmd
parallel/one-task.Rmd
parallel/eight-tasks.Rmd
parallel/four-tasks.Rmd
modules/python-executable-dir.Rmd
modules/module-load-python.Rmd
modules/software-dependencies.Rmd
modules/missing-python.Rmd
modules/available-modules.Rmd
resources/account-history.Rmd
```

The files in `HPCC_MagicCastle_slurm` will always remain the reference customization in the repository.
The subdirectories of the snippet files correspond to the episode names they are used in.

They are usually the output from corresponding commands in the episodes and should be regenerated with the corresponding commands on the HPC system you customize for.

Create the files (and subdirectories) for the snippets that you want to override.
For example, to add your own snippet with [the output of `sbatch` for the `scheduler` episode](https://carpentries-incubator.github.io/hpc-intro/13-scheduler.html#running-a-batch-job) ([page source](https://github.com/carpentries-incubator/hpc-intro/blob/main/episodes/13-scheduler.Rmd)), create a `snippets/scheduler` directory and add a `basic-job-script.Rmd` file with your customized contents:

````markdown
```output
Submitted batch job 12345
```
````

This snippet will now be used in your lesson instead of the default from the `HPCC_MagicCastle_slurm` configuration.

::: caution

### Adding additional content

Sometimes you may need to add additional content to the lesson.
The current lesson curriculum has been tried and tested to fit into the 1-day (two half-days) schedule.
Adding significant content to the lesson material will likely skew the time needed to teach the lesson.
You should keep additional content to a minimum, expand the timeframe, and/or remove other content from the workshop.

:::::::::::

::::::::::::::::::::::::::::::::::::: keypoints 

- Any divergence from the core material introduces a maintenance debt.
- Use the recommended customization methods.
- Do not make significant additions to the material without adjusting the time available.
- Only customize what helps the learner match the in-class and out-of-class experience.

::::::::::::::::::::::::::::::::::::::::::::::::
