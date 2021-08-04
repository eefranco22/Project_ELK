## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Project_ELK](https://user-images.githubusercontent.com/79772167/128137036-632ab1e5-db6d-4738-8523-3dfd27cb6e05.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the Project_ELK files may be used to install only certain pieces of it, such as Filebeat.

  - elk-playbook.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml
  - metricbeat-config.yml
  - filebeat-config.yml
  - ansible.cfg

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly reliable and available, in addition to restricting access to the network. Subsequently, it's a great defense against distributed denial-of-service (DDoS) attacks as its main responsibility is to redistribute traffic across multiple servers within its "pool" and preventing any server from being overloaded. 

In this network, the servers staged behind the load balancer are managed by a jump box virtual machine which acts as the sole gateway into either virtual network. A single entry point into the network is much easier to monitor and safeguard, plus it keeps the user separate from the network. Network security improves substantially.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs. 

- Filebeat is a shipper that can be installed on servers to collect and organize log data from their file systems, allowing you to monitor any changes to data and when they happen. 

- Metricbeat is a shipper that can be installed monitor servers by collecting metrics and statistics from the operating system and services running on the servers. 

The configuration details of each machine may be found below.

| Name         | Function     | IP Address | Operating System |
|--------------|--------------|------------|------------------|
| Jump Box     | Gateway      | 10.0.0.4   | Linux            |
| Web-1        | Ubuntu Server| 10.0.0.5   | Linux            |
| Web-2        | Ubuntu Server| 10.0.0.6   | Linux            |
| Web-3        | Ubuntu Server| 10.0.0.7   | Linux            |
| ELK          | Ubuntu Server| 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My IP address (54.245.193.207)

Machines within the network can only be accessed by Jump Box. ELK can be accessed from My IP. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses   |
|----------|---------------------|------------------------|
| Jump Box | Yes                 | 54.245.193.207 (My IP) |
| Web-1    | No                  | 10.0.0.4 (Jump Box)|
| Web-2    | No                  | 10.0.0.4 (Jump Box)|
| Web-3    | No                  | 10.0.0.4 (Jump Box)|
| ELK      | Yes                 | 54.245.193.207 (My IP) |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because configuration can easily be replicated if more machines are added. Also, any necessary updates can be implemented across multiple machines from one file. 

The playbook implements the following tasks:
- Install docker.io
- Install python-3
- Install python docker module
- Change vm memory
- Install ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="657" alt="Screen Shot 2021-08-03 at 9 52 50 PM" src="https://user-images.githubusercontent.com/79772167/128137123-b8747ff9-62a6-40c1-8ac7-a297a649cf6c.png">

### Target Machines & Beats
This ELK server is configured to monitor the following machines: Web-1: 10.0.0.5, Web-2: 10.0.0.6, Web-3: 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat collects logs indicating any changes to the OS and when they occurred. For example, you can monitor for network interruptions or transmissions. 

- Metricbeat collects metrics and statistics from the OS. For example, you could monitor for server performance metrics and memory metrics. 

### Using the Filebeat Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files.
- Update the /etc/ansible/host file to include the private IP addresses of each DVWA container
- Run the playbook, and navigate to http://13.89.240.21:5601/app/kibana to check that the installation worked as expected.

<img width="1425" alt="Screen Shot 2021-08-04 at 12 42 43 AM" src="https://user-images.githubusercontent.com/79772167/128136961-5e8c0f44-1e8d-4505-8038-8b4a37943d66.png">
<img width="1432" alt="Screen Shot 2021-08-04 at 12 43 59 AM" src="https://user-images.githubusercontent.com/79772167/128136978-be55e53a-d2b1-4069-9e68-f9a7a942b027.png">
<img width="1440" alt="Screen Shot 2021-08-04 at 12 48 07 AM" src="https://user-images.githubusercontent.com/79772167/128136997-3258b954-5430-4ae2-bf82-1c50d944baea.png">

