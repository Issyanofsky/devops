<div align="center">

# **EKS (Elastic Kubernetes Service)**

</div>

A fully managed service that makes it easy to run and manage Kubernetes clusters on AWS.

__* NOTE__ the user that deploy the cluster has the admin privilage.

# Deploying EKS cluster


    Navigate to EKS on the webpage.

    click create cluster --> custom configuration 


          disable Eks Auto mode

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

            
    
