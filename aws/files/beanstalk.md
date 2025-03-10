<div align="center">

# **Elastic Beanstalk (EB)**

</div>

A service that helps you deploy and manage web applications and services in the cloud without needing to worry about the infrastructure (like servers).

## how it works:

  1. __Create an Application:__ upload your code (like a web app or API) to Elastic Beanstalk.
  2. __Choose Platform:__ Beanstalk supports various programming languages and platforms like Node.js, Python, Java, .NET, etc. You select the one that matches your app.
  3. __Environment Setup:__ Beanstalk automatically sets up the underlying infrastructure (like EC2 instances, load balancers, etc.) for you based on the app type and platform.
  4. __Deploy:__ After choosing the platform, you can deploy your application. Beanstalk handles scaling, load balancing, and monitoring for you.

## good for:

  - for tests and debug a app.
  - app that use one container.

# Elastic Beanstal

  Navigate to Beanstalk webpage --> Create applicatin

      Environment tier - choose the environment that fit your code.
      Application name - set a name for the Beanstalk environment.

      Platform - select the platform requiered for your code (Docker, Jave, python....)
      Presets - select availability (single instance is standart. High availability uses Loadbalancer to frovide high availability good fro production)).

  __Service access:__

      provide IAM role - setting the perrmissions for services (optional).
      EC2 key pair - provide key-pair for the EC2 (for SSH ).
      EC2 instance profile - allow your EC2 instances to perform required operations.

  __Virtual Private Cloud (VPC):__

      VPC - select the VPC where the Beanstalk would deploy in.
      Public IP address - set if need Public IP address.
      Instance subnets - on which subnets it should deployed.
      Database -  setting Database (if needed)

  __Configure instance traffic and scaling - optional:__

    seetings related to the Instance.

      EC2 security groups - select security group for the instnce.

      Environment type - select direct connection or throw LoadBalancer.

      Architecture -  instance types that are made available (i used x86_64).
      Instance types - the type of instance for deploy (t3.micro....).

      AMI ID - ami to deploy on the Instance.
      
  __Configure updates, monitoring, and logging - optional:__

      System - i choose Basic.

      Managed platform updates - update policy.

      Rolling updates and deployments - set how the update and deploy will be.

      Platform software - set which installatin should be on the instance.

      Environment properties - allowing you to provide environment varibels.
    
      
    
