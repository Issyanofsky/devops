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


__IMPORTANT__ the workflow (file .tf) contin the Providers and Resources. the correct file should be:

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

        terraform init

__*__ done once (or in case there a change in the structure - like modules inside)
