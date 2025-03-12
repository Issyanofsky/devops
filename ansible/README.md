<div align="center">

# **Ansible**

![Ansible](./pic/ansible.gif)
</div>

Ansible is a tool used for automating tasks like setting up servers, configuring software, and managing infrastructure.

example:

    ansible project:
    
[https://github.com/Issyanofsky/react-java0mysql](https://github.com/Issyanofsky/react-java0mysql)
  
    ansible exercise:

[https://github.com/Issyanofsky/react-java0mysql](https://github.com/Issyanofsky/ansible-class)

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

## Condition

Control the flow of tasks, allowing them to run only when certain conditions are met.

condition types:

   * __when__ The when statement allows you to run a task only if a condition is true.

         - name: Install nginx
          apt:
            name: nginx
            state: present
          when: nginx_installed.rc != 0  # Only run if nginx is not installed

    Boolean (True/False)
    
        - name: Install apache if apache_enabled is true
          apt:
            name: apache2
            state: present
          when: apache_enabled == true

   * __failed_when and changed_when__

     - __failed_when:__ This condition determines when a task is considered failed based on its result.
     - __changed_when:__ This condition controls when a task is considered changed (i.e., when it has modified something).

            - name: Check if a file exists
              stat:
                path: /path/to/file
              register: file_status
              failed_when: file_status.stat.exists == False  # Fail if the file doesn't exist
    
            - name: Update config file
              copy:
                src: config.conf
                dest: /etc/config.conf
              changed_when: false  # Task is never marked as "changed", even if it updates the file

   * __until__ You can use until with conditions to retry tasks until a certain condition is met.
    
            - name: Wait for service to be up
              service:
                name: nginx
                state: started
              register: service_status
              until: service_status.state == 'started'
              retries: 5
              delay: 10  # Retry every 10 seconds

## Loop

Allow to run a task multiple times with different inputs. This is useful when you need to repeat the same task for a list of items, like installing several packages, managing users, or iterating over files.

Ansible provides different ways to loop through data, such as using __loop__, __with_items__, or __with_dict__, but the modern and recommended approach is to use loop.

    Example (Loop over list of items):

        ---
        - name: Install multiple packages
          hosts: all
          become: yes
          tasks:
            - name: Install packages
              apt:
                name: "{{ item }}"
                state: present
              loop:
                - nginx
                - curl
                - git

## Ansible Vault

A feature in Ansible that allows you to encrypt sensitive data, such as passwords, API keys, or private information, so they can be safely stored in your playbooks and inventories without exposing them in plain text.

Ansible Vault is used to encrypt sensitive data and protect it with a password, ensuring that sensitive information remains secure within your automation workflows (can upload to Github without exposing secrets (password and such)).

  __Key Features:__

   * __Encryption:__ Ansible Vault encrypts files, variables, or even specific parts of playbooks, making them unreadable to unauthorized users.
   * __Password Protection:__ You can use a password to encrypt and decrypt these files, ensuring only authorized users can access sensitive information.

   __Use Cases:__   

   * Storing secrets like database passwords.
   * Protecting sensitive configuration files.
   * Encrypting variables in playbooks.

### Create a new encrypted file

This will open an editor where you can add encrypted content.

            ansible-vault create secret.yml

 ### Encrypt an existing file

            ansible-vault encrypt plain_text_file.yml


 ### Decrypt a file

            ansible-vault decrypt secret.yml

 ### Edit an encrypted file

            ansible-vault edit secret.yml

  ### Run a playbook with encrypted variables

  This will prompt you for the vault password to decrypt the content during execution.
  
           ansible-playbook --ask-vault-pass playbook.yml

## Ansible Roles

A way to organize playbooks and tasks into reusable, logical units. A role contains tasks, variables, handlers, files, templates, and defaults in a structured directory format.

Roles make your playbooks more modular, readable, and reusable.


    __Role structure:__

    deviding the YAML file (extracting the task part to a ceperate file (in the root folder)
    
        my_playbook/
          ├── site.yml
          └── roles/
              └── nginx/
                  └── tasks/
                      └── main.yml


    Example:

        roles/nginx/tasks/main.yml

            ---
            - name: Install nginx
              apt:
                name: nginx
                state: present
            
            - name: Start nginx service
              service:
                name: nginx
                state: started
                enabled: yes
                
        site.yml

            ---
            - name: Deploy nginx on webservers
              hosts: webservers
              become: yes
              roles:
                - nginx

    Run playbook:

            ansible-playbook site.yml

## Ansible Galaxy

a community platform where you can share, discover, and reuse Ansible roles and collections. You can find pre-made roles for various tasks, like setting up databases, web servers, or monitoring tools.

You can install roles from Galaxy using the ansible-galaxy command.

    Example (contain 2 galaxy roles):

            ansible-galaxy role install geerlingguy.docker

            ansible-galaxy role install geerlgguy.pip

    create a YAML file:

            ---
              - hosts: ansible
                vars:
                  pip_install_packages:
                    - name: docker
                roles:
                  - geerlingguy.pip
                  - geerlingguy.docker

    Deploy:

            ansible-playbook site.yml

 <div align="center">
 
   # Common Commands and FLags

</div> 

### Run Playbook

execute a playbook.

        ansible-playbook <playbook.yml>

if inventory.ini located on diferent folder:

        ansible-playbook -i <Inventory_file_path_&_Name> <playbook.yml>

        (ansible-playbook -i ../inventory.ini playbook.yaml)

### Ping All Hosts

check the connection to all hosts defined in your inventory.

        ansible all -m ping

### Check Specific Host(s)

run a task or command on a specific host or group of hosts from your inventory.

        ansible <host/group> -m <module>
        (ansible webservers -m ping)

### Run a Command on Hosts

run any command (shell command) on remote hosts.

        ansible <host/group> -m shell -a "command"

### Check the Hosts Inventory

This command shows the list of hosts defined in your Ansible inventory.

        ansible-inventory --list

### Test an Ansible Configuration

You can test if your Ansible configuration file (ansible.cfg) is set up correctly.

        ansible-config list

### Install a Role from Ansible Galaxy

To install roles from Ansible Galaxy, which is a community repository for Ansible content.

        ansible-galaxy install <role_name>

### Create a New Role

To create a new role in the default directory structure.

        ansible-galaxy init <role_name>

### Check for Syntax Errors in a Playbook

To validate the syntax of your playbook before running it. This runs the playbook in check mode, which means it shows you what would happen, but it doesn't make any changes.

        ansible-playbook playbook.yml --check

### View Available Collections

 List all available collections installed on your system.

         ansible-galaxy collection list

### View Ansible Version
    
check which version of Ansible is installed.

        ansible --version
        ansible-playbook --version
        ansible-galaxy --version

### List Hosts in an Inventory

List all the hosts in your inventory file.

        ansible-inventory --host <hostname>

### Get Facts from Hosts

Ansible can collect detailed information about your hosts using the setup module. This gives you "facts" about the system.

        ansible <host/group> -m setup
        (ansible webservers -m setup | grep OS_family)

### Run a Playbook with Extra Variables

If you want to pass extra variables while running a playbook.

        ansible-playbook playbook.yml -e "variable_name=value"

        (ansible-playbook site.yml -e "nginx_version=1.18")

### Run a Playbook with Tags

You can execute only specific parts of a playbook using tags.

        ansible-playbook playbook.yml --tags "tag_name"

### Run a Playbook with Limit

You can limit the playbook execution to specific hosts (useful for running playbooks on subsets of hosts).

        ansible-playbook playbook.yml --limit <host/group>

### View Available Modules

see all the available modules in your version of Ansible.

        ansible-doc -l

### Get Help on a Specific Module

To view documentation about a specific module.

        ansible-doc <module_name>

### Creating a file on all remote clients

       ansible all –m file –a “path=/home/iafzal/adhoc1 state=touch mode=700”

### Deleting a file on all remote clients

       ansible all –m file –a “path=/home/iafzal/adhoc1 state=absent”

### Copying a file to remote clients

       ansible all –m copy –a “src=/tmp/adhoc2 dest=/home/iafzal/adhoc2”

### Installing package (telnet and httpd-manual)

       ansible all –m yum –a “name=telnet state=present”

       ansible all –m yum –a “name=httpd-manual state=present”. 

### Starting httpd package service
   
       ansible all –m service –a “name=httpd state=started”

### Start httpd and enable at boot time

       ansible all –m service –a “name=httpd state=started enabled=yes”

### Checking httpd service status on remote client

       ansible all –m shell -a “systemctl status httpd”

### Remove httpd package

       ansible all –m yum –a “name=httpd state=absent”
OR
       ansible all –m shell -a “yum remove httpd”.

### Creating a user on remote clients

       ansible all –m user –a “name=jsmith home=/home/jsmith shell=/bin/bash state=present”

### To add a user to a different group

       ansible all –m user –a “name=jsmith group=iafzal”

### Deleting a user on remote clients

       ansible all –m user –a “name=jsmith home=/home/jsmith shell=/bin/bash state=absent”
OR
       ansible all –m shell –a “userdel jsmith”

### You can run commands on the remote host without a shell module e.g. reboot client1

      ansible client1 –a “/sbin/reboot”
