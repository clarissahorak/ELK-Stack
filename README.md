## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/clarissahorak/ELK-Stack/blob/main/Images/RedTeam2%20%26%20Elk%20Stack%20Network%20Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

![alt text](https://github.com/clarissahorak/ELK-Stack/blob/main/Images/filebeat-playbook.yml.txt)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- What aspect of security do load balancers protect? What is the advantage of a jump box?
	Load balancers protect the availablity of servers by evenly ditributing traffic across the multiplte servers that are grouped together in the load balancer's backend pool.
        Advantages to having a jump box virtual machine includes being able update and configure all machines on a server from one centralized location and having one access point to the virtual network all while cutting points of unauthorized access. 
	
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- What does Filebeat watch for? 
	Filebeat watches and collects the log events from log files on the running operating system on the connected server. Filebeat creates an index of the log events for easy tracking in case of security events.
- What does Metricbeat record? 
	Metricbeat records the analytics of the running operating system on the connected server such as performance data, and statistical information.

The configuration details of each machine may be found below.

| Name                 |    Function    | IP Address |          OS          |
|----------------------|:--------------:|------------|:--------------------:|
| Jump-Box-Provisioner |     Gateway    |  10.0.0.4  | Linux (ubuntu 18.04) |
| Web-1                |   Web Server   |  10.0.0.5  | Linux (ubuntu 18.04) |
| Web-2                |   Web Server   |  10.0.0.6  | Linux (ubuntu 18.04) |
| Web-3                |   Web Server   |  10.0.0.8  | Linux (ubuntu 18.04) |
| ElkVM                | Log Management |  10.1.0.4  | Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Local Host IP address: 76.xxx.xxx.xxx/32 

Machines within the network can only be accessed by SSH.
- Which machine did you allow to access your ELK VM? What was its IP address?_
		Jump-Box_Provisioner - 52.147.214.175

A summary of the access policies in place can be found in the table below.

| Name    | Publicly Accessible | Allowed IP Addresses     |
|---------|---------------------|--------------------------|
| Jumpbox | Yes                 | Local Host IP            |
| Web-1   | No                  | 10.0.0.4		   |
| Web-2   | No                  | 10.0.0.4 		   |
| Web-3   | No                  | 10.0.0.4                 |
| Elk     | No                  | 10.0.0.4                 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because automating configuration with Ansible allows for easy management and installation for applications that are uniform across various machines. 

The playbook implements the following tasks:
- Install docker.io 
- install python3 & python module
- Configure docker python to increase memory 
- Download elk image 
- Configure ports and launch container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/clarissahorak/ELK-Stack/blob/main/Images/Docker%20ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 10.0.0.5
web-2 10.0.0.6

We have installed the following Beats on these machines:
	Filebeat
	Metricbeat

These Beats allow us to collect the following information from each machine:
	-FileBeat collects log events and data and will show events that occur--such as successful and failed ssh attempts.
	-MetricBeat collects metric data of the os such as cpu usage, memory usage,etc

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the source file (.yml) to destination directory.
- Update the configuration file to include groups of servers (webservers & elk in this example) & corressponding private IP addresses.
- Run the playbook, and navigate to <sudo docker ps> to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it? 
	Ansible playbook.yml Playbooks are installation scripts (filebeat & metricbeat).
	They are copyied from the ansible containers to the target webVMs (web-1 & web-2 & elkvm).
- _Which file do you update to make Ansible run the playbook on a specific machine? 
- _How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
	The configuration YAML needs updated before running the Ansible playbook.
	The ELK machine can be specified by adding the ELK grouping and specifying the private IP address of the ELK server.  
- _Which URL do you navigate to in order to check that the ELK server is running? 
	https://[IPELKVM]:5601/app/kibana  
	If this website loads, then the ELK serve is running correctly. 
