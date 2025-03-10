<div align="center">

# **EKS (Elastic Kubernetes Service)**

</div>

A fully managed service that makes it easy to run and manage Kubernetes clusters on AWS.

__* NOTE__ the user that deploy the cluster has the admin privilage.

# Deploying EKS cluster


    Navigate to EKS on the webpage.

ways to deploy:

## 1. EKS Auto Mode - new feture to create a cluster.
## 2. using web:

       click create cluster --> custom configuration 


          disable EKS Auto mode

          cluster configuration:

              name: fill cluster name
              create recommended Role - move to role settings (choose: AWS service, Use case: EKS cluster --> next --> naming the Role and the permission needed)
              kubernetes version: select version for kunernetes cluster.
              upgrade policy: standart

              cluster access (set how to connect to the cluster):
                  Allow Cluster administration access
                  cluster authentication mode: Eks API and configmap

              --> secret encryption (didnt check because i used secretmanager)

              ARC Zonal shift ( allow pod to switch between zones): disabled

              --> next

              specify networking:

                  VPC: set the VPC for the cluster to deployed at.
                  subnets: define subnet for the deployment.
                  security group: set security group for port 443 (HTTPS), 6443 (used a pre defined SG)

              --> Cluster endpoint access - set how to access the API (for managing the cluster):
                        - Public - allowing access to the cluster outside the VPC.
                        - Private - must be inside the VPC.

                    add/edit source to public access endpoint - we left 0.0.0.0

              --> next

                  logs - didnt change anything (here can set logs)

              --> next

                  select add ons - adding addons for the cluser (i left as it was).

              --> next
                  
                  create

## Add Workers Nodes

        Navigate to EKS on the webpage --> enter the cluster --> compute --> add Node group

            configure node group:

                name: name for the group (e.x. EKS-ng)
                node IAM - set permission for the nodes (workers).

            --> create recomended

                aws service
                use case: EC2
                (can add cloudWatch for monitoring)
            
            --> next

            compute and scaling configuration:

                set which and how many mechine (nodes)

                Node auti repair configuration - service that fix issues with mechine (i set yes)

            --> next

                specifiy NEtworking - specify where the workers will run.

            --> create
            
## 3. installing using EKSctl (Recomended Way to Install EKS).

        

