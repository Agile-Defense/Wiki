---
title: "Create a GoCD Pipeline"
description: "How to create a basic pipeline in GoCD"
lead: "How to create a basic pipeline in GoCD"
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "pipelines"
weight: 40
toc: true
---

### Setup
First, ensure you have a VPN connection to the O'Fallon Lab, have valid Innovations Lab credentials, and can log into [GoCD](http://gocd.agiledefense.lab)


### Create Pipeline

Once logged in, click **New Pipeline** in the upper right-hand corner and select `Use Pipeline Wizard`

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/pipeline_1.png)

<br/>

### Part 1: Material

For material type, select `Git` if you're pulling from GitHub (*common*), `Another Pipeline` if it pulls packages or artifacts from another GoCD pipeline, otherwise select the appropriate Material type.

Then add the URL associated with the repository and click `Test Connection` to make sure GoCD can see it.

{{< alert icon="👉" text="<b>NOTE</b>: If your default branch is named something other that <b>master</b>, you need to enter the <b>Repository Branch</b> name under <b>Advanced Settings</b>" />}}

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/pipeline_2.png" width="725" />

<br/>



### Part 2: Pipeline Name

Enter a name for you pipeline.

Under **Advanced Settings**, select the appropriate Pipeline Group (default is `CPaaS`). Here you can also enter parameters that will be available for every stage in a `Key: Value` store. It could be package names, directories, etc.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/pipeline_3.png" width="725" />

<br/>

### Part 3: Stage Details

Enter a name for your first Stage. This is normally to run builds or tests, depending on your package and what you need. If you do not want this first stage to start automatically after upstream changes, uncheck `Automatically run this stage on upstream changes` under **Advanced Settings**

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/pipeline_4.png" width="725" />

<br/>

### Part 4: Job and Tasks

Enter a name for the Job. A job is a series of tasks that execute in order. 

You can enter multiple commands, but it does not run in a real shell environment, so there are caveats. 

In the **Advanced Settings** menu, you can add environment variables and secure environment variables that are not visible, even on the GoCD site.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/pipeline_5.png" width="725" />

After you've configured your pipeline, you can either click [Save + Edit Full Config →]({{< relref "pipeline-config" >}}) or [Save + Run this Pipeline →]({{< relref "create/#congratulations" >}})

### Congratulations!

You have successfully configured and initiated your GoCD pipeline!