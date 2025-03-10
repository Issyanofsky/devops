<div align="center">

# **CodeDeploy**

</div>

A service that helps you automatically deploy (install or update) your code to servers, virtual machines, or cloud instances.

__Tools for CD__

   * AWS CodeDeploy - a deployment service that automates the process of deploying your application to various compute resources (like EC2 instances, on-premises servers, or AWS Lambda).
   * AWS CodePipeline - service for automating the entire software release pipeline. It connects different stages of your application development process, like building, testing, and deploying.

__Sync with GitHub or S3__

  1.  deploy content - the code for deploy (like yaml).
  2.  connection to repository (like GitHub or s3 - requier IAM role).
  3.  install agent on each of the servers (check if an update exist).

__CodeDeploy key components:__

      Application - name of code o deploy.
      Deployment configuration - Rules and conditions for success/failure during distribution.
      Deployment group - group of servers (EC2) for distributing.
      IAM instance profile - roles attached to the servers (EC2) that allow access to GitHub or S3).
      Revision - the version for distribute.
      Service rolw - role allowing CodeDeploy for AWS services.
      Target revision - which version will deployed.

<div align="center">

# **Create AWS CodeDeploy**

</div>

## 1. IAM Role

      creating 2 IAM roles:

        - Role for the EC2 instances.
        - Role for CodeDeploy.

  __IAM Role for the EC2 instances__:

        Navigate to IAM webpage.

        create Role --> 

            set:
            
            AWS Service
            use case -  (EC2)
            permissions policy - choose AmazonEC2RoleForAWSCodedeploy --> Role name (e.g. EC2codedeploy) --> create Role

  __IAM Role for the CodeDeploy Service__:

        Navigate to IAM webpage.

        create Role --> 

            set:
            
            AWS Service
            use case -  codedeploy
            permissions policy - choose role needed --> Role name (e.g. odedeploy-role-service) --> create Role

## 2. Deploy mechine (EC2)

__(can be done within the CodeDeploy page - there a need to add under UserData the agent for codeDeploy).__


        Navigate to EC2 webpage.

        instances -->> create Instance:

            mechine name - add a name suit to the mechines (EC2).
            choose OS - choose the Operating system (like Amazon kinux2).
            
            under network setting:
                allow HTTP
                key-pair - Optional
                
            under Advanced setting:
            
                set the Role we created.
                
            under UserData (example):
            
                #!/bin/bash
                # This installs the CodeDeploy agent and its prerequisites on Ubuntu 22.04.
                
                sudo apt-get update
                sudo apt-get install jq ruby-full ruby-webrick wget -y
                
                SOURCE="https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/releases/"
                DEBFILE=$(curl -s https://aws-codedeploy-us-east-1.s3.us-east-1.amazonaws.com/latest/LATEST_VERSION| jq .deb -r| sed -e 's|releases/||')
                DEBNAME=$(echo $DEBFILE | sed -e 's|.deb||')
                
                cd /tmp
                wget $SOURCE$DEBFILE
                mkdir $DEBNAME
                dpkg-deb -R $DEBFILE $DEBNAME
                sed 's/Depends:.*/Depends:ruby3.0/' -i ./$DEBNAME/DEBIAN/control
                dpkg-deb -b $DEBNAME/
                sudo dpkg -i $DEBFILE
                systemctl list-units --type=service | grep codedeploy
                sudo service codedeploy-agent status
              
             --> launch Instance

__Recomended:__ adding Tag (e.g codeDeploy true) for better managing of deployments.

## 3. setting CodeDeploy 

        Navigate to CodeDeploy webpage.

        creating a script which defines the deployment process and instructions for deploying an application to an EC2 instance or other compute resources.

        example - 

              version: 0.0
              os: linux
              files:
                - source: /index.html
                  destination: /var/www/html/
              hooks:
                BeforeInstall:
                  - location: scripts/install_dependencies
                    timeout: 300
                    runas: root
                  - location: scripts/start_server
                    timeout: 300
                    runas: root
                ApplicationStop:
                  - location: scripts/stop_server
                    timeout: 300
                    runas: root

        create application --> 

              Application anme - anming the process.

              computer platform - define wher we deploy (i choose EC2)

              --> creat app

      create deployment group:

            create deployment group -->

                Deployent group name - naming the group.

                Service Role - Set the IAM role we created (step 1).

                Deployment type - (i set to In-place)

                Environment configuration - selecting the servers to run on (i choose Amazon EC2 instance).

                setting the mechine to install - by Name or by Tag.

                agent configure with.. - (if agent wasnt install) i choose Never because we install the agent already on deploying the EC2 (step 2)).

                Deploy setting

                LoadBalancer (if we have one).

                --> create deployment group
                
## 4. setting what to deploy

      navigate to deployment (in CodeDeploy web page)

      create deployment --> 
          
          Revision Type (where the app installed).

          GitHub token (if already connected to git (on the computer) it will create a token automaticaly. there is only need to give a name.

          enter Repository Name - (e.g. https://github.com/Issyanofsky/Codedeploy)

          Commit in - set the commit to handle.

          --> create deployment
          

<div align="center">

# **Create AWS CodePipeline**

</div>

doesnt Build but can work with Jenkins (for example).

## 1. preperations:

   * copy or clone the code to GitHub
   * create an IAM Role for Jenkins to use.
   * install and configure Jenkins and AWS CodePipeline plugin for Jenkins.

## 2. craete the pipeline

  navigate to pipeline on AWS web page.

      step 1: pipeline name.
      step 2: source: girhub.
      step 3: build, choose Add Jenkins (in provider name) 
      step 4: Service Role- set the service Role.
      step 5: review.

__Add steps to te pipeline:__

    look up the IP address of an instance.

    create a Jenkins project for testing the Deployment.

    create a forth stage

      
