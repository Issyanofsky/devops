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

