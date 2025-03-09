<div align="center">

# **EC2 (Elastic Compute Cloud)**

</div>

virtual computers (called instances) to run your applications, websites, or services.

## Key Points:

  * Virtual Machines: EC2 provides virtual servers that you can use to run any software, just like a physical server, but with more flexibility.
  * Scalable: You can easily increase or decrease the number of instances based on your needs (e.g., handle more traffic or reduce costs).
  * Pay-as-you-go: You only pay for the computing power you use, and you can stop or start instances whenever you need.
  * Customizable: You can choose the size, operating system, and configuration of your EC2 instance based on your needs.

__AMI__ - Amazon Machine Image. Image run on the EC2 (e.g. Ununtu).
__region__ - each EC2 deploy in a specific region.

## EC2 instances types:

  * __On-Demand Instances (Regular Instances):__ the most flexible EC2 instances. You pay by the hour or second, depending on the instance type.
  * __Reserved Instances:__ You reserve an EC2 instance for a 1 or 3 year term in exchange for a significant discount compared to on-demand prices.
  * __Savings Plans:__ A flexible way to save money on EC2 usage. You commit to a certain amount of usage (in dollars) per hour for 1 or 3 years.
  * __Spot Instances:__  You can bid for unused EC2 capacity at a lower price. The catch is that AWS can terminate the instance with little notice if they need the capacity back.

<div align="center">

# **Launching Instance (EC2)**

</div>

     Navigate to EC2 page -->

laumch instance

    press - launch Instance -->

set:

   name - type Instance name.
   number of instances - Number of Instances to create.
   AMI - choosing Image and version for deploying on the Instance.
   key-pair - if SSH is needed.

       press "create new key-pair (choose RSA type .pen) --> "create key pair"

   * best practice is to create each instance a key-pair of its own.

   under firewall:

      select security group.

      chack the __SSH__ to allow ssh connect by IP.

Launch Instance:

     --> Launch Instance


## Other settings Available

   * __IAM instance role__ - allowing the Instance permission to other services over the cloud.
   * __placement group__ - allow creating "cluster" group of Instances.
   * __spot__ - deploying Instance in spot.
   * __user_data__ - script that execute once the Instance deployed (once only).
   

<div align="center">

# **Connecting to Instance (EC2)**

</div>

# SSH

Navigate to EC2 page --> select the Instance you want to connect to.

     --> press "connect"
     --> copy the line for SSH connection (e.g ssh -i <key.pem> ubuntu@10.185.250.129)

     * useing the key-pair you created for the Instance.

# Monitor and Trubleshoot

Navigate to EC2 page --> select the Instance you want to connect to --> actions --> monitor and trubleshoot --> Get Instance screen

(This will display the Instance screen for preview).


Navigate to EC2 page --> select the Instance you want to connect to --> actions --> monitor and trubleshoot --> Get System logs

(This will display logs).

<div align="center">

# **Auto Scaling**

</div>

