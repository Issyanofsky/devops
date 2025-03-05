<div align="center">

# **Kubernetes (K8s)**

</div>


![kubernetes](kubernetes.gif)



Kubernetes is an open-source platform for automating the deployment, scaling, and management of containerized applications (like Docker containers).

best practice setting: (min 3) Control plane servers. odd number of servers.

Distribution of kubernetes:

  * on premice:

      - k3s - light kubernetes virsion.
      - minikube - one server for all (Control and worker plane).
      - kubespray - a distribution with plugins - fast deploy.
      - kubeadm - basic kubernetes installation

  * cloud Kubernetes:

      - GKE - google kubernetes.
      - AKS - Azure kubernetes services.
      - EKS - Amazon (also eks).
      - IBM - cloud container service.
   
  
   <div align="center">

# **install Kubectl (Kubernetes command-line tool)**

</div>

# Linux install

    Download the latest release:

      curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"

   Make the kubectl binary executable:

     chmod +x ./kubectl

   Move the binary to a directory included in your PATH:

     sudo mv ./kubectl /usr/local/bin/kubectl

   Verify the installation:

     kubectl version --client

# Windows installation

   Download the latest Windows version of kubectl from:
     
      https://github.com/kubernetes/kubernetes/releases

   extract the content of the folder and set enviroment PATH to it.

     copy the kubectl.exe file to a folder.
     set his PATH in the enviroment.


    
   <div align="center">

# **install Minikube**

</div>




   
 

