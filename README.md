
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

**Note**: The following image link needs to be updated. Replace `diagram_filename.png` with the name of your diagram image file.  

https://drive.google.com/file/d/1SmpoGfhIQ2ADszpHC9JXlXTDJvU4vOMO/view?usp=sharing

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML Playbook and config_ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive and available, in addition to restricting traffic to the network.

- What aspect of security do load balancers protect? 
Load balancers protect website security and web traffic from DDos attacks  

What is the advantage of a jump box?_
A Jumpbox allows for customized security configurations, Logical access control and 
Network division, which adds an extra layer of security.



Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the  data and system performance.

- What does Filebeat watch for?
   Filebeat reads log files and sends event logs that have been changed to specified location.
 
- What does Metricbeat record?
Metricbeat records metrics and statistics that it collects from the operating system and other services running on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name       | Function      |                  IP Address         | Operating System |
|---------------|-----------------|-------------------------------------|---------|
| Jump Box |   Gateway   |  10.0.0.4   /   40.87.108.33  | Linux |
| Web-1      | Web server |  10.0.0.6                              | Linux |
| Web2       | Web server |  10.0.0.7                              | Linux |
| Web-3      | Webserver  |  10.0.0.5                              | Linux |
|ELK vm.    |  ELK server |  10.1.0.4   /   52.151.4.184  |  Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-Add whitelisted IP addresses
Workstation public IP.

Machines within the network can only be accessed by the Jumpbox.
-  Which machine did you allow to access your ELK VM? What was its IP address?_
   Jumpbox is the only machine that has allowed access to the ELK machine.
	IP:10.0.0.4
A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|---------------|---------------------------|----------------------|
| Jump Box |            Yes              | 10.0.0.4             |
|  Web-1     |             No               | 10.0.0.6             |
|  Web-2     |             No               | 10.0.0.7             |
|  Web-3     |             No               |  10.0.0.5            |
|  ELK server|           No               |  10.1.0.4	         | 

### Elk Configuration

Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible?_
 Ansible allows using one machine to configure multiple machines therefore speeding the automation process.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
Set remote_user
Install docker.io, python3 and docker module
Increase system memory.
Download the container to Elk server.
Open ports 5601:5601, 9200:9200, 5044:5044
Check kibana is up and ready.
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

**Note**: The following image link needs to be updated. Replace `docker_ps_output.png` with the name of your screenshot image file.  


![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:
- Web-1 / 10.0.0.6 
  Web-2 /10.0.0.7

We have installed the following Beats on these machines:
- Filebeat and metricbeat have been installed  on Web-1 and Web-2 VMs

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeats collects system logs and will send changed logs to either Elastic search or  Logstash.
Metricbeats monitors performance.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat cfg file to _____.
- Update the __fiilebeat___ file to include...
- Run the playbook, and navigate to Kibana Website>add log data>>system logs to check that the installation worked as expected.

  Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it? /etc/ansible/
- Which file do you update to make Ansible run the playbook on a specific machine? 
   Host file
-How do I specify which machine to install the ELK server on versus which to install Filebeat on? IP of the machines you want to filebeat_cfg and metricbeat_cfg 
- _Which URL do you navigate to in order to check that the ELK server is running?
http://52.151.4.184:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
Download Filebeat config file and copy to filebeat-config.yml
curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-darwin-x86_64.tar.gz
tar xzvf filebeat-7.6.1-darwin-x86_64.tar.gz
cd filebeat-7.6.1-darwin-x86_64/> filebeat-config.yml
Update filebeat congif.yml file
Nano filebeat-config.yml
Ctrl w to specify line 
Once playbook completed run playbook:
Ansible-playbook /etc/ansible/roles/filebeat-playbook.yml
If no errors, verify installation worked on Kibana website:
kibana>add log data>system logs>check data



