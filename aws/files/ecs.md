<div align="center">

# **ECS (Elastic Container Service)**

</div>

__Features:__

  * container Orchestartor.
  * container Management Service.
  * Scaleable & High Availability.
  * Natural fit in the Micro-service architucture.
  * All tyoe of eorkload.
  * Integration with CI/CD tools (AWS native and 3rd party).

__not fit for large scales:__

  * suit for small cluser (like 10 conainers).
  * cant manage envirioments ( no namespace for example).
  * can't add Database on the cluster.
  * cant move between clusers.

<div align="center">

# **Create ECS**

</div>

    Navigae to ECS webpage --> ECS

    --> create cluster -->

         Infrastructure - where to deploy the cluser (FARGATE or EC2 instance).

         choose Operate System (i choosed Amazon Linux)

         EC2 instance Role - (i let it create it).

         Desire Capacity - number of instances to deploy.

         key-pair - Optional. if need to enter the instances.

    under network:

        PVC - select the pvc to install the cluster.

        security group - set port to open to the cluster ( i opened - port 80, 22, 5000-5500).

        public IP - set this to get a public Ip for the cluster.

    --> create
    
<div align="center">

# **Deploy on ECS**

</div>

  __Prerequisites:__

     1. Docker Image: You need to have a Docker container image ready. This can be stored in Amazon ECR (Elastic Container Registry) or any other container registry like Docker Hub. 
     2. AWS CLI Installed: Ensure you have the AWS CLI installed and configured on your local machine.
     3. IAM Permissions: Ensure your AWS account has appropriate IAM permissions to use ECS, ECR, and other required services.

 [ECR (Elastic Container Registry)](ecr.md)  
 
## 1. Create an ECS Task Definition:

The task definition is a blueprint for your application (Docker container) and tells ECS how to run your containers.

    Navigate to the ECS Console and click Task Definitions in the left-hand menu.

    click create new Task Definition

          name: enter name for the task.
          choose mechine to deploy on (aws Fargate or EC2 instances).
          Container Definitions:
              - Click Add container.
              - container name: Name of your container (e.g., my-app-container).
              - Image: Use the full ECR image URL: 123456789012.dkr.ecr.us-west-2.amazonaws.com/my-app-repo:latest (or other repository).
              - Memory and CPU: Set the CPU and memory requirements for your container.
              - Task Role - setting permission (if needed) for conecting to aws services (e.g S3).
           Host:
             setting ports to have access to the containers.

     --> create

## 2. create task (service) - execute container

     navigate to ECS webpage --> go to Clusters --> select the cluster you created --> create (in the service Tab)

     choose setting as requiered:

         Fargate or EC2.
         select the task Definition for deploy.
         set service name.
         Configure the desired number of tasks (how many instances of your app you want to run).
         Set up a load balancer (if needed) to distribute traffic across multiple instances of your service.

     --> create


## Verify the Deployment:
   
  * After creating the ECS service, you can go to the Tasks tab to see the running task(s).
  * If you set up a load balancer, you can access your application through the load balancer's DNS name.
  * If using Fargate, the tasks will automatically scale based on the configurations you set.

## Optional: Set Up Auto-Scaling

 * ECS allows you to automatically scale the number of running containers based on demand (e.g., traffic or CPU usage).
 * You can set up auto-scaling by modifying the ECS service settings and defining scaling policies.



   
   
