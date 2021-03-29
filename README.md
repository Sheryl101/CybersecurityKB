<<<<<<< HEAD
# CybersecurityKB
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/Sheryl101/CybersecurityKB/blob/3b38ff5bbb11224cd40b9c911825cf531e9d0c79/Diagrams/Network%20Diagram%20(ELK).pdf

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build
=======
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![image](https://user-images.githubusercontent.com/45856811/112399316-43446800-8cc3-11eb-9f10-8cad9ea827d3.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

[Ansible Playbook](https://github.com/Sheryl101/CybersecurityKB/blob/4c08a89b5254d01abb38a3baec328a6394c9000f/Ansible/ansible.cfg)

[Ansible Hosts File](https://github.com/Sheryl101/CybersecurityKB/blob/4c08a89b5254d01abb38a3baec328a6394c9000f/Ansible/hosts.txt)

[ELK Playbook](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/install-elk.yml)

[filebeat Playbook](https://github.com/Sheryl101/CybersecurityKB/blob/4c08a89b5254d01abb38a3baec328a6394c9000f/Docker/filebeat-playbook)

[metricbeat Playbook](https://github.com/Sheryl101/CybersecurityKB/blob/4c08a89b5254d01abb38a3baec328a6394c9000f/Docker/metricbeat-playbook)




### This document contains the following details:

Description of the Topology

Access Policies

ELK Configuration

Beats in Use

Machines Being Monitored

How to Use the Ansible Build
>>>>>>> 911328aa1c58cbf79fba8f110660430990578f75


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

<<<<<<< HEAD
Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_
- _TODO: What does Metricbeat record?_

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| TODO     |          |            |                  |
| TODO     |          |            |                  |
| TODO     |          |            |                  |
=======
Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.
- Load balancers add resiliency by rerouting live traffic from one server to another if a server falls prey to a DDoS attack or otherwise becomes unavailable.
- A Jump Box Provisioner is also important as it prevents Azure VMs from being exposed via a public IP Address.  This allows us to do monitoring and logging on a single box.  We can also restrict the IP addresses able to communicate with the Jump Box, as we've done here.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filebeat collects data about the file system.
- Metricbeat collects machine metrics such as uptime.

The configuration details of each machine may be found below.

| Name      | Function           | IP Address | Public IP       |Operating System |
|-----------|--------------------|------------|-----------------|------------------|
| Jump Box  | Gateway            | 10.0.0.4   | 13.77.182.22    | Linux            |
| DVWA-VM1  | Azure VM           | 10.0.0.5   | Load Balancer   | Linux            |
| DVWA-VM2  | Azure VM           | 10.0.0.6   | Load Balancer   | Linux            |
| DVWA-VM3  | Azure VM           | 10.0.0.7   | Load Balancer   | Linux            |
| ELK-Server| Analytics Platform | 10.1.0.5   | 52.184.167.220  | Linux            |
>>>>>>> 911328aa1c58cbf79fba8f110660430990578f75

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

<<<<<<< HEAD
Only the _____ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_

Machines within the network can only be accessed by _____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
=======
Only the Jump Box Provisioner machine can accept connections from the Internet. 

Machines within the network can only be accessed by my home IP address.
>>>>>>> 911328aa1c58cbf79fba8f110660430990578f75

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
<<<<<<< HEAD
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.
=======
| Jump Box | Yes                 | 13.77.182.22         |
| DVWA-VM1 | No                  | 10.0.0.4             |
| DVWA-VM2 | No                  | 10.0.0.4             |
| DVWA-VM3 | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for setup in minutes using OpenSSH without installing anything on the servers.


The playbook implements the following tasks:
- Install Docker.io
- Install Python-pip
- Increase Virtual Memory
- Download and Launch ELK Docker Container (image sebp/elk)
- Published ports 5044, 5601 and 9200 were made available 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/elk.png)

### Beats in Use and Machines being Monitored
This ELK server is configured to monitor the following machines:
- DVWA-VM1 10.0.0.5
- DVWA-VM2 10.0.0.6
- DVWA-VM2 10.0.0.7

The following Beats are on these machines:
- Filebeat 
- - Metricbeat 

These Beats allow us to collect the following information from each machine:
- Filebeat will be used to collect log files from very specific files such as Apache, Azure tools and web servers.
- Metericbeat will be used to monitor VM stats, per CPU core stats, per filesystem stats, memory stats and network stats.

### How to Use the Ansible Build
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- SSH into the ELK Container ssh sysadmin@10.0.0.4 for my setup
- Run docker container list -a to verify that the container is on.
- If it isn't, run docker start sebp/elk.
- Exit the ELK Container
- Navigate to (Your IP Address):5601 from your web browser.
- Open your ELK server homepage
- Click on Add Log Data.
- Click on the DEB tab under Getting Started to view the correct Linux Filebeat installation instructions.
- Choose System Logs.
- Copy the filebeat-playbook.yml file to /etc/ansible/roles
- Run the playbook (ansible-playbook filebeat-playbook.yml), and navigate to http://52.184.167.220:5601/app/kibana to check that the installation worked as expected.
>>>>>>> 911328aa1c58cbf79fba8f110660430990578f75

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
