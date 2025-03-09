

<div align="center">

# **OpenEBS MayaStore**

</div>

 a software-defined storage solution for Kubernetes that provides persistent storage for applications. It allows you to create and manage storage volumes that can be used by your Kubernetes pods. 
 MayaStore is part of OpenEBS and works well with cloud-native applications, providing scalable and highly available storage.

 Key Features of MayaStore:

   * Dynamic Provisioning: Automatically creates storage volumes when needed by Kubernetes pods.
   * Highly Available: Ensures your data is replicated and available even if a pod or node fails.
   * Snapshot Support: Allows you to take backups of your data.
   * Easy to Use: Seamless integration with Kubernetes for managing persistent storage.


<div align="center">

# **install**

</div>

## Prerequisites

  * minimum 3 workers nodes.
  * each node with an empty drive attached (for the storage).

## 1. install Helm

__On each Worker Node:__

     curl -o http://raw.githubusercontent.com/helm/helm/main/script/get-helm-3
     ./get-helm-3

verify installatin:

    helm version

## 2. install nvme-tcp (needed for super-fast-storage like SSD) 

fast storage technology used in modern computers. It's designed to make use of solid-state drives (SSDs) that connect directly to the computer’s motherboard through a high-speed interface (like PCIe).

__On each Worker Node:__

check if already install

    modinfo nvme-tcp

if not install:

   sudo apt install linux-modules-extra-$(uname -r) -y

if not running:

    sudo modprobe nvme-tcp

set it perment (after restart):

    echo "nvme-tcp" | sudo tee -a /etc/modules

## 3.  prepering HugePages

allows the system to use larger memory pages than the default size (which is typically 4KB). By using larger memory pages (like 2MB or 1GB), systems can reduce the overhead of managing a
large number of smaller pages, which can lead to better performance, especially for memory-intensive applications.

__On each Worker Node:__

(swap must be turn off)

Get information related to HugePages:

    cat /proc/meminfo | grep HugePages

configure the number of HugePages available for the system (improve performance for memory-intensive applications.):

    echo 1024 | sudo tee /sys/kernel/mm/hugepages/hugepages-2048kb/nr_hugepages

make the HugePages configuration persistent across reboots (configure the system so that when the system is rebooted, it will automatically allocate 1024 HugePages):

    echo vm.nr_hugepages=1024 | sudo tee -a /etc/sysctl.conf

## 4. labeling Nodes

specify which nodes should handle specific storage tasks (like hosting volumes or managing persistent data). Labeling nodes helps OpenEBS know which node should run storage workloads,
ensuring proper resource allocation and management.

Node is being assigned to run Mayastor for providing storage (repeat this step for each Worker Node - Labeling each node for Mayastor):

     kubectl label nodes <node-name> openebs.io/engine=mayastor

## 5. Install OpenEBS & Mayastor

execute on the Control plane (once):

    helm repo add openebs http://openebs.github.io/charts
    helm repo update
    helm repo add mayastor http://openebs.github.io/mayastor-extensions/
    helm install mayastor mayastor/mayastor -n mayastor --create-namespace

* if needed to change the replica count (defult is set to 3 replica's):

    kubectl edit sts openebs-etcd -n openebs

  change replicas to the number requiered (ex. 2)

  remove the line (to be the same as the replica number): ETCD_INITIAL_CLUSTER_CTCD

## 6.  Setting Disk-pool (YAML)

__For each of the Worker Node:__

    apiVersion: "openebs.io/v1beta1"
    kind: DiskPool
    metadata:
      name: pool-on-node-1 # name of the pool. should be uqniqe for each node.
      namespace: mayastor
    spec:
      node: workernode-1-hostname # name of the Working node.
      disks: ["/dev/disk/by-id/<id>"]


apply the files:

    kubectl apply -f <Disk-pool.yaml>

## 7. Create StorageClass

provisioner that will manage the storage (Mayastor's provisioner).

    apiVersion: storage.k8s.io/v1
    kind: StorageClass
    metadata:
      name: mayastor-3
    parameters:
      ioTimeout: "30"
      protocol: nvmf
      replicaCount: "3"   # number of replicas for Mayastor volumes.
    provisioner: io.openebs.csi-mayastor

   
