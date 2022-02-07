# ELK-Stack-Deployment
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

In this project we deployed an Elasticsearch, Logstash, and Kibana stack (ELK). The ELK stack can be deployed simply by an ssh from your host.

Here is the YAML file that I used:

---
- name: Configure Elk VM with Docker
  hosts: ELK
  remote_user: sysadmin
  become: true
  tasks:
    - name: Install docker.io
      apt:
        update_cache: yes
        name: docker.io
        state: present

    - name: Install pip3
      apt:
        force_apt_get: yes
        name: python3-pip
        state: present

    - name: Install Docker python module
      pip:
        name: docker
        state: present

    - name: Use more memory
      sysctl:
        name: vm.max_map_count
        value: "262144"
        state: present
        reload: yes

    - name: download and launch a docker elk container
      docker_container:
        name: elk
        image: sebp/elk:761
        state: started
        restart_policy: always
        published_ports:
          - 5601:5601
          - 9200:9200
          - 5044:5044
          - 
![TODO: Update the path (name of picture) with the name of your diagram](Images/diagram_filename.png)
https://docs.google.com/document/d/1VUHMzr6ZSPFB63T2d3uNQfJRMM_vGSbUvOs9nKNB-v4/edit
These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._ (gallant_hofstadter)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _stable____, in addition to restricting _____ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load balancers protect the system from attacks by shifting attack traffic, and the jump box provides access from one point in the system.
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_ FIlebeat watches for information that changes
- _TODO: What does Metricbeat record?_ Metricbeat collects stats and sends them to a specific output.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name        | Function   | IP Address | Operating System |
|-------------|------------|------------|------------------|
| Jump-Box    | Gateway    | 10.0.2.4   | Linux            |
| VM2 (Web-1) | Web Server | 10.0.2.5   | Linux            |
| VM3 (Web-2) | Web Server | 10.0.2.6   | Linux            |
| ELK stack   | Web Server | 10.2.0.4   | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __Jump-Box(gateway)___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Home IP address to personal machine
- 

Machines within the network can only be accessed by __Jump-Box___.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
Jump-Box 10.0.2.4
A summary of the access policies in place can be found in the table below.

| name        | publicly accessible? | Allowed IP addresses |
|-------------|----------------------|----------------------|
| Jump Box    | Yes                  | Home IP              |
| VM2 (Web-1) | NO                   | 10.0.2.4             |
| VM3 (web-2) | No                   | 10.0.2.4             |
| ELK stack   | No                   | 10.0.2.4             |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
The Advantage is you can use a single playbook to to configure multiple servers.
The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install docker.io
- Install python-pip
- INstall docker
- sysctl -w vm.max_map_count=262144
- Launch ELK

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
VM2 (web-1) 10.0.2.5
VM3 (web-2) 10.0.2.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
Filebeat and metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
Filebeat collects changes to files. Metricbeat collect metrics and statistics like uptime.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_/etc/ansible/file/filebeat-configuration.yml
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
edit the /etc/ansible/host file to add the ip addresses of webservers or elkservers
- _Which URL do you navigate to in order to check that the ELK server is running? publicip

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._ ansible-playbook filebeat-playbook.yml
Here is a link to my network diagram https://docs.google.com/document/d/1VUHMzr6ZSPFB63T2d3uNQfJRMM_vGSbUvOs9nKNB-v4/edit
