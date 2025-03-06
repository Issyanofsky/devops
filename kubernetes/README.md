<div align="center">

# **Kubernetes (K8s)**

</div>


![kubernetes](kubernetes.gif)



Kubernetes is an open-source platform for automating the deployment, scaling, and management of containerized applications (like Docker containers).


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


 # cluster Architecture

  * Control plane:
       - API server - comunicating with the cluster (usualy port 8443). uses self certificate to secure communicating between nodes.
       - Scheduler - The Scheduler is responsible for deciding where the workloads (like Pods) should run inside the cluster.
       - Controller Manager - responsible for making sure that the current state of the cluster matches the desired state.
       - etcd -  key-value store that Kubernetes uses to store all its cluster data.

  * Worker nodes components:
       - kubelet -  is an agent that runs on each node in your Kubernetes cluster.
       - kube-proxy - a network proxy that runs on each node in the Kubernetes cluster.
       - Container Runtime - oftware responsible for running containers on the nodes.

## high Availability

Using more then one Control plain for high availability of the cluster. best practice setting odd number of servers (min 3 Control plane servers). 

     * Importent: there is a need of a LoadBalancer for high availability and fault tolerance (must be installed primerly to the cluster). A Load Balancer is necessary to distribute incoming API requests evenly among the multiple Control Plane nodes and to ensure seamless operation in the following scenarios (HPProxy, Nginx, AWS (NLB,ALB)).

     
   <div align="center">

# **install Kubectl (Kubernetes command-line tool)**

</div>

check if already kubectl install, by:

   which kubectl


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

# **Kubectl Commands**

</div>

    * kubectl get nodes - display cluster nodes.
    * kubectl get pods -A - display all pods on cluster.
    * kubectl delete pod <pod_Name> - delete pod.
    * kubectl describe <pod_Name> - describe pod info.
    * kubectl logs <pod_Name> - display pods log.

 ## running pod using yaml

   apply pod:
    
       kubectl apply -f <file_Name.yaml>

  delete pod

      kubectl delete pod <pod_Name>

 ## kube exec

   execute command on a running pod.

      kubectl exec -it <pod_Name> --/bin/bash - open a bash on the running pod.

 ## kubectl run

   applying (runing) a pod coommand (without yaml file)

     kubectl run -i -tty --image=<image_name> --restart=never --sh


    
   <div align="center">

# **Minikube**

</div>

[follow the steps on (***](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)

## windows install

   using PowerShell:

     New-Item -Path 'c:\' -Name 'minikube' -ItemType Directory -Force Invoke-WebRequest -OutFile 'c:\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing
     
   Add the minikube.exe binary to your PATH (Make sure to run PowerShell as Administrator).

    $oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
    if ($oldPath.Split(';') -inotcontains 'C:\minikube'){
      [Environment]::SetEnvironmentVariable('Path', $('{0};C:\minikube' -f $oldPath), [EnvironmentVariableTarget]::Machine)
    }


## minikube commands

  * minikube start - Start your cluster.
  * minikube pause - Pause Kubernetes without impacting deployed applications.
  * minikube unpause - Unpause a paused instance.
  * minikube stop - Halt the cluster.
  * minikube config set memory 9001 - Change the default memory limit (requires a restart).
  * minikube addons list - Browse the catalog of easily installed Kubernetes services.
  * minikube start -p aged --kubernetes-version=v1.16.1 - Create a second cluster running an older Kubernetes release.
  * minikube delete --all - Delete all of the minikube clusters.
  * minikube status

  minikube start driver=virtualbox --no-vtx-check
 

<div align="center">

# **Services (svc)**

</div>

Service is a resource that defines how to access a set of Pods, and it can automatically balance traffic between them.

Types of Services:

     * ClusterIP - only accessible within the Kubernetes cluster.
     * NodePort - accessible from outside the cluster (range port 30000-32767).
     * LoadBalancer - uses an external load balancer to distribute traffic.

## display services

    kubectl get services -A - display all services in the cluster.

    kubectl get svc -n namespace - display services in a specific namespace.

## discribe

  kubectl describe svc <service_Name> - display descriptionn of the service setting.

## delete service

  kubectl delete -n <namespace>  svc <service_Name> - delete service name

## deploy service using command (not yaml)

  kubectl expose deploy <deploy_Name> --port 3000 --name <service_Name>

## deply service using YAML

  after creating a yaml file for creating a service:
  
      kubectl apply -f <yaml_file>

  example of yaml:

     apiVersion: v1
     kind: Service
     metadata:
       name: myapp-service
     spec:
       selector:
         app: myapp  # Selects Pods with this label
       ports:
         - protocol: TCP
           port: 80
           targetPort: 80
       type: NodePort  # Exposes the service outside the cluster
