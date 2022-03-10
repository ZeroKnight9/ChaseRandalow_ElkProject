ChaseRandalow_ElkProject
## Automated ELK Stack Deployment – Chase Randalow

The files in this repository were used to configure the network depicted below.
  - /ChaseRandalow_ElkProject/Diagrams/ElkStackDiagram

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook file may be used to install only certain pieces of it, such as Filebeat.
  - /ChaseRandalow_ElkProject/Ansible/filebeat-playbook.yml
  - /ChaseRandalow_ElkProject/Ansible/filebeat-config.yml

This document contains the following details:
  - Description of the Topology
  - Access Policies
  - ELK Configuration
  - Beats in Use
  - Machines Being Monitored
  - How to Use the Ansible Build



### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly efficient, in addition to restricting traffic to the network. Load balancers protect against Distributed Denial of Service attacks (DDoS) by switching where the attacking traffic goes. Instead of the attacking traffic hitting the private server, it is instead redirected to a public cloud, thus preventing the attack. A Jumpbox is an easy to use, inexpensive function that allows the user to access other devices on the network from a single node.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system statistics and metrics.
- Filebeat watches for any potential alterations made to data and when those alterations may have been made.
- Metricbeat monitors your servers to record the metrics and statistics of the systems, then pushes them to an output location.
The configuration details of each machine may be found below.
| Name                 | Function   | IP Address | Operating System |
|----------------------|------------|------------|------------------|
| Jump_Box_Provisioner | Gateway    | 10.0.0.4   | Linux            |
| Web1                 | Web Server | 10.0.0.5   | Linux            |
| Web2                 | Web Server | 10.0.0.6   | Linux            |
| Web3                 | Web Server | 10.0.0.7   | Linux            |
| Elk                  | Elk Server | 10.1.0.4   | Linux            |


### Access Policies
The machines on the internal network are not exposed to the public Internet. 
Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
  - Home computer public IP address
Machines within the network can only be accessed by home computer and Jumpbox.
  - Jump_Box_Provisioner VM. IP address was 10.0.0.4 via SSH port 22.
  - Home computer using home computer public IP address.
A summary of the access policies in place can be found in the table below.
| Name                 | Publicly Accessible | Allowed IP Address        |
|----------------------|---------------------|---------------------------|
| Jump_Box_Provisioner | Yes                 | Home IP address           |
| Web1                 | No                  | 10.0.0.5                  |
| Web2                 | No                  | 10.0.0.6                  |
| Web3                 | No                  | 10.0.0.7                  |
| Elk                  | No                  | Home IP address, 10.1.0.4 |



### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
A single Playbook can store multiple commands at once.
The playbook implements the following tasks:
  - Install docker.io
  - Install Python pip3
  - Install docker python module
  - Run command: sysctl -w vm.max_map_count=262144
  - Download and launch the docker containing Elk
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
  -/ChaseRandalow_ElkProject/README/Images/docker_ps_output.png



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
  - Web1: 10.0.0.5
  - Web2: 10.0.0.6
  - Web3: 10.0.0.7
We have installed the following Beats on these machines:
  - MetricBeat
  - FileBeat
These Beats allow us to collect the following information from each machine:
  - Filebeat collects changes made to the system and sends these logs to kibana.
  - MetricBeat collects system metrics and statistics and sends these logs to kibana.



### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
  - Copy the Playbook file to /etc/ansible.
  - Update the host file to include...
  - Run the playbook and navigate to command line to check that the installation worked as expected.

- Which file is the playbook? Where do you copy it? 
       filebeat-playbook.yml, /etc/ansible/roles
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
	/etc/ansible/hosts. 
       The webservers group is given Filebeat while the elkservers group is given Elk.
- Which URL do you navigate to in order to check that the ELK server is running?
	http://20.120.33.169:5601/app/kibana
