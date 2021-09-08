---
title: "Booting from File ISO"
description: "How to provision a new virtual machine in Innovations Lab vSphere"
lead: "How to provision a new virtual machine in Innovations Lab vSphere"
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "provisioning"
weight: 12
toc: true
---

### Setup
First, ensure you have a VPN connection to the O'Fallon Lab, have valid Innovations Lab credentials, and can log into [Innovations Lab vSphere](https://adlbvc01.agiledefense.lab/ui/)

<br/>

### Provision

1. Right click on **DellCluster** and select **New Virtual Machine**.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_1.png)

<br/>

2. Select **Create a new virtual machine** if it isn't selected already and click **Next**.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_2.png)

<br/>

3. Give your VM a name, then click **Next**. We'll use `Test_VM` for this example.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_3.png)

<br/>

4. Select a Resource Pool, if desired. Otherwise, select the parent **DellCluster**. We're going to select **SoftwareDev** in this example. Click **Next**.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_4.png)

<br/>

5. Select a storage solution for your vm and hit **Next**. I'm selecting `vsanDatastore` because it has the largest capacity at the moment. 

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_5.png" width="725" />

<br/>

6. Select `ESXI 6.7 Update 2 and later` to ensure you have the latest compatibility hardware and performance features. Then click **Next**.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_6.png" width="725" />

<br/>

7. Select the **Guest OS Family** for your family of operating system based on your ISO file. Then select the appropriate **Guest OS Version** and hit **Next**. We'll use **Windows** for the family and **Microsoft Windows Server 2012 (64-bit)** for the version.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/iso_1.png)

<br/>

8. Customize your virtual hardware settings.
   1. Select how many CPUs needed for your OS and operations
   2. Select how much Memory for your OS and operations
   3. Select Hard Disk size for your OS and operations
   4. Select `Browse` in **New Network** dropdown menu and choose the `VM Lab` network to ensure proper connectivity to the web.
   5. Under **New CD/DVD Drive** select `Datastore ISO File`. Then navigate to where your ISO file is stored in the lab and select it. Then click **OK**.
   6. Ensure you click `Connect at Power On` for the CD/DVD drive.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/iso_2.png" width="725" />

<br/>

9. Finish customizing your hardware/firmware as needed. Then click **Next**.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/iso_3.png" width="725" />

<br/>

10. Inspect your settings to ensure nothing was missed. When you're ready, click **Finish**. Then, navigate to your VM in vSphere and click the green play (`start`) button to boot. Then click `Launch Web Console` to open the console.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/iso_4.png" width="725" />

<br/>

11. Walk through the process of installing your operating system. The steps will vary depending on OS family and version.

### Congratulations!!

You've successfully created a custom VM with your own OS! Log in with the credentials you set up during the OS installation process, and you're ready to go.

> <sup>**NOTE**: This will not register the VM with DNS, nor will it setup LDAP authentication with the Active Directory. You will have to do that manually for your VM, if you so desire.</sup>
