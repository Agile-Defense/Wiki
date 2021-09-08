---
title: "Net Booting from PXE"
description: "How to provision a new virtual machine in Innovations Lab vSphere"
lead: "How to provision a new virtual machine via Net Boot"
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "provisioning"
weight: 11
toc: true
---

### Setup
First, ensure you have a VPN connection to the O'Fallon Lab, have valid Innovations Lab credentials, and can log into [Innovations Lab vSphere](https://adlbvc01.agiledefense.lab/ui/)

### Provision

1. Right click on **DellCluster** and select **New Virtual Machine**.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_1.png)

<br/>

2. Select **Create a new virtual machine** if it isn't selected already and click **Next**.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_2.png)

<br/>

3. Give your VM a name, then click **Next**. 

{{< alert icon="👉" text="<b>NOTE</b>: The name given will end up being the hostname of the vm, as well as the DNS routing name. <br><br> (e.g. if you name it <b>Test_VM</b>, the hostname will be <b>TestVM</b> because underscores get removed and the DNS endpoint will be <b>test_vm.agiledefense.lab</b>)." />}}

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

7. Select `Linux` for **Guest OS Family** and `Ubuntu Linux (64-bit)` for **Guest OS Version** and hit **Next**.

![img](https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_7.png)

<br/>

8. Customize your virtual hardware settings.
   1. Select how many CPUs (`Recommend a minimum of 2`)
   2. Select how much Memory (`Recommend a minimum of 2GB`)
   3. Select Hard Disk size (`Recommend a minimum of 50GB`)
   4. Select `Browse` in **New Network** dropdown menu and choose the `VM Lab` network to ensure proper connectivity to the web.
   5. Customize the rest of the hardware to your desired specifications

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_8.png" width="725" />

<br/>

9. Select **VM Options** while still in the **Customize hardware** menu and under **Boot Options** select `EFI` for **Firmware**, otherwise it will not boot properly.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_9.png" width="725" />

<br/>

10. Now scroll down and expend the **Advanced** tab of the **VM Options** menu. The click **EDIT CONFIGURATION** under the **Configuration Parameters** section. Then click **ADD CONFIGURATION PARAMS**. Under **Name**, type or copy/paste `guestinfo.hostname`. Under the **Value** type the name of your vm. In this case, it was `Test_VM`. Click **OK** and lastly, click **Next**

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_10.png" width="725" />

<br/>

11. Inspect your settings to ensure nothing was missed. When you're ready, click **Finish**. Then, navigate to your VM in vSphere and click the green play (`start`) button to initiate cloud init.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_11.png" width="725" />

<br/>

12. After 15-20 minutes, and several reboots, you should be able to ssh to your new vm utilizing your lab username and password.

<img src="https://raw.githubusercontent.com/Agile-Defense/agile-defense.github.io/main/assets/images/netboot_12.png" width="725" />


### Congratulations!!

You've successfully net booted your first Linux VM in the Innovations Lab. For any issues that may arise during any of these steps, please see the [FAQ]({{< relref "faq" >}}).
