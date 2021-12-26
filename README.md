## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(Images/Network_Azure_ELK_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the install-elk.yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition the jump box restricts access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the system logs and metrics.

The configuration details of each machine may be found below.

| Name               | Function   | IP Address | Operating System |
|--------------------|------------|------------|------------------|
| JumpBoxProvisioner | Gateway    | 10.1.0.4   | Linux            |
| Web-1              | Host       | 10.1.0.8   | Linux            |
| Web-2              | Host       | 10.1.0.9   | Linux            |
| ELK                | Monitoring | 10.3.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 24.179.132.82

Machines within the network can only be accessed by the Jump Box. With IP addresse: 10.3.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 24.179.132.82        |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because you can scale your configuration to many more machines more efficiently and with fewer errors.

The playbook implements the following tasks:
- Installs apt packages: docker.io, python3-pip
- Installs pip package: docker
- Downloads the docker conatiner sebp/elk:761
- Configures the container to start with ports 5601, 9200, abd 5044 mapped
- Starts the container and enables the docker service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
  Web-1: 10.1.0.8
  Web-2: 10.1.0.9

We have installed the following Beats on these machines:
  -Filebeat
  -Metricbeat

These Beats allow us to collect the following information from each machine:
  Filebeat collects logs
  Metricbeat collects system metrics which could give you warning as reconnaissance or an attack is happening.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to the ansible directory.
- Update the hosts file to include each machines ip followed by ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to http://[your.VM.IP]:5601/app/kibanato check that the installation worked as expected.
