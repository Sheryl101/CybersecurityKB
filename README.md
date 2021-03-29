## Azure vm set-up:
[Jumpbox/Web Servers](https://github.com/Sheryl101/CybersecurityKB/blob/91a88c340673a464aa53ac1fe7cea10891bcbc2f/AZURE%20vm%20set-up/Jumpbox_%20web-1%20_web-2%20setup.pdf)


## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![image](https://user-images.githubusercontent.com/45856811/112399316-43446800-8cc3-11eb-9f10-8cad9ea827d3.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

[Ansible Playbook](https://github.com/Sheryl101/CybersecurityKB/blob/4c08a89b5254d01abb38a3baec328a6394c9000f/Ansible/ansible.cfg)

[Ansible Hosts File](https://github.com/Sheryl101/CybersecurityKB/blob/4c08a89b5254d01abb38a3baec328a6394c9000f/Ansible/hosts.txt)

[ELK Playbook](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/install-elk.yml)


### This document contains the following details:

Description of the Topology

Access Policies

ELK Configuration

Beats in Use

Machines Being Monitored


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

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
| web-1     | Azure VM           | 10.0.0.5   | 52.148.177.153 (LB)| Linux         |
| web-2     | Azure VM           | 10.0.0.6   | 52.148.177.153 (LB)| Linux         |
| web-3     | Azure VM           | 10.0.0.7   | 52.148.177.153 (LB)| Linux         |
| ELK-Server| Analytics Platform | 10.1.0.5   | 52.184.167.220  | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. 

Machines within the network can only be accessed by my home IP address.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 13.77.182.22         |
| web-1    | No                  | 10.0.0.5             |
| web-2    | No                  | 10.0.0.6             |
| web-3    | No                  | 10.0.0.7             |


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
- web-1 10.0.0.5
- web-2 10.0.0.6
- web-2 10.0.0.7

BEFORE DOING ANYTHING MAKE SURE YOU START AND ATTACH YOUR DOCKER CONTAINER WITH: sudo docker container start and sudo docker container attach TO DO THIS MAKE SURE YOU HAVE RAN ansible-playbook install-elk.yml OR THESE BEATS WILL NOT FIND ANYTHING TO MONITOR!

The following Beats are on these machines:
- Filebeat 
- Metricbeat 

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

[Filebeat Playbook](https://github.com/Sheryl101/CybersecurityKB/blob/4c08a89b5254d01abb38a3baec328a6394c9000f/Docker/filebeat-playbook)

[Filebeat Configuration](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/filebeat-config.yml)


- Scroll to line #1106 and replace the IP address with the IP address of your ELK machine, 10.1.0.5 for the purposes of my setup.
- Scroll to line #1806 and replace the IP address with the IP address of your ELK machine, 10.1.0.5 for the purposes of my setup.
- Run the playbook with ansible-playbook filebeat-configuration.yml.
- Next, confirm that the ELK stack was receiving logs. 
- Navigate back to the Filebeat installation page on the ELK server GUI.
- Verify that your playbook is completing Steps 1-4.
- On the same page, scroll to Step 5: Module Status and click Check Data.
- Scroll to the bottom and click on Verify Incoming Data.
- If the ELK stack was successfully receiving logs, you would have seen:

[Success](https://github.com/Sheryl101/CybersecurityKB/blob/main/Diagrams/kibana.PNG)

- Copy the metricbeat-configuration.yml file to /etc/ansible/files.

[Metricbeat Configuration](https://github.com/Sheryl101/CybersecurityKB/blob/d1395f8fb97038344e168e2912e558b1de3dd9c5/Docker/metricbeat-config)

- Copy the metricbeat-configuration.yml file to /etc/ansible/files.

[Metricbeat Playbook](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/metricbeat-playbook)

- Scroll to line #1106 and replace the IP address with the IP address of your ELK machine, 10.1.0.5 for the purposes of my setup.
- Scroll to line #1806 and replace the IP address with the IP address of your ELK machine, 10.1.0.5 for the purposes of my setup.

- Run ansible-playbook metricbeat-configuration.yml
- To verify that your play works as expected, on the Metricbeat installation page in the ELK server GUI, scroll to Step 5: Module Status and click Check Data.
