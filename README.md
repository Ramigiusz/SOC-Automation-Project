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
- A Windows 10 machine with Sysmon installed
- A Wazuh Server
- A TheHive Server
