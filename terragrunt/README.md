<div align="center">

# **Terragrunt**

![Terragrunt](./pic/terragrunt.gif)
</div>

Terragrunt is a tool that works with Terraform to make managing infrastructure easier. It helps organize and simplify the use of Terraform configurations, especially when you have multiple environments (like dev, staging, and production).

Terragrunt automates tasks like setting variables, handling state files, and working with modules, making it less repetitive and reducing errors. It helps you keep your Terraform code clean and DRY (Don't Repeat Yourself).

Example (creating EKS and ECS cluster using Terragrunt): https://github.com/Issyanofsky/infra

## pre-hook, post-hook, and error-hook

In Terragrunt, pre-hook, post-hook, and error-hook are commands you can use to run custom scripts before, after, or if something goes wrong during the Terraform run.

  * __per-hook:__ Runs a command or script before Terraform starts. For example, you can use it to check for prerequisites or set up something needed for the infrastructure.
  * __post-hook:__ Runs a command or script after Terraform finishes. You can use this to do cleanup, send notifications, or any other task once the changes are applied.
  * __error-hook:__ Runs a command or script if Terraform fails (e.g., if an error happens during the process). You can use it for logging or alerting in case of failure.

      Example:
    
          terraform {
            source = "../modules/network"
          }
          
          # Pre-hook: Run before Terraform plan or apply
          locals {
            pre_hook_command = "echo 'Running pre-hook: Checking prerequisites...'"
          }
          
          # Run pre-hook before any terraform commands
          dependencies {
            pre_hooks = [
              {
                command = local.pre_hook_command
                args    = []
              }
            ]
          }
          
          # Post-hook: Run after Terraform apply
          locals {
            post_hook_command = "echo 'Running post-hook: Sending notifications...'"
          }
          
          # Run post-hook after terraform apply
          post_hooks = [
            {
              command = local.post_hook_command
              args    = []
            }
          ]
          
          # Error-hook: Run if Terraform fails
          locals {
            error_hook_command = "echo 'Error occurred: Running error-hook for logging...'"
          }
          
          # Run error-hook if terraform fails
          error_hooks = [
            {
              command = local.error_hook_command
              args    = []
            }
          ]

<div align="center">

# **Install Terragrunt**

</div>

__1. download Terragrunt.exe__

     Navigate to https://terragrunt.gruntwork.io/docs/getting-started/install/.

     Download the correct file (for windows download - terragrunt_windows_amd64.exe)

__2. Copy file (Terragrunt.exe)__

    Copy content to a NEW folder on the computer.

__3. set Environment setting__

    Set the PATH of the folder just created in the environment setting of windows.

__4. Check Installation__

    type:

      terragrunt --version 

<div align="center">

# **Terragrunt commands**

</div>

## init

This command initializes the Terragrunt working directory, setting up necessary Terraform providers and modules.

     Example:

        terragrunt init
        
## plan

This command generates an execution plan for Terraform. It shows what changes Terragrunt will make to your infrastructure.

     Example:

        terragrunt plan

## apply

This command applies the changes defined in your Terraform configuration to your infrastructure.

     Example:

        terragrunt apply

## destroy

This command destroys all the resources defined in your Terraform configuration, effectively removing the infrastructure.

     Example:

        terragrunt destroy

## output

This command displays the outputs from a previously applied Terraform plan. Useful to view the values defined in your Terraform output blocks.

     Example:

        terragrunt output


## validate

This command checks the syntax and validity of your Terraform configuration files.

     Example:

        terragrunt validate

    Also for validates all the Terraform configurations in all directories.

        terragrunt validate-all

## run-all

Runs the command in all subdirectories (environments) recursively. Useful if you have multiple environments or modules.

     Example:

        terragrunt run-all plan
        terragrunt run-all apply
        terragrunt run-all destroy
        terragrunt run-all output (Retrieves the outputs from all Terraform configurations recursively across multiple environments.) 

## state

Interacts with the Terraform state, allowing you to perform actions like show, list, etc.

     Example:

        terragrunt state list
