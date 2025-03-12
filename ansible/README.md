<div align="center">

# **Ansible**

![Ansible](./pic/ansible.gif)
</div>

Ansible is a tool used for automating tasks like setting up servers, configuring software, and managing infrastructure.

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

# **Setting Remote mechine (computers)**

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

     
