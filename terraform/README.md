<div align="center">

# **TerraForm**

![Terraform](./pic/terraform.gif)
</div>

A tool that helps you automate and manage your cloud infrastructure in a simple and consistent way.

Instead of manually creating and configuring cloud resources (like servers, databases, and networks), you write code to describe the infrastructure you need. Terraform then automatically creates and manages those resources for you.

Terraform File use extention: __.tf__

# Instal Terraform (windows)

## 1. create a folder

 On the computer create a folder for placing the Terraform EXE file (e.g. c:\terraform).

## 2. Downlowd Terraform

Download the suited file from:

      https://developer.hashicorp.com/terraform/install

## 3. Copy content

Copy the content from the Download to the folder we just created (step 1).

## 4. Environment Setting

Add the PATH (the folder we created) to the Environment setting. so it will be accessable from all path.

<div align="center">

## **Providers**

</div>

  * Terraform interacts with cloud platforms and services through providers. Providers are plugins that allow Terraform to communicate with services like AWS, Google Cloud, Azure, etc.
  * Each provider has a set of resources (like EC2 instances, S3 buckets, etc.) that you can manage with Terraform.

  This example establish connection to AWS cloud:
  
      provider "aws" {
        region = "us-east-1"
        access_key = "....."
        secret_key = "....."
      }

<div align="center">

## **Resources**

</div>

Resources represent the actual cloud components you're creating or managing. For example, an EC2 instance on AWS, a storage bucket on Google Cloud, or a database on Azure.


Example for creating an EC2 instance:

      resource "aws_instance" "example" {
        ami           = "ami-0c55b159cbfafe1f0"  # Example AMI ID
        instance_type = "t2.micro"
      }


__* NOTICE__ the workflow (file .tf) contin the Providers and Resources. the correct file should be:

      provider "aws" {
        region = "us-east-1"
        access_key = "....."
        secret_key = "....."
      }

      resource "aws_instance" "example" {
        ami           = "ami-0c55b159cbfafe1f0"  # Example AMI ID
        instance_type = "t2.micro"
      }

<div align="center">

## **Deploying Terraform**

</div>

Creating a folder with the terraform .tf file. 

Navigate using Gitbash (Powershell) to the folder

## Init

Initilize the folder. create and download the nessery files needed for deploying the Terraform script.

     type in GitBash:
   
        terraform init

__*__ done once (or in case there a change in the structure - like modules inside)

## Plan

shows you what changes Terraform will make to your infrastructure based on your configuration.

     type in GitBash:
   
        terraform plan

## apply

After reviewing the plan, you run terraform apply to create or modify your infrastructure based on the configuration files.

it compare the "new" configuration to the state and apply the changes (not exucting all).

     type in GitBash:
   
        terraform apply

## detroy

delete the infrastructure. removes all the resources managed by Terraform.


     type in GitBash:
   
        terraform destroy

<div align="center">

## **State**

</div>
  
Terraform maintains a state file (usually called terraform.tfstate) that keeps track of your resources and their current status. This allows Terraform to know what resources exist and what needs to be changed when you apply updates.
The state file is important for managing the lifecycle of resources and keeping track of any changes.


<div align="center">

## **Variables (variables.tf)**

</div>

Variables in Terraform allow you to parameterize your configuration. Instead of hardcoding values like instance types, regions, or AMI IDs, you use variables so you can change them easily.

__Using Variables:__

    1. Create a variables.tf file in the same directory as the main.tf file.
    2. edit the file and Add the Variables. for example:

          variable "region" {
            description = "The AWS region to launch the instance"
            default     = "us-west-2"
          }
          
          variable "instance_type" {
            description = "The type of EC2 instance"
            default     = "t2.micro"
          }
   
    3. Edit the main.tf to get the Variables. example:

         provider "aws" {
           region = var.region
         }
         
         resource "aws_instance" "example" {
           ami           = "ami-0c55b159cbfafe1f0"
           instance_type = var.instance_type
         }

         
<div align="center">

## **Provisioners**

</div>

Execute scripts or commands on the resources after they are created or modified. It’s like performing a setup task (e.g., installing software) on your resources after Terraform has created them.

     Example (When Terraform creates an EC2 instance, it will automatically run the commands to install Nginx on it):

         resource "aws_instance" "example" {
           ami           = "ami-0c55b159cbfafe1f0"
           instance_type = "t2.micro"
         
           provisioner "remote-exec" {
             inline = [
               "sudo apt-get update",
               "sudo apt-get install -y nginx"
             ]
           }
         }


<div align="center">

## **Connections**

</div>

define how Terraform connects to a remote resource (like an EC2 instance) for tasks like provisioning or running scripts. Typically, you use SSH for Linux instances or WinRM for Windows.

     Example (Terraform uses the connection block to SSH into the instance (ubuntu user, using the private key) and execute commands like creating the hello.txt file):
       
         resource "aws_instance" "example" {
           ami           = "ami-0c55b159cbfafe1f0"
           instance_type = "t2.micro"
         
           connection {
             type        = "ssh"
             user        = "ubuntu"
             private_key = file("~/.ssh/id_rsa")
             host        = self.public_ip
           }
         
           provisioner "remote-exec" {
             inline = [
               "echo 'Hello, world!' > /home/ubuntu/hello.txt"
             ]
           }
         }


__Create SSH Key__

        ssh-keygen -t rsa
