# CyberClass
Displaying ELK Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

See "Azure Diagram.png"

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._ -> See "ElkServerPlaybook.png"

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly ___flexible__, in addition to restricting ___DDOS__ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load balancers are important because they protect servers from being overwhelmed by incoming traffic. Load balancers act by diverting traffic to servers that can handle
the increased workload. If a server becomes overtaxed then the system would fail and the end users will not be able to perform their day to day functions. A Jump box
is important because it is a single Virtual Machine that can control multiple VMs and containers. In order to get to other VMs or containers the must first connect
to the Jump Box. This ensures that no unauthorized individuals can get to the valuable information past the Jump Box. It acts as a filtration method to keep 
unauthorized users away from valuable information.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the __files___ and system __logs___.
- _TODO: What does Filebeat watch for?_ Filebeat is used to collect data about the files within a system or VM
- _TODO: What does Metricbeat record?_ Metricbreat records system metrics that tell how well the machine is functioning. Metric beat monitors uptime and sends error
events when an issue arises in the system. 


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.5   | Linux            |
| DVWA1    | Docker   | 10.0.0.7   | Linux            |
| DVWA2    | Docker   | 10.0.0.9   | Linux            |
| Elk      | Logging  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __Elk___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 
- _TODO: Add whitelisted IP addresses_ 40.78.3.181 and 40.78.90.22

Machines within the network can only be accessed by _the Jump Box VM____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_ JumpBox: 10.0.0.5 (Public: 13.91.123.16)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |     Yes             | 68.132.41.215        |
| DVWA1    |     No              | 68.132.41.215        |
| DVWA2    |     No              | 68.132.41.215        |
| Elk      |     Yes             | 68.132.41.215        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
The big advantage of configurating through automation is the VMs can be removed and re-created very quickly. In order to keep the system secure and decrease costs a 
system engineer will want to take advantage of automations to take down and spin up VMs, containers, etc. on a daily basis.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ... To install ELK, a yaml file is created and designed to automate the installation. First the hostd are defined which are the virtual machines that will be 
updated with the information to follow. The name below the heading will designate what will be installed when the file is run. Next the file is defined, in this case
it is "docker.io" which will automatically download Docker when the file is run. Additionally, a container is set to be installed and launched within Docker.
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

See "Docker PS.png"

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
Monitoring machines with IP addresses 40.78.3.181 and 40.78.90.22

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
Filebeat and Metricbeat was installed on DVWA1, DVWA2, and ELK VMs

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects log information about the system and aggregates it into aesthically pleasing format
Metricbeat collects the machines metrics on how well the machine is functioning. It can be formatted to provide information on various types of errors.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
The file is ansibleplaybook.yml. I copied it to the DVWA1 and DVWA2 VMs to then run the ansible playbook on them
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
You update the "hosts" file and set the network IPs to the VM's you want the ansible playbook to run on. You specify the group of VMs you want to install the payload 
on by updating the "hosts" file with the appropriate IPs under the right group. For example, the DVWA1 and DVWA2 VMs were under the "webservers" group. When writing
the playbook you specify the "webservers" group so when the file is run it will know to look at the IPs in the "webservers" group.
- _Which URL do you navigate to in order to check that the ELK server is running?
Input the public IP of your Elk VM into the URL to check if it is running correctly. Since we opened the port from the Internet, we should be able to connect over the
internet to the ELK VM.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
"ansible-playbook" will run the playbook. For instance you'd type "ansible-playbook filebeat-playbook.yml" to run the filebeat-playbook.yml file.
