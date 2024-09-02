# SOC Automation Lab


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
This configuration should ensure that the machine runs smoothly.

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

