# GT-Edu-project
ELK-Stack in Azure

# Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.

![](https://user-images.githubusercontent.com/71580112/109997994-cbe07180-7cde-11eb-939d-1aced4b58d3d.png)




This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to build and use ansible to automate and deploy on docker containers and monitor those web servers.


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly avalable, in addition to restricting access to the network.
The load balancer ensures that the work to process incoming traffic will be shared across all three vulnerable web servers.  Access controls will ensure that only autherized users can connect to the inter virtual network 

Integrating an ELK server allows Admin to easily monitor the vulnerable VMs for system traffic, logs, metrics and system changes.
    -Filebeat watches for log files/locations and collect log events. (Filebeat: Lightweight Log Analysis & Elasticsearch)
    
    -Metricbeat records metrics and statistical data from the operating system and from services running on the server (Metricbeat: Lightweight Shipper for Metrics)

The configuration details of each machine may be found below.


| Name          | Function            | Public IP Address | Private IP Address | Operating system | 
|---------------|---------------------|-------------------|--------------------|------------------|
| Jump Box      | Gateway w/ Ansible  | 52.146.87.161     | 10.0.0.4           | Linux ubuntu     |
| Web 1         | Docker w/ DVWA      | No Public IP      | 10.0.0.10          | Linux ubuntu     |
| Web 2         | Docker w/ DVWA      | No Public IP      | 10.0.0.11          | Linux ubuntu     |
| Web 3         | Docker w/ DVWA      | No Public IP      | 10.0.0.12          | Linux ubuntu     |
| ELK Server    | Docker w/ ELK Stack | 168.61.178.12     | 10.2.0.4           | Linux ubuntu     |
| Load Balancer | Load Balancing      | 52.224.192.76     | No Private IP      |                  |

A load balancer with a health probe has been provisioned in front of the 3 DVWA web server VM's.
Avalibility zone 1: JumpBox, Load Balancer, DVWA Web server 1-3
Avalibility zone 2: ELK Server




### Access Policies

A summary of the access policies in place can be found below

ACL's (access control lists) were set up to allow only inbound connections from white listed Ip Addresses to the Jump Box VM which can then communicate with all other servers through the ansible container over SSH port 22 utilizing SSH public keys for security. 

| VM Name       | Public Access | Public Port | Private IP Access | Private Port |
|---------------|---------------|-------------|-------------------|--------------|
| Jump Box      | 52.146.87.161 | 22          | 10.0.0.4          | 22           |
| Load Balancer | 52.224.192.76 |             |                   |              |
| DVWA Web1     | 52.224.192.76 | 80          | 10.0.0.10         | 22           |
| DVWA Web2     | 52.224.192.76 | 80          | 10.0.0.11         | 22           |
| DVWA Web3     | 52.224.192.76 | 80          | 10.0.0.12         | 22           |
| ELK Server    | 168.61.178.12 | 5601        | 10.2.0.1          | 22           |

The web servers can accept HTTP traffic through the load balancer but have no public facing IP Address. The Elk Server could be accessed over HTTP port 5601 to examine the monitored data.


## ELK Server Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, The advantage of automating the installation process is that multiple server deployments can be accomplished easily and quickly without having to physically touch each server.

The ELK VM exposes an Elastic Stack instance. **Docker** is used to download and manage an ELK container.

Rather than configure ELK manually, we opted to develop a reusable Ansible Playbook to accomplish the task.

![](install-elk.yml)
![](https://github.com/Viewaskew/GT-Edu-project/blob/09e6940ec84b983e3836a34254a4dde545123fc1/install-elk.yml)

The playbook implements the following tasks:

Install Docker.io and pip3
Increases VM memory
Download and Configure elk docker container
Sets Published Ports
  
