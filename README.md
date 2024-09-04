![image](https://github.com/user-attachments/assets/a08c5bf6-90b5-46a3-95bf-847a7899c243)# SOC Automation Lab


## Project Introduction
This SOC Automation Lab project is all about setting up a mini Security Operations Center (SOC) at home. Using tools like Wazuh, Shuffle, and TheHive, the goal is to build a SOAR (Security Orchestration, Automation, and Response) system that can automatically detect, analyze, and respond to security threats without needing constant human input. It's a hands-on way to learn how to get different security tools to work together, enrich threat data, and automate responses, making the whole process smoother and more efficient.

![SocAutomation drawio (1)](https://github.com/user-attachments/assets/d46b6dfe-6d38-46e2-9cbf-1dc4e21f4ef0)

### Skills Learned
- Grasping how SOAR systems work and how to set them up.
- Integrating and automating different security tools.
- Getting better at spotting threats and responding automatically.
- Learning how to enrich security alerts with additional data.
- Building workflows that make security operations quicker and easier.
### Tools Used
- Wazuh for monitoring security events and analyzing data.
- Shuffle for creating automation workflows that handle alerts and incidents.
- TheHive for managing incidents and helping the team collaborate.
- Sysmon for detailed system monitoring on the Windows Wazuh Agent, capturing key event data.

## Steps

### 1. Install Applications & Virtual Machines
We'll kick off our project by setting up the necessary virtual machines and tools in our lab environment. This step involves the installation, configuration, and implementation of the key components we'll be using.

By the end of this step, we will have:
- A Windows 10 machine with Sysmon installed.
- A Wazuh Server.
- A TheHive Server.
#### 1.1 VirtualBox Installation
For virtualization, we will use VirtualBox software, which will provide us with the environment needed to deploy virtual machines. You can download and install VirtualBox from their official website https://www.virtualbox.org/wiki/Downloads

During installation, it's recommended to compare the checksums to verify the integrity of the downloaded file. You can find more information about this on the VirtualBox downloads page.

#### 1.2 Windows 10 Installation
Start by downloading the Windows 10 installation media from the official Microsoft website https://www.microsoft.com/en-us/software-download/windows10 Then follow these steps:
1. Choose the option to create installation media for a different computer.
2. Select the option to download an ISO file.
3. Choose your desired location and complete the download.

In VirtualBox, click on "New" to create a new virtual machine. When prompted, select the Windows 10 ISO file you downloaded earlier.

![image](https://github.com/user-attachments/assets/eec4140e-a27c-4d9c-bb4a-62e259965da9)


I recommend selecting "Unattended Installation" if you want to manually install the OS, but you can choose to do this differently if you prefer. Next, you'll be asked to configure the hardware specifications for your virtual machine. Here's a recommended setup:
- At least 4 GB of RAM.
- 2 CPUs.
- 50 GB of storage.
This configuration should ensure that the machine runs smoothly, but consider your host PC capabilities.

![image](https://github.com/user-attachments/assets/2f96a6c8-d1ed-41ea-984f-91790db64f3a)

Once configured, you should see your machine listed in the VirtualBox dashboard.

Launch your virtual machine and proceed with the Windows installation. During the process, when asked for a product key, select "I don't have a product key." Then, choose "Windows 10 Pro" as the version to install. Select "Custom: Install Windows only" to continue. Windows will now begin installing in the background.

![image](https://github.com/user-attachments/assets/bac583e8-8231-449d-b432-63f40a5c3768)

#### 1.3 Install VirtualBox Guest Additions
To enhance your Windows 10 virtual machine's performance and enable features like shared folders, improved video support, and seamless mouse integration, we'll install VirtualBox Guest Additions. Here’s how to do it:
1. With your Windows 10 virtual machine running, click on "Devices" in the VirtualBox menu.
2. Select "Insert Guest Additions CD Image" from the dropdown menu.
3. Open "This PC" in Windows Explorer, where you will see the Guest Additions CD drive.
4. Double-click the drive to open it, then run the installation file (VBoxWindowsAdditions.exe).
5. Follow the prompts to complete the installation.
Once the installation is finished, restart your virtual machine to apply the changes.

![image](https://github.com/user-attachments/assets/4bb97b74-a28a-4868-8ad1-c9306798d99a)
![image](https://github.com/user-attachments/assets/aed61c5d-0d81-4e0d-b346-84ee7ccf2cc5)

#### 1.4 Install Sysmon for Enhanced Event Tracking
The final step in setting up your Windows 10 machine is to install Sysmon from Sysinternals. Sysmon is a powerful tool that significantly enhances your event tracking capabilities, making it invaluable for monitoring system activity and detecting potential threats. This will be crucial for the practical examples and use cases we'll explore in this project.

Here’s how to get Sysmon up and running:

1. Download Sysmon:
    Visit the official Sysmon download page on Microsoft’s website. https://learn.microsoft.com/pl-pl/sysinternals/downloads/sysmon
    Download the latest version of Sysmon to your Windows 10 virtual machine. 
2. Obtain a Configuration File:
    - To configure Sysmon effectively, you'll need a well-balanced configuration file. A great resource for this is the Sysmon Modular project on GitHub.
    - Go to Sysmon Modular on GitHub. https://github.com/olafhartong/sysmon-modular
    - Look for the sysmonconfig.xml file. This file offers a balanced configuration for Sysmon, providing a good mix of detailed event logging without overwhelming your system with excessive data.
   
    ![image](https://github.com/user-attachments/assets/16b1cfee-523c-4266-86b2-10619b559220)
    ![image](https://github.com/user-attachments/assets/b2a28cd9-07ac-4241-8b3e-3914bd9d0f1c)

3. Install Sysmon with the Configuration:
    - Once you have both Sysmon and the sysmonconfig.xml file, open a command prompt with administrative privileges.
    - Navigate to the directory where you downloaded Sysmon.
    - Run the following command to install Sysmon with your chosen configuration file:
    ```
    sysmon -accepteula -i sysmonconfig.xml
    ```
    This command installs Sysmon, accepts the license agreement, and applies the balanced configuration from the sysmonconfig.xml file.
   ![image](https://github.com/user-attachments/assets/2b139299-45ad-4381-a941-d651892042a9)

5. Restart your virtual machine to ensure that Sysmon starts logging events
6. Check if Sysmon is running:

   You can easily check is Sysmon is running by examining event logs itself, just head to the Event Viewer and find Sysmon logs.
   **Applications and Services -> Microsoft -> Windows -> Sysmon**
    ![image](https://github.com/user-attachments/assets/ddb26fe8-144b-4edd-89fe-8f5960f9afda)

#### 1.5 Install Ubuntu VMs
To complete this step, we'll install Ubuntu systems for our Wazuh Manager and TheHive. Both TheHive and Wazuh are compatible with Ubuntu 22.04 LTS.

**Wazuh Installation**

![image](https://github.com/user-attachments/assets/1dc71d67-85b4-43de-9342-e061b1903276)

I'll be using DigitalOcean's cloud services for both virtual machines to conserve local computer resources. You can choose any cloud provider or create additional VMs on your local machine. I opted for DigitalOcean because they offer a free $200 credit, which should be sufficient to complete our project without incurring any costs.
Next, we'll set up the Wazuh Manager on a DigitalOcean droplet (DigitalOcean's term for virtual machines). 
Follow these steps:
- Navigate to the DigitalOcean dashboard and click on **Create -> Droplets.**
- Select a region that is **geographically closest** to you for better latency and performance.
- Choose **Ubuntu 22.04 LTS** as the operating system image.
- Select a droplet with **8 GB of RAM** and **50 GB of storage** to ensure it can handle the Wazuh Manager's requirements.
- For security, especially since this machine will be exposed to the internet, choose a **strong authentication method**. I will be using password, but if you prefer, you can select a SSH keys. Ensure the password is strong and unique.
- Give your droplet a meaningful name, such as** "WazuhManager"**, to easily identify it in your dashboard.
- Once you've configured everything, click **Create Droplet** to start the deployment process.

![image](https://github.com/user-attachments/assets/0b8e391a-449c-40a7-9f52-89de3f25de30)

While your droplet is deploying, it's important to secure it by setting up firewall rules. We'll configure the firewall to only allow traffic from your machine to this VM.
Navigate to **Networking** and **Firewalls**

![image](https://github.com/user-attachments/assets/85d0d3bf-d57d-40e9-9b86-0c3f8fd44fbd)

By default, DigitalOcean allows SSH access to your droplet from any machine, but we want to restrict that to ensure your Wazuh Manager droplet is secure. We’ll create inbound firewall rules to block all traffic except from your local computer. These rules will cover both TCP and UDP traffic. For the source IP, use your public IP address, which you can find at [WhatIsMyIP.com.](https://www.whatismyip.com/)

Once you've created the firewall, navigate to the **Droplets** section in your DigitalOcean dashboard, select your **droplet**, go to **Networking**, and scroll down to the **Firewalls** section. Click **Edit**, then select the firewall you just created. Under **Droplets**, click **Add Droplets**, and select your **Wazuh Manager VM**.

Now, the firewall is applied to your droplet, securing it by restricting access to only your machine.

![image](https://github.com/user-attachments/assets/9a3a99aa-96d2-4a9e-8d9b-9889c77ac0de)

You can access the droplet through the DigitalOcean web interface. To do this, go to your droplet's page, select **Access** from the menu, and then click **Launch Console**.

Personally, I encountered an issue when trying to connect to the droplet through the DigitalOcean console. If you face the same problem, I recommend using PuTTY as an alternative. PuTTY is a free SSH client that works well for connecting to your droplet.

![image](https://github.com/user-attachments/assets/04158d34-d68f-4ea8-86a6-b34ab5a57e61)

Once you're connected to the Wazuh Manager droplet, it's time to install Wazuh. But first, make sure to update and upgrade your system:
```
sudo apt update
sudo apt upgrade
```
After your system is updated, you can proceed with the Wazuh installation by running the following commands:
```
curl -sO https://packages.wazuh.com/4.8/wazuh-install.sh
sudo bash wazuh-install.sh -a
```
After the installation is complete, take note of the username and password generated for the Wazuh web interface. You’ll need these credentials to log in later.

To finish setting up Wazuh, open your web browser and enter the public IP address of your Wazuh Manager VM. This will take you to the Wazuh web interface where you can complete the installation process and start configuring your security monitoring environment.

![image](https://github.com/user-attachments/assets/70efea8e-8630-490f-94d5-48a742afb75d)

**TheHive Installation**

For the TheHive server, follow the same process as you did for the Wazuh Manager droplet. This includes creating and configuring the droplet, assigning the firewall, and updating the operating system.

![image](https://github.com/user-attachments/assets/df7c0f40-ab63-49b7-9109-05531c0aa3fe)

The only difference at this stage is that you'll be installing TheHive instead of Wazuh on this system. TheHive installation instructions:
1. Install dependencies:
   ```
   apt install wget gnupg apt-transport-https git ca-certificates ca-certificates-java curl software-properties-common python3-pip lsb-release
   ```
2. Install Java:
    ```
    wget -qO- https://apt.corretto.aws/corretto.key | sudo gpg --dearmor  -o /usr/share/keyrings/corretto.gpg
    echo "deb [signed-by=/usr/share/keyrings/corretto.gpg] https://apt.corretto.aws stable main" |  sudo tee -a /etc/apt/sources.list.d/corretto.sources.list
    sudo apt update
    sudo apt install java-common java-11-amazon-corretto-jdk
    echo JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto" | sudo tee -a /etc/environment 
    export JAVA_HOME="/usr/lib/jvm/java-11-amazon-corretto"
    ```
3. Install Cassandra:
   ```
   wget -qO -  https://downloads.apache.org/cassandra/KEYS | sudo gpg --dearmor  -o /usr/share/keyrings/cassandra-archive.gpg
   echo "deb [signed-by=/usr/share/keyrings/cassandra-archive.gpg] https://debian.cassandra.apache.org 40x main" |  sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
   sudo apt update
   sudo apt install cassandra
   ```
4. Install ElasticSearch
    ```
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch |  sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
    sudo apt-get install apt-transport-https
    echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/7.x/apt stable main" |  sudo tee /etc/apt/sources.list.d/elastic-7.x.list
    sudo apt update
    sudo apt install elasticsearch
    ```
    Optionally:
       Create a jvm.options file under /etc/elasticsearch/jvm.options.d and put the following configurations in that file.
   ```
   -Dlog4j2.formatMsgNoLookups=true
   -Xms2g
   -Xmx2g
   ```
5. Install TheHive
    ```
    wget -O- https://archives.strangebee.com/keys/strangebee.gpg | sudo gpg --dearmor -o /usr/share/keyrings/strangebee-archive-keyring.gpg
    echo 'deb [signed-by=/usr/share/keyrings/strangebee-archive-keyring.gpg] https://deb.strangebee.com thehive-5.2 main' | sudo tee -a /etc/apt/sources.list.d/strangebee.list
    sudo apt-get update
    sudo apt-get install -y thehive
    ```
For more details you can check TheHive installation guide on their official website https://docs.strangebee.com/thehive/installation/step-by-step-installation-guide/

### 2.TheHive Configuration
We installed alot of services for our TheHive, now we need to configure it.

#### 2.1 Cassandra Configuration
We'll start by configuring Cassandra, which is used for storing NoSQL data.
1. Edit the Configuration File: Open the Cassandra configuration file located at /etc/cassandra/cassandra.yaml.

![image](https://github.com/user-attachments/assets/1eb042e5-c8a6-47e6-bf40-a940855fbcaa)

2. Find **listen_address** variable and then set the address to the public IP address of your TheHive server

![image](https://github.com/user-attachments/assets/9251032c-944d-42fe-bda7-f70ec5c5fc16)

3. Update the rpc_address: Set the rpc_address to the public IP address of your TheHive server.

![image](https://github.com/user-attachments/assets/6e18520a-dc37-48a9-81f1-7eecbad3541e)

3. Configure the Seed Provider: Locate the seed_provider section and update the seeds parameter with the public IP address of your TheHive server.

![image](https://github.com/user-attachments/assets/dd283e63-b84e-4725-91d8-f841ec056155)

4. Save and Stop the Cassandra Service: After making these changes, save the file and stop the Cassandra service. This will prepare it for a clean start. ```systemctl stop cassandra.service```
5. Cleanup Old Files: Since TheHive was installed from its package, you may need to remove any old or conflicting files that could interfere with the new setup. ```rm -rf /var/lib/cassandra/*```
5. Start the Cassandra Service: Once the cleanup is complete, restart the Cassandra service to apply the changes. ```systemctl start cassandra.service```
6. Verify the Configuration: To ensure everything is working correctly, check the status of the Cassandra service: ```systemctl status cassandra.service```


#### 2.2 ElasticSearch Configuration
Next we will configure ElasticSearch used for querying data.
1. Edit the Configuration File: Open the ElasticSearch configuration file located at /etc/elasticsearch/elasticsearch.yml.

![image](https://github.com/user-attachments/assets/d97b7bf9-dec5-49c4-a3ae-f61de1cf1753)

2. Uncomment **cluster.name** and name it ex. thehive
3. Uncomment **node.name**
4. Uncomment **network.host** and put public ip address of TheHive VM
5. Uncomment **http.port**, by default ElasticSearch uses port 9200
6. ElasticSearch requires either **discovery.seed_host**s or **cluster.initial_master_nodes** to be set to start up properly. We will uncomment cluster.initial_master_nodes and because we work in micro environement we will remove node-2, leaving only node-1 (or whatever name you set for your node).

Save changes and enable elasticsearch
```
systemctl start elasticsearch
systemctl enable elasticsearch
```

![image](https://github.com/user-attachments/assets/7de2f599-5ec0-40c8-9520-4ace3075ae81)

#### 2.3 TheHive configuration
Before we actually start configuring TheHive we need to ensure that thehive user and group have has access to the thehive path
```
ls -la /opt/thp
```

![image](https://github.com/user-attachments/assets/5a1b37ab-a6fd-4a69-a2ea-fa8d481eb5ac)

As you see, root user and group have access to thehive, we want to change this.
```
chown -R thehive:thehive /opt/thp
```
This will change owner of thehive to thehive user and group

![image](https://github.com/user-attachments/assets/dfc090a1-a8d4-43cd-bb1e-516e18102d3a)

