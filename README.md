## Azure vm set-up:
[Jumpbox/Web Servers](https://github.com/Sheryl101/CybersecurityKB/blob/91a88c340673a464aa53ac1fe7cea10891bcbc2f/AZURE%20vm%20set-up/Jumpbox_%20web-1%20_web-2%20setup.pdf)

# Automated ELK Stack Deployment
---------------------------------

The files in this repository were used to configure the network depicted below.

![ELK diagram](https://github.com/Sheryl101/CybersecurityKB/blob/main/Diagrams/NeworkDiagramELK.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Each portion of the playbook is broken down into individual playbooks, so that only certain pieces might be installed, such as Filebeat or Metricbeat only. 

  - [DVWA playbook](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/DVWA.yml)
  - [ELK playbook](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/install-elk.yml)
  - [Filebeat playbook](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/filebeat-playbook)
  - [Metricbeat playbook](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/metricbeat-playbook)
  - [Filebeat config](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/filebeat-config.yml)
  - [Metricbeat config](https://github.com/Sheryl101/CybersecurityKB/blob/main/Docker/metricbeat-config)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build
  
---------------------------------

## Description of the Topology
---------------------------------

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive and fault tolerant, in addition to restricting access to the network. By setting up a jump box, we limit the footprint of publicly accessible systems on the network, and also keep all management of playbooks and deployment organized.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat ships log files.
- Metricbeat ships metrics from the various machines' operating systems and services. (For ex: Apache, Ngnix, or MySQL)

The configuration details of each machine may be found below.

| Name               | Function | IP Address               | Operating System     |
|--------------------|----------|--------------------------|----------------------|
| JumpBoxProvisioner | Gateway  | 13.77.182.22  / 10.0.0.4 | Linux / Ubuntu 18.04 |
| Web1               | DVWA     | 10.0.0.5                 | Linux / Ubuntu 18.04 |
| Web2               | DVWA     | 10.0.0.6                 | Linux / Ubuntu 18.04 |
| Web3               | DVWA     | 10.0.0.7                 | Linux / Ubuntu 18.04 |
| ELK                | ELK Stack| 52.184.167.220 / 10.1.0.5| Linux / Ubuntu 18.04 |

---------------------------------

## Access Policies
---------------------------------

The JumpBoxProvisioner machine can accept limited connections from the Internet. Access to this machine is only allowed from the following IP address and at the following port:
- 13.77.182.22 / port 22

The Azure Load Balancer can accept connections from the Internet. TCP protocol is allowed from the following IP addresses and at the following port:
- any / port 80

The machines on the internal network with only private IPs (Web1, Web2, Web3) are not directly exposed to the public Internet. Web1, Web2 and Web 3 can accept TCP traffic from the JumpBoxProvisioner, from the following IP and port:
- 10.0.0.4 / port 22  
  
Web1, Web2 + Web3 can also accept any TCP traffic from the following Azure Load Balancer, as part of its backend pool setup, from the following IP and port:
- 52.148.177.153 / port 80

The ELK machine can accept limited connections from the Internet. ELK can accept TCP traffic from the workstation, from the following IP and port:
- 52.184.167.220 / port 5601

The ELK machine (on VNet2) can also accept traffic from VNet1, as they are peered virtual networks.  
Published ports:  
- 5044
- 5601
- 9200

A summary of the public access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP Addresses | Allowed Ports | Allowed Traffic |
|--------------------|---------------------|----------------------|---------------|-----------------|
| JumpBoxProvisioner | Yes                 | 13.77.182.22         | 22            | Any             |
| Web1               | no public IP        | 52.148.177.153 (LB)  |               |                 |
| Web2               | no public IP        | 52.148.177.153 (LB)  |               |                 |
| Web3               | no public IP        | 52.148.177.153 (LB)  |               |                 |
| ELK                | Yes                 | 52.184.167.70        | 5601          | TCP             |

---------------------------------

## DVWA Configuration
---------------------------------

Ansible was used to automate configuration of the DVWA machines. No configuration was performed manually, which is advantageous because one can repeatedly install the same configuration on machines quickly and at scale.

The playbook implements the following tasks:
- Uses apt to install docker.io and python3.
- Uses pip to install docker.
- Installs DVWA container and sets published ports to 80:80.


The following screenshot displays the result of running `docker ps` after successfully configuring the DVWA instance.

![screenshot of docker ps output](https://github.com/Sheryl101/CybersecurityKB/blob/main/Images/docker_ps_dvwa.png)

### Target Machines
This playbook configured the DVWA instance on the following machines:
- Web1 - 10.0.0.5
- Web2 - 10.0.0.6
- Web3 - 10.0.0.7  

---------------------------------

## Elk Configuration
---------------------------------

Ansible was also used to automate configuration of the ELK machine. 

The playbook implements the following tasks:
- Increases virtual memory with sysctl.
- Uses apt to install docker.io and python3.
- Uses pip to install docker.
- Installs ELK container and sets published ports to 5044:5044, 5601:5601, and 9200:9200.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![screenshot of docker ps output](https://github.com/Sheryl101/CybersecurityKB/blob/main/Images/docker_ps_elk.png)

### Target Machines & Beats
This ELK server:
- ELK - 10.1.0.5 

is configured to monitor the following machines:
- Web1 - 10.0.0.5
- Web2 - 10.0.0.6
- Web3 - 10.0.0.7

Installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat ships the logs, including application, service, system and event logs. For example, syslog files, showing general information about the activity on the system, and auth.log files, that detail both failed and successful logins or authentications. 
- Metricbeat records the metrics of the machine, like CPU and memory usage. For example, each machine ships CPU Usage, Network IO, and Memory Usage information.
  
---------------------------------

## Using the Playbooks
---------------------------------

### Set up -
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook files for DVWA, ELK, Filebeat and Metricbeat to `/etc/ansible/roles`
- Update the `/etc/ansible/hosts` file to create groups to specify the DVWA machines and the ELK machine. Also include the line for using python3.

![screenshot of hosts file](https://github.com/Sheryl101/CybersecurityKB/blob/main/Images/hosts.png)

### DVWA -
Run the DVWA playbook.
- `ansible-playbook install-DVWA.yml`
- SSH into one of the DVWA machines and use curl to verify it was set up successfully and running. 
- `curl localhost/setup.php`
- Navigate to the public IP of the Load Balancer from your workstation to confirm it was successful, and can be accessed from a browser.   
   Ex: `http:/52.148.177.153//setup.php`

### ELK -
Run the ELK playbook.
- `ansible-playbook install-elk.yml`
- Navigate to the public IP of the ELK machine on port 5601 to verify connection to the Kibana app.   
  Ex: `http://http://52.184.167.70:5601/app/kibana` 

### Filebeat -
To use the Filebeats playbook, the `filebeat-config.yml` file needs to be configured and saved to `/etc/ansible/roles/files/`



- Set "Elasticsearch output" hosts IP to ELK machine IP / port 9200.
![screenshot of filebeat-config](https://github.com/Sheryl101/CybersecurityKB/blob/main/Images/filebeat-config1.png)
- Set  "Kibana" host IP to ELK machine IP / port 5601.
![screenshot of filebeat-config](https://github.com/Sheryl101/CybersecurityKB/blob/main/Images/filebeat-config0.png)

Run the Filebeat playbook.
- `ansible-playbook filebeat-playbook.yml`
- Navigate to the public IP of the ELK machine on port 5601 to verify connection to the Kibana app. Select add log data, system logs, and check data to verify it is receiving data.   
  Ex: `http://52.184.167.70:5601/app/kibana` 

### Metricbeat -
To use the Metricbeats playbook, the `metricbeat-config.yml` file needs to be configured and saved to `/etc/ansible/roles/files/`

- Set "Kibana" host IP to ELK machine IP / port 9200.
![screenshot of metricbeat-config](https://github.com/Sheryl101/CybersecurityKB/blob/b05192f788bcc7a5f4471294b989fa1ca5727a18/Images/metricbeat-config0.png)
- Set "Elasticsearch output" hosts IP to ELK machine IP / port 5610. 
![screenshot of metricbeat-config](https://github.com/Sheryl101/CybersecurityKB/blob/b05192f788bcc7a5f4471294b989fa1ca5727a18/Images/metricbeat-config1.png)

Run the Metricbeat playbook.
- `ansible-playbook metricbeat-playbook.yml`
- Navigate to the public IP of the ELK machine on port 5601 to verify connection to the Kibana app. Select add metrics, system metrics, and check data to verify it is receiving data.   
  Ex: `http://52.184.167.70:5601/app/kibana` 
  
[Detail Set-Up for Filebeat & Metricbeat](https://github.com/Sheryl101/CybersecurityKB/blob/3ec7be6f0b7af14f05eb5fba3fca7cb09777bafa/Filebeat_Metricbeat%20Container%20Set-up/Filebeat_Metricbeat%20Set-Up.pdf)
