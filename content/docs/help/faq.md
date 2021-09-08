---
title: "FAQ"
description: "Answers to frequently asked questions."
lead: "Answers to frequently asked questions."
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "help"
weight: 630
toc: true
---

## Keyboard shortcuts for search?

- focus: `Ctrl + /`
- select: `↓` and `↑`
- open: `Enter`
- close: `Esc`


## GoCD Stage not getting assigned an agent

There are three possibilities:

1. Pipeline not in the correct Environment.
   - Check to see if the pipeline is in the environment by logging into [GoCD](http://gocd.agiledefense.lab).
   - Navigate to **Admin** at the top menu and select **Environments** in its drop down.
   - Find your environment and click on it to expand it. 
   - If you do not see your pipeline under **Pipelines**, click the edit button next to the **Pipelines** header.
   - Check the box next to your pipeline to add it. 
   - Then hit **Save**.

2. Go-Agent not able to reach GoCD Server
   - `ssh` to the specific go-agent and inspect `go-agent-launcher.log` file. 

3. Unable to connect - SSL handshake error or connection reset
   - `ssh` to the specific go-agent and inspect `go-agent-bootstrapper.out.log` file. 


## My Go-Agent is no longer in the agent pool

This is usually caused by the token used to register the agent with the main server getting invalidated. This can be fixed by `ssh`-ing to the agent in question and running the following commands (ensure you have `sudo` permissions):

```bash
sudo rm -rf /var/lib/go-agent/config
sudu systemctl restart go-agent
```

Then navigate back to the [GoCD Agents](http://gocd.agiledefense.lab/go/agents) pool and [enable]({{< relref "agent#enabling-environments-and-resources" >}}) it.
