## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img src="/Diagrams/Diagram.png">

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml files may be used to install only certain pieces of it, such as Filebeat.

  [Ansible Files](Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unwanted access to the network.
The main use of the load balancer in this case would be to divert requests to the appropriate web server which can provide stability and reliability when trying to access the DVWA servers. The Jumpbox is used as an access point which is controlled/run on my own home network which allows remote access to DVWA and Elk servers ONLY from my IP.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
-Filebeat is used to monitor Log Files 
-Metricbeat is used to monitor Server Metrics 

The configuration details of each machine may be found below.

| Name      | Function  | IP Address | Operating System |
|-----------|-----------|------------|------------------|
| Jump Box  | Gateway   | 10.0.0.4   | Linux            |
| DVWA 1    | Web Server| 10.0.0.5   | Linux            |
| DVWA 2    | Web Server| 10.0.0.6   | Linux            |
| DVWA 3    | Web Server| 10.0.0.7   | Linux            |
| ELK server| Elk Stack | 10.1.0.4   | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the my home network based on security rules I put in place.

Machines within the Web server’s network can only be accessed by SSH via port 22 from the Jumpbox Machine IP.
The ELK server is only allowed to be accessed by my home network which allows for access via port 5601(kibana) or internally via ssh from the Jumpbox only because I peered the two networks to communicate with each other.

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump Box  | Yes Via port 22     | My Home Network      |
| DVWA 1    | NO                  | 10.0.0.4             |
| DVWA 2    | NO                  | 10.0.0.4             |
| DVWA 3    | NO                  | 10.0.0.4             |
| ELK Server| YES Via port 22/5601| 10.0.0.4/Home Network|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because this allows for minimal chance of errors while applying changes/updates to all servers.

The playbook implements the following tasks:
- Install Docker.io
- Install pip3 (allows for software packages to be downloaded in python 3)
- Install Docker python Module
- Increase the amount of memory used (which is needed to run ELK Stack)
- Download and launch ELK Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img src="/README/Images/Elk.png">

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- DVWA 1 (10.0.0.5)
- DVWA 2 (10.0.0.6)
- DVWA 3 (10.0.0.7)

We have installed the following Beats on these machines:
- Filebeat
- MetricBeat

These Beats allow us to collect the following information from each machine:
- Metricbeat is used to log system metrics and process information such as CPU Usage, Inbound/Outbound Traffic, and Memory Usage.
- Filebeat is used to logs changes within files on the system along with forwarding that information which will then be parsed to allow for visualization of the data being changed.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk.yml file to /etc/ansible directory.
- Update the hosts file to include the internal IP address of the servers you want to have ELK added to.
- Run the playbook and navigate to Kibana to check that the installation worked as expected.

