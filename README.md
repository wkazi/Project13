## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](https://user-images.githubusercontent.com/86036665/143174845-1a8bd163-b253-464d-8c35-84abd9657328.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

  Project13/Ansible

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available for clients, in addition to restricting inbound access to the network.

* What aspect of security do load balancers protect? 
o It protects the system from DDoS attacks by shifting attack traffic
o Availability which is part of CIA, load balancers protects, ensure application’s availability when needed, and allowing requests to be shared across a number of servers 

* What is the advantage of a jump box?
o Only Jump box can access the Virtual network via ssh 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network files and system logs and system metrics.

What does Filebeat watch for? 
For log files/locations, collect log events and forwards them to   Elasticsearch or Logstash for indexing

What does Metricbeat record?
Records metrics and statistical data from the operating system and from services running on the server

The configuration details of each machine may be found below.

| Name      | Function               | IP Address | Operating System         |
|-----------|------------------------|------------|--------------------------|
| Jump Box  | Gateway                | 10.0.0.4   | Linux (Ubuntu 18.04 LTS) |
| Web-1     | DVWA                   | 10.0.0.5   | Linux (Ubuntu 18.04 LTS) |
| Web-2     | DVWA                   | 10.0.0.6   | Linux (Ubuntu 18.04 LTS) |
| Web-3     | DVWA                   | 10.0.0.7   | Linux (Ubuntu 18.04 LTS) |
| ELKServer | Monitoring "ELK Stack" | 10.1.0.4   | Linux (Ubuntu 18.04 LTS) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
IP address from my local machine

Machines within the network can only be accessed by SSH.

Which machine did you allow to access your ELK VM? JumpBox Provisioner What was its IP address? 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP addresses       | Allowed Ports |
|-----------|---------------------|----------------------------|---------------|
| Jump Box  | Yes (SSH)           | IP from my local machine   | 22            |
| Web-1     | Yes (HTTP)          | 10.0.0.1-254               | 80            |
| Web-2     | Yes (HTTP)          | 10.0.0.1-254               | 80            |
| Web-3     | Yes (HTTP)          | 10.0.0.1-254               | 80            |
| ELKServer | Yes (HTTP, SSH)     | 10.0.0.1-254, SSH 10.0.0.4 | 5601   


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

What is the main advantage of automating configuration with Ansible?
* Build and deployment is performed automatically. No configuration was performed manually because everything can be done from single container in the Jump box Provisioner quickly. In addition to that playbooks allow to configure multiple virtual machines via a single command script avoiding errors.

The playbook implements the following tasks:
* Installs docker.io
* Installs python-pip
* Installs the docker module using pip
* Increase the virtual memory of ELKServer
* Downloads and launched the sebp/elk container over ports 5601,9200,5044



The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![dockerps](https://user-images.githubusercontent.com/86036665/143174914-a8802de0-f18f-4b2a-840e-ccda64af4763.png)

Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)



### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring_
Web-1 10.0.0.5
Web-2 10.0.0.6
Web-3 10.0.0.7

We have installed the following Beats on these machines:
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat: Collects logs events and watches for log files and locations which can be used to track any logs we want. Example: Lightweight Log Analysis $ Elasticsearch.

Metricbeat: Records metrics and statistical data from services running on the server and the operating system. Example: Lightweight Shipper for Metrics). 


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/
- Update the /etc/ansible/hotst to include ELKServer and the other webservers
- Run the playbook, and navigate to http://40.118.186.99:5601/app/kibana to check that the installation worked as expected.

_ Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Install-elk.yml Where do you copy it? /etct/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine? 
/etc/ansible/hosts
How do I specify which machine to install the ELK server on versus which to install Filebeat on? 
Specify the machine to install the ELK server in /etc/ansible/hosts 

- _Which URL do you navigate to in order to check that the ELK server is running?
http://40.118.186.99:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

* ssh RedAdmin@JumpBox  “ssh Redadmin@20.106.165.246 
* docker start vigorous_chaplygin   (starts and ansible container)
* docker attach vigorous_chaplygin  (connect to the ansible container via ssh@ipddress)
* cd /etc/ansible/  
* ansible-playbook pentest.yml
k, update the files, etc._
