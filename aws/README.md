<div align="center">

# **AWS**
![AWS](../pic/aws.gif)
</div>

# Legend:

   * [S3](./files/s3.md)
   * [Route 53](./files/route53.md)
   * [EC2 (Elastic Compute Cloud)](./files/ec2.md)
   * [Load Balancer](./files/LoadBalancer.md)
   * 

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

# **VPC (Virtual Private Cloud**
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
