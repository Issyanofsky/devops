<div align="center">

# **Ansible**

![Ansible](./pic/ansible.gif)
</div>

Ansible is a tool used for automating tasks like setting up servers, configuring software, and managing infrastructure.

example:
  ansible project: [https://github.com/Issyanofsky/react-java0mysql](https://github.com/Issyanofsky/react-java0mysql)
  ansible exercise: [https://github.com/Issyanofsky/react-java0mysql](https://github.com/Issyanofsky/ansible-class)

## Key Points:

  1. __Configuration Management:__ It helps automate the setup and management of servers (like installing software, updating settings, etc.).
  2. __Simple Syntax:__ Uses a simple language (YAML) to define tasks. These tasks are written in playbooks.
  3. __Agentless:__ You don’t need to install anything on the target servers. It uses SSH to communicate with them.
  4. __Idempotent:__ It ensures that running the same tasks multiple times won’t cause issues (i.e., the system will only change if needed).
  5. __Scalable:__ You can manage one server or thousands with the same tool.

__*__ on the free version - it doesnt have a Database.

__*IMPORTANT__ only work on Linux. Ansible must be deploy on a Linux base server.

## Good for:

  1. __Provision System:__ It sets up new machines or servers by installing the necessary software and configurations.
  2. __Configure System:__ It adjusts system settings, like network configurations or software settings, to match a desired state.
  3. __Deploy Apps:__ It installs and updates applications on servers.
  4. __Manage Systems and Apps:__ It ensures the systems and apps are running smoothly and as expected, fixing issues if needed.

__* NOTE__ Not good for installing operation systems.

<div align="center">

# **Install Ansible Server**

</div>

https://www.ansiblepilot.com/articles/how-to-install-ansible-in-ubuntu-24.04-ansible-install/

## 1. Prerequisites

  * A Linux server for deploying Ansible.

## 2. Creating Key-pair

creating a key-pair for connecting  to the network mechine using SSH.
    
    Log into the server, and type:

          ssh-keygen -t rsa

## 3. Install Ansible

on the ansible server (log into it):

          sudo apt update
          sudo apt upgrade
          sudo apt install ansible

Verify Installation:
    
          ansible --version
          ansible-playbook --version
          ansible-galaxy --version

__*IMPORTANT__ check that all versions are the same.

<div align="center">

## **Setting Remote mechine (computers)**

</div>

Set the remote mechine to allow access to the Ansible (root privilage).

  1. __export public key__

     Allowing SSH connection using key-pair (avoiding passward).

           From within the Ansible server (repeat this for each remote mechine):

                 ssh-copy-id <ansible_user>@<mechine_name or IP>
     
  2. __Set root permission (on Ubuntu)__
     
      gives the user permission to run any command as any user (including root) without needing to enter a password when using sudo

           On each of the mechine (connect to each one), set root permission.
     
                sudo visudo

           roll down, under %sudo, Add the following line:

               <user> ALL=(ALL) NOPASSWD: ALL

 <div align="center">
 
   # structure
   
![Ansible](./pic/ansible1.gif)
</div>    

## Key files structure

  * __Inventory:__ This file lists all the servers (hosts) that Ansible will manage. It can be a simple text file where you list server names or IP addresses.
  * __Playbook:__ A playbook is a YAML file where you write instructions (plays) for Ansible to follow. It tells Ansible what tasks to run on the servers (like installing software, copying files, etc.).
  * __Roles (optional):__ for organizing tasks into reusable units.

  Example of file structure:

          ansible/
            ├── inventory/       # List of servers
            ├── playbooks/       # YAML playbook files
            └── roles/           # Optional, for organizing tasks

## Creating Ansible evironment

 initialize an Ansible configuration file with all options disabled.

       on the absible server:

           ansible-config init --disabled > ansible.cfg

__*Optionally__ 

    create a folder and create a ansible.cfg file manualy.

    Add the follwoing line to the ansible.cfg:

          [defaults]
          inventory=<location_of_the_inventory_file>

## Setting Inventory File

Simple text file where you list server names or IP addresses.

Add the mechine to manage in a list:

          nano inventory.ini

  add the mechine (including the Ansible), example:

          [remote-controler]
          ansible ansible_host=172.0.0.1 ansible_connection=local become=true
          
          [control-plane]
          cp ansible_host=192.168.1.70 ansible_become=true
          
          [workers]
          w0 ansible_host=192.168.1.71 ansible_become=true
          w1 ansible_host=192.168.1.72 ansible_become=true
          
          [k8s_cluster:children]
          control-plain
          workers


## Ansible playbook

__key structure:__

  * __hosts:__ Specifies the target machines or groups of machines (from the inventory) where tasks will be executed.
  * __Tasks:__ A list of actions (commands or modules) to be performed on the hosts. Each task typically uses a module, like installing a package or copying a file.
  * __Variables:__ Optional, but you can define variables that can be reused throughout the playbook.
  * __Handlers:__ Special tasks that only run when notified by other tasks (like restarting a service after a configuration change).
  * __Name:__ A human-readable description of the playbook, tasks, or handlers, used for clarity and documentation.
  * __tags:__ used to run specific parts of a playbook or limit the execution of tasks. This is helpful when you only want to run certain tasks instead of the entire playbook.
  * __become:__ used to execute tasks with escalated privileges (like sudo), allowing Ansible to run commands as a different user, typically as the root user.

    Example:

        ---
        - name: Example playbook
          hosts: webservers
          become: yes  # Use sudo to execute tasks as root
          vars:
            app_name: "myapp"
          
          tasks:
            - name: Install package
              apt:
                name: "{{ app_name }}"
                state: present
        
            - name: Start service
              service:
                name: "{{ app_name }}"
                state: started
        
          handlers:
            - name: Restart service
              service:
                name: "{{ app_name }}"
                state: restarted

## Ansible Roles

A way to organize playbooks and tasks into reusable, logical units. A role contains tasks, variables, handlers, files, templates, and defaults in a structured directory format.

Roles make your playbooks more modular, readable, and reusable.

