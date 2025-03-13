<div align="center">

# **Rancher**

![Rancher](../pic/rancher.gif)

</div>

Rancher is a platform used to manage and deploy Kubernetes clusters. makes it easier to set up, manage, and scale Kubernetes clusters across different environments (like on-premises, in the cloud, or hybrid).


## Installing Rancher

This deployment is of single rancher node installation. it deployed in a Docker Container.

### Prerequisites:

A server to deploy the Container. this guide is on a AWS Instance.

__* IMPORTANT__ lossing the IP of the server will lose all connection to the rancher (changing the IP can only dont within the rancher).

on the AWS consol. 

Deploy a EC2 Instance with the following setting:
         
          type: t2.midium
          key-pair (for SSH connecting)
          allow SSH (apply all)
          Ubuntu (not AWS Linux)

set IAM Role

          gave the EC2 permissions to other mechine.
          
set Elastic IP for the EC2 

      on the Elastic IP assosiate it to the EC2 - under actions --> assosiate Elastic IP address
      (its free as long the EC2 is on)

### Connecting to the EC2

      ssh -i <certificate_name> ubuntu@<EC2_IP>

### Installing Docker

      sudo apt update
      curl -fsSL https://get.docker.com -o get-docker.sh
      sudo sh get-docker.sh

give user permission

      sudo usermod -aG docker <user> 
      (sudo usermod -aG docker ubuntu)

Verify:

log-off and log-on again to the server

      ssh -i <certificate_name> ubuntu@<EC2_IP>

type
      docker info

### Run Rancher

      docker run -d --restart=unless-stopped -p 80:80 -p 443:443 --privileged rancher/rancher

__*__ there is no need to set volume. the container has its own volume set.

Verify:

     docker ps
     
## Entering Rancher

type the IP of the EC2 on the browser

### log in

follow the instructions on the rancher webpage.

         docker logs <container_ID> 2>&1 | grep "Bootstrap password:"

__* Notice__ on the first login the rancher set the IP in his files. so make sure this IP (server) is right!!.

__* RECOMEND__ change password for better security.

### IMPORTANT to Know:

  * __Credentials:__ set credintials before creating any cluster to avoid permission issues (e.g. the acess key for AWS).
  * __Kubectl:__ the kubectl commands are made throw the rancher servers.
     - getting a kubeconfig file in the web page.
     - rancher server must be ON for executing kubectl commands.
  * __Delete:__ rancher can delete only what has been built with it (you can import other cluster for monitoring).
