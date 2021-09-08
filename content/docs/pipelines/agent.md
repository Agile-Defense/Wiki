---
title: "Configure a GoCD Agent"
description: "Configure a Default GoCD Agent"
lead: "Configure a Default GoCD Agent"
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "pipelines"
weight: 60
toc: true
---

### Setup

Log in to the VM you would like to configure as a Default GoCD Agent. If you do not have one, you can [Provision One →]({{< relref "provision" >}}).

{{< alert icon="👉" text="This guide assumes you have <b>sudo</b> access. If you do not, you will not be able to configure the GoCD Agent." />}}

### Configure

There are two ways you can configure the vm:

1. You can download the script from inside the vm via `curl`:

```bash
curl https://raw.githubusercontent.com/Agile-Defense/scripts/master/GoCD/configure_default_agent.sh -O configure_default_agent.sh
chmod +x configure_default_agent.sh
```

or via `wget`:

```bash
wget https://raw.githubusercontent.com/Agile-Defense/scripts/master/GoCD/configure_default_agent.sh
chmod +x configure_default_agent.sh
```

Then run it with 

```bash
./configure_default_agent.sh
````

It will automatically clean up after itself too.

2. If you cannot download it for any reason, just copy and paste this into your terminal:

```bash
#!/bin/bash

# Add go-agent to sources list for apt
echo "deb https://download.gocd.org /" | sudo tee /etc/apt/sources.list.d/gocd.list

# Add go-agent key apt-key
curl https://download.gocd.org/GOCD-GPG-KEY.asc | sudo apt-key add -

# Run update to pull latest go-agent into apt
sudo apt-get update

# Install go-agent
sudo apt-get install go-agent

# Configure go-sever for agent
sudo sed -i -e 's/localhost:8153/gocd.agiledefense.lab/' /usr/share/go-agent/wrapper-config/wrapper-properties.conf

# Start and enable go-agent
sudo systemctl start go-agent
sudo systemctl enable go-agent

# Download sonar-scanner zip file
wget -O sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.6.2.2472-linux.zip

# Install unzip to unzip zipfile (not installed by default)
sudo apt-get -y install unzip

# Unzip sonar-scanner files
sudo unzip sonar-scanner.zip -d /etc

# Rename directory for better management and linking
sudo mv /etc/sonar-scanner-* /etc/sonar

# Configure default sonar server
sudo sed -i -e 's/#sonar.host.url=http:\/\/localhost:9000/sonar.host.url=http:\/\/sonar.agiledefense.lab/' /etc/sonar/conf/sonar-scanner.properties

# Create symlinks to binaries so they're availabel on system PATH
sudo ln -s /etc/sonar/bin/sonar-scanner /usr/bin/sonar-scanner
sudo ln -s /etc/sonar/bin/sonar-scanner-debug /usr/bin/sonar-scanner-debug

# Install pip3 apt package
sudo apt install -y python3-pip

# Pip install dependency-check (use sudo so it installs bin file on PATH)
sudo pip3 install dependency-check

# Install Java 11 for dependency-check
sudo apt install -y openjdk-11-jdk-headless

# Generate SSH key for go user
sudo su - go -c 'ssh-keygen -b 2048 -t rsa -f /var/go/.ssh/id_rsa -q -N ""'


# Register Key with GitHub
registration_status=$(curl -G -X POST -v --data-urlencode "key=$(sudo cat /var/go/.ssh/id_rsa.pub)" --data-urlencode "host=$(hostname)" "http://gocd.agiledefense.lab:6523/register-ssh-key")
if [[ "$registration_status" == *"successful"* ]]
then
	echo "Sucessfully registered ssh key with GoCD-Agent github account"
else
	echo "Failed to register: $registration_status" && exit 1
fi

# Perform initial pull to add ssh-key to known hosts
sudo su - go -c 'if [ ! -n "$(grep "^github.com " ~/.ssh/known_hosts)" ]; then ssh-keyscan github.com >> ~/.ssh/known_hosts 2>/dev/null; fi; git clone git@github.com:Agile-Defense/GoAgentPullTest.git'
sudo rm -rf /var/go/GoAgentPullTest
sudo rm -rf sonar-scanner.zip
sudo rm -rf configure_default_agent.sh
```

### Enabling, Environments, and Resources

After the script finishes and cleans up, you need to navigate to [GoCD Agents Tab](http://gocd.agiledefense.lab/go/agents) and check the box next to the Agent you just configured. You will see it is not enabled yet. Click `Enable` to enable it. 

After it's been enabled, add it to the requisite environments by checking the box next to it again, clicking the `Environments` drop down menu, selecting the environments, and clicking **Apply**.

Lastly, check the box again and click the `Resources` drop down menu. From here, select all of the resources you've installed. If you just ran the script and have not installed any other resources, select `Python3`, `GitHub`, `dependency-check`, and `sonar-scanner`. If you used a [net-booted]({{< relref "net-booting" >}}) VM, you can also select `Linux-Ubuntu`. Then click **Apply**.


  