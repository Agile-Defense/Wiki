---
title: "Provisioning New Lab VM"
description: "How to provision a new virtual machine in Innovations Lab vSphere"
lead: "How to provision a new virtual machine in Innovations Lab vSphere"
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "provisioning"
weight: 1
toc: true
---

## Get started

There are two main ways to provision a new server:

### Net Boot from PXE

{{< alert icon="👉" text="This is the recommended method. It will install Ubuntu 21.10 Impish Indri." />}}

This will guide you step-by-step through [Net Booting. →]({{< relref "net-booting" >}})

### Boot from ISO file

{{< alert icon="👉" text="This method will NOT configure your server with LDAP/AD authentication." />}}

This will guide you through provisioning via [File ISO. →]({{< relref "file-iso" >}})
