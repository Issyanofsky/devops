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

![HAProxy](HAProxy.gif)

Using more then one Control plain for high availability of the cluster. best practice setting odd number of servers (min 3 Control plane servers). 

* Importent: there is a need of a LoadBalancer for high availability and fault tolerance (must be installed primerly to the cluster). A Load Balancer is necessary to distribute incoming API requests evenly among the multiple Control Plane nodes and to ensure seamless operation in the following scenarios (HAProxy, Nginx, AWS (NLB,ALB)).

     
   <div align="center">

# **install Kubectl (Kubernetes command-line tool)**

</div>

check if already kubectl install, by:

   which kubectl

## Linux install

    Download the latest release:

      curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl"

   Make the kubectl binary executable:

     chmod +x ./kubectl

   Move the binary to a directory included in your PATH:

     sudo mv ./kubectl /usr/local/bin/kubectl

   Verify the installation:

     kubectl version --client

## Windows installation

   Download the latest Windows version of kubectl from:
     
      https://github.com/kubernetes/kubernetes/releases

   extract the content of the folder and set enviroment PATH to it.

     copy the kubectl.exe file to a folder.
     set his PATH in the enviroment.


# Connecting to Cluster

list all the contexts defined in your kubectl configuration file and the active one (with "*").

      kubectl config get-contexts

      kubectl config view - display info of the cluster we connected.

to connect the local computer to the cluster:

     copy from the Control plane the file, located:

     sudo cat ~/.kube/config

     paste the content to a new file (ex. k8sconfig), located in the local computer (ex. C:\Users\ec\.kube):

     export KUBECONFIG=~/.kube/k8config - set to the config file we created.

Verifiy:

    kubectl config get-contexts

    or any kubectl command:

    kubectl get nodes
     
     

   <div align="center">

# **Labels**

</div>

Adding Labels to nodes allow to give more flexibility in scheduking pods to host (ex. GPU-nodes).

Viewing Node Labels

      kubectl get nodes --show-labels
      
   Or for a specific node:

      kubectl describe node node-01

Adding or Modifying Node Labels

     kubectl label node node-01 disk=ssd
     
Update an existing label:

    kubectl label node node-01 env=production --overwrite

## Taints and Tolerations (Advanced Node Labeling)

Labels alone don’t restrict access—they just help with selection. To prevent pods from scheduling on certain nodes, you use taints, and pods need tolerations to bypass them.

Taint a node:

     kubectl taint nodes node-01 special=gpu:NoSchedule - prevents pods from scheduling on node-01 unless they tolerate special=gpu.


<div align="center">

# **Secrets**

</div>

Secrets are Kubernetes objects designed to store and manage sensitive information, such as passwords, API keys, tokens, or certificates. They keep this data separate from your application code or pod definitions, improving security and flexibility.

Common Use Cases:

   * Database Credentials: Store username/password for a database.
   * API Tokens: Pass tokens to apps securely.
   * TLS Certificates: Use kubernetes.io/tls secrets for Ingress or apps needing HTTPS.
   * Registry Authentication: Pull images from private Docker registries.

## Creating a Secret

Using kubectl:

     kubectl create secret generic my-secret --from-literal=username=admin --from-literal=password=supersecret

Using a YAML File:

     apiVersion: v1
     kind: Secret
     metadata:
       name: my-secret
     type: Opaque
     data:
       username: YWRtaW4=  # base64 for "admin"
       password: c3VwZXJzZWNyZXQ=  # base64 for "supersecret"     

    * Note: The data field requires base64-encoded values. You can encode manually (echo -n "admin" | base64) or let kubectl handle it with --from-literal.

From Files:

    echo -n "admin" > username.txt
    echo -n "supersecret" > password.txt
    kubectl create secret generic my-secret --from-file=username.txt --from-file=password.txt

## Using Secrets in Pods

consumed by pods in two ways:

1. Environment Variables

    apiVersion: v1
    kind: Pod
    metadata:
      name: my-pod
    spec:
      containers:
      - name: my-app
        image: my-app:latest
        env:
        - name: USERNAME
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: username
        - name: PASSWORD
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: password

2. Mounted Files

     apiVersion: v1
     kind: Pod
     metadata:
       name: my-pod
     spec:
       containers:
       - name: my-app
         image: my-app:latest
         volumeMounts:
         - name: secret-volume
           mountPath: "/etc/secrets"
           readOnly: true
       volumes:
       - name: secret-volume
         secret:
           secretName: my-secret

## Managing Secrets

View Secrets:

     kubectl get secrets
     kubectl describe secret my-secret

Decode Secrets:

    kubectl get secret my-secret -o jsonpath='{.data.username}' | base64 -d

Edit Secrets:

    kubectl edit secret my-secret

Delete Secrets:

    kubectl delete secret my-secret

    
        
<div align="center">

# **Kubectl Commands**

</div>

    * kubectl get nodes - display cluster nodes.
    * kubectl get pods -A - display all pods on cluster.
    * kubectl delete pod <pod_Name> - delete pod.
    * kubectl describe <pod_Name> - describe pod info.
    * kubectl logs <pod_Name> - display pods log.

## cluster commands

    * sudo systemctl status kublete - check basic k8s kublete status.
    * sudo system restart kubelete - way to refresh API connection.
    * kubectl describe configmap kubeadm-config -n kube-system - display Cluser info

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
