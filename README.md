# Cybersecurity-Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/Azure_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

- name: install filebeat deb
    command: dpkg -i filebeat-7.4.0-amd64.deb

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system statistics.

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.4   | Linux            |
| DVWA-VM1 | VM       | 10.1.0.5   | Linux            |
| DVWA-VM2 | VM       | 10.1.0.6   | Linux            |
| ELK-VM   | ELK      | 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the 10.1.0.4 machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

Machines within the network can only be accessed by 10.1.0.4.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Any/My IP Address    |
| DVWA-VM1 | No                  | 10.1.0.4             |
| DVWA-VM2 | No                  | 10.1.0.4             |
| ELK-VM   | No                  | 10.1.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because ansible is able to configure each VM identically in a short period of time. 

The playbook implements the following tasks:
- Install Docker
- Install Python
- Install Docker Module
- Increase Memory
- Download and Launch ELK Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.1.0.5
- 10.1.0.6

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- 'Filebeats' collects logs, which it fowards to Elasticsearch for anaylzing.
- 'Metricbeats' collects metrics from the system, which we use to ensure the system is running smoothly.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ./filebeat.yml file to /etc/filebeat/.
- Update the hosts file to include the webserver host group with the specified ELK virtual machine IP address.
- Run the playbook, and navigate to http://10.2.0.4:5601 to check that the installation worked as expected.
