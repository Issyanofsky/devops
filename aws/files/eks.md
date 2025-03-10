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

Simple way to create and manage Kubernetes clusters on AWS.

__Install eksctl__

        eksctl is a command-line tool for creating and managing EKS clusters. It allows you to define and deploy the cluster easily using a YAML configuration file.

        Install guide:
        
            https://eksctl.io/installation/

        
__Install AWS CLI & Configure AWS__

        Make sure the AWS CLI is installed and configured with your AWS credentials.

            aws configure

            Enter your AWS Access Key ID, Secret Access Key, and the region (e.g., us-west-2).

__Create a YAML File for the Cluster__

        Create a YAML file (cluster.yaml) to define your EKS cluster's settings.

        Example:

            apiVersion: eksctl.io/v1alpha5
            kind: ClusterConfig
            metadata:
              name: cluster-demo
              region: eu-central-1
            vpc:
              subnets:
                public:
                  eu-central-1a: { id: subnet-0d8a5cf25b3ac2688 }
                  eu-central-1b: { id: subnet-08bcc9b1169ccf5ee }
                  eu-central-1c: { id: subnet-04c60d9bcb3843d5f }
              clusterEndpoints:
                privateAccess: true
                publicAccess: true
            managedNodeGroups:
              - name: managed-ng-1
                minSize: 2
                maxSize: 4
                instanceType: t2.micro
                desiredCapacity: 3
                volumeSize: 30
                ssh:
                  allow: false
                labels: {role: worker}
                tags:
                  nodegroup-role: worker
                iam:
                  withAddonPolicies:
                    externalDNS: true
                    certManager: true
            iam:
              withOIDC: true
            addons:
            - name: vpc-cni
              attachPolicyARNs:
                - arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy
              resolveConflicts: overwrite

    Open Gitbash (PowerShell):

        Navigate to the Folder containing the YAML file.

        Createing the cluster. type command:
        
            eksctl create cluster -f <cluster.yaml>

__Delete__

            eksctl delete cluster --region=ea-central-1 --name=cluster-demo --wait
            
