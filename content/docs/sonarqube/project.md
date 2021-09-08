---
title : "Setup SonarQube Project"
description: "Setup project for static code and dependency checking"
lead: "Setup project for static code and dependency checking"
date: 2020-10-06T08:48:45+00:00
lastmod: 2020-10-06T08:48:45+00:00
draft: false
images: []
menu:
  docs:
    parent: "sonarqube"
weight: 60
toc: true
---



### Setup

This guide assumes you have a GoCd Pipeline already setup. If not, [Setup a Pipeline]({{< relref "create" >}}). 

Log in to [SonarQube](http://sonar.agiledefense.lab) with your lab credentials.

### Add Project

Click the **Add Project** drop down menu in the upper right-hand corner under your username and select `Manually`.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/sonar_1.png)

<br/>

On the next menu, enter in the `Project Key` and `Display Name`. They can be the same or different, but the `Project Key` is how Sonar indexes your project. Then, click **Set Up**.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/sonar_2.png)

<br/>

### Generate token

On the next page after clicking **Set Up**, it will ask if you want to `Generate a token` or `Use an existing token`. It is **HEAVILY** encouraged that you generate a new token for your project. 

To do that, highlight `Generate a token`, enter a name for the token, we'll use `test_token`, and then click **Generate**.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/sonar_3.png)

<br/>

After that, your token will appear. **Be sure to copy your token!!**. This is the only time it is displayed. If you lose it before adding it into the `Sonar-Scan` stage of the pipeline, you'll need to revoke and regenerate a new one.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/sonar_4.png)

<br/>

### Create Sonar-Scan Stage

Log into [GoCD]() with your lab credentials, and click on the wheel icon in the top right corner of your pipeline.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/sonar_5.png)

<br/>

Then go to the **Stages** tab in your pipeline config and click **Add new stage**. 

Name it `Sonar-Scan` or something to that effect and name the job something like `sonar-scanner`.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/sonar_6.png" width="725" />

<br/>

For the **Command** enter `sonar-scanner`, and the **arguments** are `-Dlogin={TOKEN}` where `{TOKEN}` is the token you copied from the **Generate token** step. Now click **Save**.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/sonar_7.png" width="725" />

<br/>

### Optional: Dependency Checking

Although optional, it is highly encouraged to set up dependency checking for your project. To do that, go to your `Sonar-Scan` stage of your pipeline and enter its `sonar-scanner` Task tab. Then click **Add Task** for type `Custom Command`.

For the command enter `dependency-check`, and the **arguments** are `--disableAssembly --enableExperimental -s . --project {PROJECT} -f HTML` where `{PROJECT}` is the project name we gave the SonarQube project in the **Add Project** step.

{{< alert icon="👉" text="<b>NOTE</b>: Ensure that each argument is on its own line with no leading or trailing spaces." />}}

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/sonar_8.png" width="725" />

<br/>

Now make the `dependency-check` task first so it can generate the files that are needed when running `sonar-scanner`. Just drag it by the dots on the left, so it's above the top task. Be sure to click **Save**. 

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/sonar_9.png" width="725" />

<br/>

### Restart Pipeline

Now that your Stages, jobs, and tasks are added, you can manually execute your pipeline from the dashboard, or waiting for changes to your code to automatically start it. 

### Congratulations!

Your pipeline has not increased its level of operational and engineering excellence by incorporating static code vulnerability analysis and dependency scanning. 
