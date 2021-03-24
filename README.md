# Project-1

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img width="772" alt="Screen Shot 2021-03-24 at 6 03 33 AM" src="https://user-images.githubusercontent.com/73920494/112308006-401b8e80-8c67-11eb-9123-b8cdd3bf8572.png">


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the playbook may be used to install only certain pieces of it, such as Filebeat. 

  - ELK-install.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting overload to the network.
- Load Balancers protect the availability of an application by defending against DDoS attacks.
- Jumpboxes are a secure way to access network VMs without exposing the VMs to high-risk activity (i.e. email, internet browsing, etc). Jumpboxes are used for administrative reasons only, limiting the risk to hackers. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors log files and collects log events, forwarding them to Elasticsearch or Logstash for indexing. 
- Metricbeat collects metrics from services running on the server and sends them to Elasticsearch or Logstash for storage.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| ELK-VM   |LogMonitor| 10.1.0.4   | Linux            |
| Web-1    |Webservers| 10.0.0.6   | Linux            |
| Web-2    |Webservers| 10.0.0.7   | Linux            |
| Web-3    |Webservers| 10.0.0.8   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 69.21.193.0/24

Machines within the network can only be accessed by SSH.
- Only the workstation can access the ELK-VM and Jump Box, using IP address: 69.21.193.0/24
- Webservers can be accessed from the Jump Box internal IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 69.21.193.0/24       |
|  ELK-VM  | No                  | 69.21.193.0/24       |
|Webservers| No                  | 10.0.0.4, 10.1.0.4   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- it allows IT administrators to focus on more valuable tasks than performing mundane daily tasks, such as machine configurations. 

The playbook implements the following tasks:
- Installs Docker 
- Installs and runs python3
- Downloads and automatically launches the Docker ELK container
- Enables Docker to run automatically, even after a reboot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="572" alt="docker_ps" src="https://user-images.githubusercontent.com/73920494/112308385-b0c2ab00-8c67-11eb-9881-4ef46824eb32.png">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.6
- 10.0.0.7
- 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat (filebeat-7.4.0-amd64.deb)
- Metricbeat (metricbeat-7.4.0-amd64.deb)

These Beats allow us to collect the following information from each machine:
- Filebeat collects log files and log events, which can be used to view access logs from users, or error logs from applications on the server.
- Metricbeat collects metrics from services running on the server, and can be used to monitor and/or analyze the memory being used by an application, or analyzing system CPU. 

### Using the ELK-install Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ELK-install.yml file to /etc/ansible/roles.
- Update the hosts file in Ansible to include the group [elk] with the internal IP of your ELK-VM: [internal_ip] ansible_python_interpreter=/usr/bin/python3
- Run the playbook <ansible-playbook ELK-install.yml>, and navigate to http://[your.ELK-VM.Public.IP]:5601/app/kibana to check that the installation worked as expected.

To install Filebeat and Metricbeat, follow the steps below:
- Copy filebeat-configuration.yml and metricbeat-configuration.yml to /etc/ansible/files.
- Update the configuration files to include the ELK-VMs internal IP. 
- Copy the filebeat-playbook.yml and the metricbeat-playbook.yml to /etc/ansible/roles.

