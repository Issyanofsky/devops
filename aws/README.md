<div align="center">

# **AWS**
![AWS](../pic/aws.gif)
</div>

# Legent:

   * [VPC (Virtual Private Cloud)](#VPC-(Virtual-Private-Cloud))
# Services:

   * [S3](./files/s3.md)
   * [Route 53](./files/route53.md)
   * [EC2 (Elastic Compute Cloud)](./files/ec2.md)
   * [Load Balancer](./files/LoadBalancer.md)
   * [RDS (Relational Database Service)](./files/RDS.md)

__Cloud Service Models:__ 

  * IaaS (Infrastructure as a Service): You get hardware resources (ex. AWS EC2).
  * PaaS (Platform as a Service): You get a platform to build and run apps (ex. Google App Engine).
  * SaaS (Software as a Service): You get a complete software application ready to use (ex. Microsoft 365).

__Types of clouds:__

  * Private Cloud: A cloud environment dedicated to a single organization.
  * Hybrid Cloud: A combination of private and public clouds, allowing data and applications to be shared between them.
  * Community Cloud: A cloud shared by a group of organizations with similar goals or security requirements. It’s like a private cloud but for a community of users.
  * Public Cloud: A cloud that is open to everyone, and resources are shared among multiple users. You use it over the internet.

# Importent Concepts:

## Regions 

a physical location where AWS has multiple data centers (e.g. us-east-1 (Northern Virginia) or eu-west-1 (Ireland)).

## Availability Zones (AZ)

one or more data centers within a region (e.g., us-east-1a, us-east-1b, us-east-1c).

## edge location

data centers designed to deliver content (like websites or videos) faster to users by caching content closer to them (e.g. AWS CloudFront uses Edge Locations to cache content for quicker access worldwide).

## IAM (Identity and Access Management) 

lets you create and manage users, groups, and roles. helps keep your AWS environment secure by ensuring that only authorized users can access certain resources.

Adding users, creating groups, assigining 2fA (under "security credantials) and more....

<div align="center">

# **VPC (Virtual Private Cloud)**
</div>

 A private network in the cloud where you can launch and manage your AWS resources (like EC2 instances, databases, and more). It allows you to control networking, security, and traffic routing for your resources in AWS.

 ## creating a VPC

 Navigate to VPC webpage --> create VPC

  * select VPC and More
  * set the following settings:

  __IPv4 CIDR block__ (dont need to change unless you wish other ipp range).
  __Number of Availability Zones__ set the zones for the VPC (recommended minimum 2).
  __Number of private subnets (minimum 2) --> expend "Customize subnets CIDR blocks and set the IP for each subnet:

        example: 
          Public subnet CIDR block in eu-central-1a - 10.0.101.0/24
          Public subnet CIDR block in eu-central-1b - 10.0.102.0/24 
          Private subnet CIDR block in eu-central-1a - 10.0.1.0/24
          Private subnet CIDR block in eu-central-1b - 10.0.2.0/24

  __NAT gateway__ (needed only if need connecting to Private subnet) - enough to choose 1 per AZ (one NAT for all zones).
  __VPC endpoints__ allow traffic to be ruted inside the VPC (without exiting the internet- less cost and better security).



<div align="center">

# **VPN**
</div>

Navigate to VPC webpage --> right side under Virtual private network (VPN)

ways to connet using VPN:

  __Virtual Private Gateway (VGW):__ A virtual gateway that connects your VPC (Virtual Private Cloud) to a remote network, like your on-premises data center or another VPC.
  
  __Site-to-Site Connection:__ A secure connection between your on-premises network (e.g., office or data center) and your AWS VPC using a VPN (Virtual Private Network).
  
  __Client VPN Endpoint:__ allows remote users (like employees) to securely connect to your AWS network from anywhere.

## VPN connection to EC2 (in a private Zone)

__1. Session Manager__ establish secure shell-like connections directly from the AWS Management Console or AWS CLI.

    Set Up Permissions for Session Manager:

          Navigate to IAM webpage --> Create a IAM role with AmazonSSMManagedInstanceCore policy attached.

          Attach this role to your EC2 instance.

          Make sure your EC2 instance has the SSM agent installed (he SSM Agent is installed by default on most modern Amazon AMIs (like Amazon Linux, Ubuntu, etc.)).
    
    Verify EC2 Instance is Managed by Systems Manager:

          Navigate to EC2 webpage --> Under Instances & Nodes, click Managed Instances.

          Make sure your EC2 instance appears in the list with a green status (meaning it is successfully managed by Systems Manager).
          
    Start a Session:

          Navigate to EC2 webpage --> Under Instances & Nodes, click Managed Instances.

          Click Start Session.

  __2. Bastion__

  Acts as a gateway or jump server that allows you to access instances that do not have public IP addresses.

  The Bastion Host need a public IP to allow SSH or RDP access from the internet (resident in public zone). it act like a proxy for the private Instances.

  __Launch an EC2 instance (Bastion Host):__

          Launch a EC2 instance in the public AZ (Ubuntu) with a public IP assign And key-pair.

          set security groups: Add an inbound rule that allows SSH (port 22) access from your IP address or IP range.

          ssh -o ProxyCommand="ssh -i bastion.pem -W %h:%p ec2-user@bastion-host" ec2-user@target-instance

          (e.g. ssh -o proxycommand=="ssh -i bastion.pem -w %h:%p ubuntu@3.127.27.209" -i prod.pem ec2-user@10.0.1.51)

  __* Note__ can use Route53 for using domain to reach the bastion.

__3. OpenVPN__ 

an open-source software that allows you to set up a VPN (Virtual Private Network). It creates a secure tunnel between your on-premises network (or local device) and a remote network (such as your AWS VPC).


          
